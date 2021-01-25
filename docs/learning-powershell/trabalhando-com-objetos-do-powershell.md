# Trabalhando com objetos PowerShell

Quando os cmdlets são executados no PowerShell, a saída é um objeto, ao contrário de apenas retornar texto.
Isso fornece a capacidade de armazenar informações como propriedades.
Como resultado, lidar com grandes quantidades de dados e obter apenas propriedades específicas é uma tarefa trivial.

Como um exemplo simples, a função a seguir recupera informações sobre dispositivos de armazenamento em uma plataforma de sistema operacional Linux ou MacOS.
Isso é feito analisando a saída de um comando existente, * parted -l * no contexto administrativo, e criando um objeto a partir do texto bruto usando o cmdlet * New-Object *.

```powershell
function Get-DiskInfo
{
    $disks = sudo parted -l | Select-String "Disk /dev/sd*" -Context 1,0
    $diskinfo = @()
    foreach ($disk in $disks) {
        $diskline1 = $disk.ToString().Split("`n")[0].ToString().Replace('  Model: ','')
        $diskline2 = $disk.ToString().Split("`n")[1].ToString().Replace('> Disk ','')
        $i = New-Object psobject -Property @{'Friendly Name' = $diskline1; Device=$diskline2.Split(': ')[0]; 'Total Size'=$diskline2.Split(':')[1]}
        $diskinfo += $i
    }
    $diskinfo
}
```

Execute a função e armazene os resultados como uma variável.
Agora recupere o valor da variável.
Os resultados são formatados como uma tabela com a visualização padrão.

*Observação: neste exemplo, os discos são discos virtuais em uma máquina virtual do Microsoft Azure.*

```powershell
PS /home/psuser> $d = Get-DiskInfo
[sudo] password for psuser:
PS /home/psuser> $d

Friendly Name            Total Size Device
-------------            ---------- ------
Msft Virtual Disk (scsi)  31.5GB    /dev/sda
Msft Virtual Disk (scsi)  145GB     /dev/sdb

```

Passar a variável pelo pipeline para *Get-Member* revela métodos e propriedades disponíveis.This is because the value of *$d* is not just text output.
O valor é na verdade uma matriz de objetos `.Net` com métodos e propriedades.
As propriedades incluem Dispositivo (*Device*), Nome amigável (*Friendly Name*) e Tamanho total (*Total Size*).

```powershell
PS /home/psuser> $d | Get-Member


   TypeName: System.Management.Automation.PSCustomObject

Name          MemberType   Definition
----          ----------   ----------
Equals        Method       bool Equals(System.Object obj)
GetHashCode   Method       int GetHashCode()
GetType       Method       type GetType()
ToString      Method       string ToString()
Device        NoteProperty string Device=/dev/sda
Friendly Name NoteProperty string Friendly Name=Msft Virtual Disk (scsi)
Total Size    NoteProperty string Total Size= 31.5GB
```

Para confirmar, podemos chamar o método `GetType ()` interativamente do console.

```powershell
PS /home/psuser> $d.GetType()

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     True     Object[]                                 System.Array
```

Para indexar na matriz e retornar apenas objetos específicos, use os colchetes.

```powershell
PS /home/psuser> $d[0]

Friendly Name            Total Size Device
-------------            ---------- ------
Msft Virtual Disk (scsi)  31.5GB    /dev/sda

PS /home/psuser> $d[0].GetType()

IsPublic IsSerial Name                                     BaseType
-------- -------- ----                                     --------
True     False    PSCustomObject                           System.Object
```

Para retornar uma propriedade específica, o nome da propriedade pode ser chamado interativamente no console.

```powershell
PS /home/psuser> $d.Device
/dev/sda
/dev/sdb
```

Para gerar uma exibição das informações diferente do padrão, como uma exibição com apenas propriedades específicas selecionadas, passe o valor para o cmdlet *Select-Object*.

```powershell
PS /home/psuser> $d | Select-Object Device, 'Total Size'

Device   Total Size
------   ----------
/dev/sda  31.5GB
/dev/sdb  145GB
```

Por fim, o exemplo abaixo demonstra o uso do cmdlet *ForEach-Object* para iterar pela matriz e manipular o valor de uma propriedade específica de cada objeto.
Neste caso, a propriedade Tamanho Total, que era fornecida em Gigabytes, é alterada para Megabytes.
Alternativamente, indexe em uma posição na matriz conforme mostrado abaixo no terceiro exemplo.

```powershell
PS /home/psuser> $d | ForEach-Object 'Total Size'
 31.5GB
 145GB

PS /home/psuser> $d | ForEach-Object {$_.'Total Size' / 1MB}
32256
148480

PS /home/psuser> $d[1].'Total Size' / 1MB
148480
```
