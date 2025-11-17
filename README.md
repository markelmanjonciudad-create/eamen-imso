# powershell


# Contraseña común para todos los usuarios
$commonPassword = ConvertTo-SecureString "12345Abcde" -AsPlainText -Force

# -------------------------
# Crear grupos
# -------------------------
New-LocalGroup -Name "Trabajadores" -Description "Grupo de trabajadores"
New-LocalGroup -Name "Responsables" -Description "Grupo de responsables"

# -------------------------
# Crear usuarios Trabajador1..5
# Cuentas caducan en 1 año
# -------------------------
for ($i=1; $i -le 5; $i++) {
    $username = "Trabajador$i"
    $user = New-LocalUser -Name $username -Password $commonPassword -AccountExpires (Get-Date).AddYears(1) -FullName "Trabajador $i" -Description "Usuario trabajador"
    Add-LocalGroupMember -Group "Trabajadores" -Member $username
}

# -------------------------
# Crear usuarios Responsable1 y Responsable2
# -------------------------
for ($i=1; $i -le 2; $i++) {
    $username = "Responsable$i"
    $user = New-LocalUser -Name $username -Password $commonPassword -FullName "Responsable $i" -Description "Usuario responsable"
    Add-LocalGroupMember -Group "Responsables" -Member $username
}

# -------------------------
# Crear usuario Informatico
# Contraseña nunca expira, pertenece a Administradores
# -------------------------
New-LocalUser -Name "Informatico" -Password $commonPassword -FullName "Informatico" -Description "Usuario con permisos de administrador" -PasswordNeverExpires $true
Add-LocalGroupMember -Group "Administradores" -Member "Informatico"

# -------------------------
# Crear usuario nuevo_usuario
# -------------------------
New-LocalUser -Name "nuevo_usuario" -Password $commonPassword -FullName "Nuevo Usuario" -Description "Usuario adicional"

# -------------------------
# Comprobaciones
# -------------------------

# Listar miembros de Trabajadores
Write-Host "Miembros del grupo Trabajadores:"
Get-LocalGroupMember -Group "Trabajadores"

# Listar miembros de Responsables
Write-Host "`nMiembros del grupo Responsables:"
Get-LocalGroupMember -Group "Responsables"

# Ver propiedades de un usuario de cada grupo
Write-Host "`nPropiedades de Trabajador1:"
Get-LocalUser -Name "Trabajador1" | Format-List *

Write-Host "`nPropiedades de Responsable1:"
Get-LocalUser -Name "Responsable1" | Format-List *


#linux 
su - alum1
touch listado.txt prueba.txt
exit

su - alum2
touch docum.txt
exit

su - usuadm
touch notas.txt
mkdir compartir
touch compartir/ejercicios.txt
exit



