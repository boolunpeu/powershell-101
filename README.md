# windows-101

In this repo you will find 2 .md files explaining what i did and what i learned about windows and his shell environnement + a csv file which results from a powershell script

Here is the script : 

`#Get System Info

$systemInfo = Get-WmiObject -Class Win32_ComputerSystem

$osInfo = Get-WmiObject -Class Win32_OperatingSystem

$processorInfo = Get-WmiObject -Class Win32_Processor

$memoryInfo = Get-WmiObject -Class Win32_PhysicalMemory

#Create an object containing the system info

$pcInfo = [PSCustomObject]@{
- "Fabricant du système" = $systemInfo.Manufacturer
- "Modèle du système" = $systemInfo.Model
- "Nom du système" = $systemInfo.Name
- "Type du système" = $systemInfo.SystemType
- "Nombre de processeurs" = $systemInfo.NumberOfProcessors
- "Nombre de cœurs du processeur" = $processorInfo.NumberOfCores
- "Processeur" = $processorInfo.Name
- "Mémoire installée (Go)" = [math]::Round($systemInfo.TotalPhysicalMemory / 1GB, 2)
- "Nom du système d'exploitation" = $osInfo.Caption
- "Version du système d'exploitation" = $osInfo.Version
- "Architecture du système d'exploitation" = $osInfo.OSArchitecture
}

#Export to CSV

$pcInfo | Export-Csv -Path "pc_specs.csv" -NoTypeInformation

Write-Host "Les spécifications du PC ont été enregistrées dans pc_specs.csv"`

