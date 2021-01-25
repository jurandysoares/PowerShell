# Como criar e executar scripts do PowerShell

Você pode combinar uma série de comandos em um arquivo de texto e salvá-lo com a extensão de arquivo '.ps1', e o arquivo se tornará um script do PowerShell.
Isso começaria abrindo seu editor de texto favorito e colando no exemplo a seguir.

```powershell
# Script para retornar endereços IPv4 atuais em um host Linux ou MacOS
$ipInfo = ifconfig | Select-String 'inet'
$ipInfo = [regex]::matches($ipInfo,"addr:\b(?:\d{1,3}\.){3}\d{1,3}\b") | ForEach-Object value
foreach ($ip in $ipInfo)
{
    $ip.Replace('addr:','')
}
```

Nota do tradutor: O comando `ifconfig` não costuma vir mais nas distribuições Linux. Em seu lugar, costuma vir o comando `ip` que, com o subcomando `address`, fornece os endereços das interfaces de rede e, com as opções `-4` e `-json`, lista somente os endereços IPv4 e no formato JSON.

```powershell
ip -json -4 addr | ConvertFrom-Json | ForEach-Object {$_.addr_info.local}
```

Em seguida, salve o arquivo em algo memorável, como `. \ NetIP.ps1`.
No futuro, quando você precisar obter os endereços IP para o nó, poderá simplificar essa tarefa executando o script.

```powershell
.\NetIP.ps1
10.0.0.1
127.0.0.1
```

Você pode realizar essa mesma tarefa no Windows.

```powershell
# One line script to return current IPv4 addresses on a Windows host
Get-NetIPAddress | Where-Object {$_.AddressFamily -eq 'IPv4'} | ForEach-Object IPAddress
```

Como antes, salve o arquivo como `. \ NetIP.ps1` e execute em um ambiente PowerShell.

Nota: Se você estiver usando o Windows, certifique-se de definir a política de execução do PowerShell como "RemoteSigned" neste caso.

Consulte [Executar scripts do PowerShell é tão fácil quanto 1-2-3][run-ps] para obter mais detalhes.

```powershell
.\NetIP.ps1
127.0.0.1
10.0.0.1
```

## Criação de um script que pode realizar a mesma tarefa em vários sistemas operacionais

Se você quiser criar um script que retorne o endereço IP no Linux, MacOS ou Windows, pode fazer isso usando uma instrução IF.

```powershell
# Script para retornar endereços IPv4 atuais para Linux, MacOS ou Windows
$IP = if ($IsLinux) {
    ip -json -4 addr | ConvertFrom-Json | ForEach-Object {$_.addr_info.local}
}
elseif ($IsMacOS)
{
    $ipInfo = ifconfig | Select-String 'inet'
    $ipInfo = [regex]::matches($ipInfo,"addr:\b(?:\d{1,3}\.){3}\d{1,3}\b") | ForEach-Object value
    foreach ($ip in $ipInfo) {
        $ip.Replace('addr:','')
    }
}
else
{
    Get-NetIPAddress | Where-Object {$_.AddressFamily -eq 'IPv4'} | ForEach-Object IPAddress
}

# Remova o endereço de loopback da saída, independentemente da plataforma
$IP | Where-Object {$_ -ne '127.0.0.1'}
```

[run-ps]: https://www.itprotoday.com/powershell/running-powershell-scripts-easy-1-2-3
