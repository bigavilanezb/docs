# 🖥️ Comandos Linux → Windows (PowerShell & CMD)

## 📋 Tabla de Equivalencias Rápidas

| Linux/Mac | Windows PowerShell                       | Windows CMD   | Descripción          |
| --------- | ---------------------------------------- | ------------- | -------------------- |
| `ls`      | `Get-ChildItem` o `ls`                   | `dir`         | Listar archivos      |
| `cd`      | `Set-Location` o `cd`                    | `cd`          | Cambiar directorio   |
| `pwd`     | `Get-Location` o `pwd`                   | `cd`          | Directorio actual    |
| `mkdir`   | `New-Item -ItemType Directory` o `mkdir` | `mkdir`       | Crear carpeta        |
| `rm`      | `Remove-Item` o `rm`                     | `del`         | Eliminar archivo     |
| `rm -rf`  | `Remove-Item -Recurse -Force`            | `rmdir /s /q` | Eliminar carpeta     |
| `cp`      | `Copy-Item` o `cp`                       | `copy`        | Copiar archivo       |
| `mv`      | `Move-Item` o `mv`                       | `move`        | Mover/renombrar      |
| `cat`     | `Get-Content` o `cat`                    | `type`        | Ver contenido        |
| `touch`   | `New-Item -ItemType File`                | `type nul >`  | Crear archivo vacío  |
| `grep`    | `Select-String`                          | `findstr`     | Buscar en texto      |
| `find`    | `Get-ChildItem -Recurse`                 | `dir /s`      | Buscar archivos      |
| `clear`   | `Clear-Host` o `cls`                     | `cls`         | Limpiar pantalla     |
| `echo`    | `Write-Output` o `echo`                  | `echo`        | Imprimir texto       |
| `chmod`   | `icacls`                                 | `icacls`      | Cambiar permisos     |
| `ps`      | `Get-Process`                            | `tasklist`    | Procesos activos     |
| `kill`    | `Stop-Process`                           | `taskkill`    | Matar proceso        |
| `which`   | `Get-Command`                            | `where`       | Ubicación de comando |

---

## 🗂️ Manejo de Archivos y Carpetas

### **Listar archivos**

```powershell
# PowerShell
ls                          # Listado básico
Get-ChildItem               # Completo
ls -Force                   # Incluye ocultos
ls -Recurse                 # Recursivo (subcarpetas)

# CMD
dir
dir /a                      # Incluye ocultos
dir /s                      # Recursivo
```

### **Crear carpeta**

```powershell
# PowerShell
mkdir mi-carpeta
New-Item -ItemType Directory -Path "mi-carpeta"

# CMD
mkdir mi-carpeta
md mi-carpeta
```

### **Crear archivo vacío**

```powershell
# PowerShell
New-Item -ItemType File -Path "archivo.txt"
"" > archivo.txt            # Alternativa rápida
ni archivo.txt              # Alias corto

# CMD
type nul > archivo.txt
echo. > archivo.txt
```

### **Eliminar archivo**

```powershell
# PowerShell
Remove-Item archivo.txt
rm archivo.txt              # Alias
del archivo.txt             # También funciona

# CMD
del archivo.txt
erase archivo.txt
```

### **Eliminar carpeta (recursivo)**

```powershell
# PowerShell
Remove-Item -Recurse -Force carpeta
rmdir -Recurse -Force carpeta
rm -rf carpeta              # Alias estilo Linux

# CMD
rmdir /s /q carpeta
rd /s /q carpeta
```

### **Copiar archivos**

```powershell
# PowerShell
Copy-Item origen.txt destino.txt
cp origen.txt destino.txt
Copy-Item -Recurse carpeta carpeta-copia  # Carpeta completa

# CMD
copy origen.txt destino.txt
xcopy /e /i carpeta carpeta-copia         # Carpeta completa
```

### **Mover/Renombrar**

```powershell
# PowerShell
Move-Item viejo.txt nuevo.txt
mv viejo.txt nuevo.txt
Rename-Item viejo.txt nuevo.txt  # Solo renombrar

# CMD
move viejo.txt nuevo.txt
ren viejo.txt nuevo.txt          # Solo renombrar
```

---

## 📄 Leer y Buscar Contenido

### **Ver contenido de archivo**

```powershell
# PowerShell
Get-Content archivo.txt
cat archivo.txt             # Alias
gc archivo.txt              # Alias corto
cat archivo.txt | Select-Object -First 10  # Primeras 10 líneas

# CMD
type archivo.txt
more archivo.txt            # Con paginación
```

### **Buscar en archivos (grep)**

```powershell
# PowerShell
Select-String "texto" archivo.txt
cat archivo.txt | Select-String "texto"
Get-ChildItem -Recurse | Select-String "texto"  # En todos los archivos

# CMD
findstr "texto" archivo.txt
findstr /s "texto" *.*      # Recursivo
```

### **Buscar archivos**

```powershell
# PowerShell
Get-ChildItem -Recurse -Filter "*.txt"
ls -Recurse *.txt
Get-ChildItem -Recurse | Where-Object {$_.Name -like "*config*"}

# CMD
dir /s *.txt
dir /s /b *config*          # Solo nombres
```

---

## 🔧 Procesos y Sistema

### **Ver procesos**

```powershell
# PowerShell
Get-Process
ps                          # Alias
Get-Process | Where-Object {$_.Name -like "node*"}

# CMD
tasklist
tasklist | findstr node
```

### **Matar proceso**

```powershell
# PowerShell
Stop-Process -Name "node"
Stop-Process -Id 1234
kill -Name node             # Alias

# CMD
taskkill /IM node.exe /F
taskkill /PID 1234 /F
```

### **Ver puerto en uso**

```powershell
# PowerShell
Get-NetTCPConnection | Where-Object {$_.LocalPort -eq 3000}
netstat -ano | findstr :3000

# CMD
netstat -ano | findstr :3000
```

---

## 🌐 Comandos para Desarrollo Web

### **Limpiar caché de Next.js**

```powershell
# PowerShell
Remove-Item -Recurse -Force .next -ErrorAction SilentlyContinue
Remove-Item -Recurse -Force node_modules -ErrorAction SilentlyContinue
Remove-Item -Recurse -Force .turbo -ErrorAction SilentlyContinue

# CMD
if exist .next rmdir /s /q .next
if exist node_modules rmdir /s /q node_modules
if exist .turbo rmdir /s /q .turbo
```

### **Matar servidor en puerto 3000**

```powershell
# PowerShell
$port = 3000
Get-NetTCPConnection | Where-Object {$_.LocalPort -eq $port} | ForEach-Object {Stop-Process -Id $_.OwningProcess -Force}

# CMD
for /f "tokens=5" %a in ('netstat -ano ^| findstr :3000') do taskkill /F /PID %a
```

### **Crear archivo .env**

```powershell
# PowerShell
@"
NEXT_PUBLIC_SUPABASE_URL=tu-url
NEXT_PUBLIC_SUPABASE_ANON_KEY=tu-key
"@ | Out-File -FilePath .env.local -Encoding UTF8

# CMD
(
echo NEXT_PUBLIC_SUPABASE_URL=tu-url
echo NEXT_PUBLIC_SUPABASE_ANON_KEY=tu-key
) > .env.local
```

---

## 🎨 Navegación y Utilidades

### **Cambiar directorio**

```powershell
# PowerShell & CMD (igual)
cd carpeta
cd ..                       # Subir un nivel
cd ../..                    # Subir dos niveles
cd ~                        # Ir a home (solo PowerShell)
cd D:\proyectos             # Cambiar de disco
```

### **Limpiar pantalla**

```powershell
# PowerShell
Clear-Host
cls                         # Alias
clear                       # Alias

# CMD
cls
```

### **Ver variables de entorno**

```powershell
# PowerShell
Get-ChildItem Env:
$env:PATH
echo $env:NODE_ENV

# CMD
set
echo %PATH%
echo %NODE_ENV%
```

### **Crear variable de entorno temporal**

```powershell
# PowerShell
$env:NODE_ENV = "development"

# CMD
set NODE_ENV=development
```

---

## ⚡ Aliases Útiles para PowerShell

Puedes crear aliases permanentes en tu perfil de PowerShell:

```powershell
# Editar perfil de PowerShell
notepad $PROFILE

# Agregar estos aliases:
Set-Alias -Name ll -Value Get-ChildItem
Set-Alias -Name grep -Value Select-String
Set-Alias -Name which -Value Get-Command

function rmrf { Remove-Item -Recurse -Force $args }
function touch { New-Item -ItemType File $args }
function mkcd { mkdir $args; cd $args }
```

---

## 🔗 Comandos Git (funcionan igual)

```bash
git clone https://github.com/user/repo.git
git add .
git commit -m "mensaje"
git push
git pull
git status
git branch
git checkout -b nueva-rama
```

---

## 💡 Tips Importantes

### **1. PowerShell tiene auto-completado con Tab**

```powershell
Get-Ch[Tab]         # Completa a Get-ChildItem
Remove-It[Tab]      # Completa a Remove-Item
```

### **2. Usar `-ErrorAction SilentlyContinue` para evitar errores**

```powershell
Remove-Item .next -Recurse -Force -ErrorAction SilentlyContinue
```

### **3. Pipelines funcionan similar a Linux**

```powershell
Get-ChildItem | Where-Object {$_.Length -gt 1MB}
ls *.txt | Select-String "error"
```

### **4. Comandos con espacios en rutas**

```powershell
cd "C:\Mis Documentos\Proyecto"
Remove-Item "carpeta con espacios" -Recurse
```

---

## 🚀 Script Útil para Proyectos Next.js

Guarda esto como `clean-nextjs.ps1`:

```powershell
# clean-nextjs.ps1
Write-Host "🧹 Limpiando proyecto Next.js..." -ForegroundColor Cyan

$folders = @(".next", "node_modules", ".turbo", "out")

foreach ($folder in $folders) {
    if (Test-Path $folder) {
        Write-Host "Eliminando $folder..." -ForegroundColor Yellow
        Remove-Item -Recurse -Force $folder
    }
}

Write-Host "✅ Limpieza completada!" -ForegroundColor Green
Write-Host "💿 Reinstalando dependencias..." -ForegroundColor Cyan

pnpm install

Write-Host "🚀 Listo para correr el proyecto!" -ForegroundColor Green
```

**Usar:**

```powershell
.\clean-nextjs.ps1
```

---

## 📚 Recursos

- [PowerShell Docs](https://learn.microsoft.com/en-us/powershell/)
- [CMD Reference](https://ss64.com/nt/)
- [PowerShell vs Bash](https://learn.microsoft.com/en-us/powershell/scripting/learn/ps101/01-getting-started)

---

## 🎯 Resumen de lo Más Usado

```powershell
# Navegación
ls                              # Listar
cd carpeta                      # Cambiar directorio
pwd                             # Directorio actual

# Archivos
New-Item archivo.txt            # Crear archivo
Remove-Item archivo.txt         # Eliminar archivo
cat archivo.txt                 # Ver contenido

# Carpetas
mkdir carpeta                   # Crear carpeta
rmdir -Recurse -Force carpeta   # Eliminar carpeta
cp -Recurse carpeta copia       # Copiar carpeta

# Búsqueda
ls -Recurse *.txt               # Buscar archivos
cat archivo.txt | Select-String "texto"  # Buscar en contenido

# Procesos
Get-Process                     # Ver procesos
Stop-Process -Name node         # Matar proceso
netstat -ano | findstr :3000    # Ver puerto
```

¡Guarda esto para referencia! 🔖
