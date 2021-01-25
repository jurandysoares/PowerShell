# Guia do PowerShell para iniciantes

Se você for novo no PowerShell, este documento o guiará por alguns exemplos para lhe dar algumas idéias básicas do PowerShell. 
Recomendamos que você abra uma console/sessão do PowerShell e digite junto com as instruções deste documento para obter o máximo deste exercício.

## Inicie a console/sessão do PowerShell

Primeiro, você precisa iniciar uma sessão do PowerShell seguindo o [Guia de instalação do PowerShell](./README.md#installation-powershell).

## Familiarizando-se com os comandos do PowerShell

Nesta seção, você aprenderá como

- criar um arquivo, excluir um arquivo e alterar o diretório do arquivo
- descubra qual versão do PowerShell você está usando atualmente
- sair de uma sessão do PowerShell
- peça ajuda se precisar
- encontre a sintaxe dos cmdlets do PowerShell
- e mais

Conforme mencionado acima, os comandos do PowerShell são projetados para ter uma estrutura Verbo-substantivo, por exemplo `Get-Process`,` Set-Location`, `Clear-Host`, etc.
Vamos exercitar alguns dos comandos básicos do PowerShell, também conhecidos como **cmdlets**.

Observe que usaremos o sinal de prompt do PowerShell **PS />** conforme aparece no Linux nos exemplos a seguir.
Ele é mostrado como `PS C: \>` no Windows.

1. `Get-Process`: Obtém os processos em execução no computador local ou remoto.
   
    Por padrão, você receberá dados semelhantes aos seguintes:

    ```powershell
    PS /> Get-Process

    Handles   NPM(K)    PM(K)     WS(K)     CPU(s)     Id    ProcessName
    -------  ------     -----     -----     ------     --    -----------
        -      -          -           1      0.012     12    bash
        -      -          -          21     20.220    449    powershell
        -      -          -          11     61.630   8620    code
        -      -          -          74    403.150   1209    firefox

    …
    ```

    Interessado apenas na instância do processo do Firefox que está sendo executado no seu computador?

    Experimente isto:

    ```powershell
    PS /> Get-Process -Name firefox

    Handles   NPM(K)    PM(K)     WS(K)    CPU(s)     Id   ProcessName
    -------  ------     -----     -----    ------     --   -----------
        -      -          -          74   403.150   1209   firefox

    ```

    Deseja obter de volta mais de um processo?
    Em seguida, basta especificar os nomes dos processos e separá-los com vírgulas.

    ```powershell
    PS /> Get-Process -Name firefox, powershell
    Handles   NPM(K)    PM(K)     WS(K)    CPU(s)     Id   ProcessName
    -------  ------     -----     -----    ------     --   -----------
        -      -          -          74   403.150   1209   firefox
        -      -          -          21    20.220    449   powershell

    ```

2. `Clear-Host`: Limpa a exibição no programa host.

    ```powershell
    PS /> Get-Process
    PS /> Clear-Host
    ```

    Digitou muito apenas para limpar a tela?

    Veja como o *alias* pode ajudar.

3. `Get-Alias`: Obtém os aliases da sessão atual.


    ```powershell
    Get-Alias

    CommandType     Name
    -----------     ----
    …

    Alias           cd -> Set-Location
    Alias           cls -> Clear-Host
    Alias           clear -> Clear-Host
    Alias           copy -> Copy-Item
    Alias           dir -> Get-ChildItem
    Alias           gc -> Get-Content
    Alias           gmo -> Get-Module
    Alias           ri -> Remove-Item
    Alias           type -> Get-Content
    …
    ```

    Como você pode ver, `cls` ou ` clear` são apelidos para `Clear-Host`.

    Agora tente:

    ```powershell
    PS /> Get-Process
    PS /> cls
    ```

4. `cd -> Set-Location`: Define o local de trabalho atual para um local especificado.

    ```powershell
    PS /> Set-Location /home
    PS /home>
    ```

5. `dir -> Get-ChildItem`: Obtém os itens e itens filho em um ou mais locais especificados.

    ```powershell
    # Obtenha todos os arquivos no diretório atual:
    PS /> Get-ChildItem

    # Obtenha todos os arquivos no diretório atual, bem como seus subdiretórios:
    PS /> cd $home
    PS /> dir -Recurse

    # Lista todos os arquivos com a extensão "txt".
    PS /> cd $home
    PS /> dir –Path *.txt -Recurse
    ```

6. `New-Item`: Cria um novo item.

    ```powershell
    # Um arquivo vazio será criado se você digitar o seguinte:

    PS /> New-Item -Path ./teste.txt


        Directory: /


    Mode                LastWriteTime         Length  Name
    ----                -------------         ------  ----
    -a----         7/7/2016   7:17 PM              0  test.txt
    ```

    Você pode usar o parâmetro `-Value` para adicionar alguns dados ao seu arquivo.

    Por exemplo, o comando a seguir adiciona a frase `Olá mundo!` Como um conteúdo de arquivo em `teste.txt`.

    Como o arquivo `teste.txt` já existe, usamos o parâmetro` -Force` para substituir o conteúdo existente.

    ```powershell
    PS /> New-Item -Path ./teste.txt -Value Olá mundo!" -Force

        Directory: /


    Mode                LastWriteTime         Length  Name
    ----                -------------         ------  ----
    -a----         7/7/2016   7:19 PM             24  test.txt

    ```

    Existem outras maneiras de adicionar alguns dados a um arquivo.

    Por exemplo, você pode usar `Set-Content` para definir o conteúdo do arquivo:

    ```powershell
    PS />Set-Content -Path ./teste.txt -Value "Olá mundo novamente!"
    ```

    Ou simplesmente use `>` como abaixo:

    ```powershell
    # Crie um arquivo vazio
    "" > teste.txt

    # define "Olá, mundo!!!" como conteúdo do arquivo teste.txt
    "Olá mundo!!!" > teste.txt

    ```

    O sinal de cerquilha `#` acima é usado para comentários no PowerShell.

7. `type -> Get-Content`: Obtém o conteúdo do item no local especificado.

    ```powershell
    PS /> Get-Content -Path ./teste.txt
    PS /> type -Path ./teste.txt

    Olá mundo!!!
    ```

8. `del -> Remove-Item`: Exclui os itens especificados.

    Este cmdlet excluirá o arquivo `/ home / jen / test.txt`:

    ```powershell
    PS /> Remove-Item ./test.txt
    ```

9.  `$PSVersionTable`: Exibe a versão do PowerShell que você está usando no momento.

    Digite `$PSVersionTable` em sua sessão do PowerShell, você verá algo como abaixo.
    "PSVersion" indica a versão do PowerShell que você está usando.

    ```powershell
    Name                           Value
    ----                           -----
    PSVersion                      6.0.0-alpha
    PSEdition                      Core
    PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
    BuildVersion                   3.0.0.0
    GitCommitId                    v6.0.0-alpha.12
    CLRVersion
    WSManStackVersion              3.0
    PSRemotingProtocolVersion      2.3
    SerializationVersion           1.1.0.1

    ```

10. `Exit`: Para sair da sessão do PowerShell, digite `exit`.

    ```powershell
    exit
    ```

## Preciso de ajuda?

O comando mais importante no PowerShell é possivelmente o `Get-Help`, que permite que você aprenda rapidamente o PowerShell sem ter que pesquisar na Internet.

O cmdlet `Get-Help` também mostra como os comandos do PowerShell funcionam com exemplos.

Mostra a sintaxe e outras informações técnicas do cmdlet `Get-Process`.

```powershell
PS /> Get-Help -Name Get-Process
```

Ele exibe os exemplos de como usar o cmdlet `Get-Process`.

```powershell
PS />Get-Help -Name Get-Process -Examples
```

Se você usar o parâmetro **-Full**, por exemplo, `Get-Help -Name Get-Process -Full`, ele exibirá mais informações técnicas.

## Descubra comandos disponíveis em seu sistema

Você quer descobrir quais cmdlets do PowerShell estão disponíveis em seu sistema? Basta executar `Get-Command` conforme abaixo:

```powershell
PS /> Get-Command
```

Se você deseja saber se um cmdlet específico existe em seu sistema, você pode fazer algo como a seguir:

```powershell
PS /> Get-Command Get-Process
```

Se você deseja saber a sintaxe do cmdlet `Get-Process`, digite:

```powershell
PS /> Get-Command Get-Process -Syntax
```

Se você quiser saber como usar o `Get-Process`, digite:

```powershell
PS /> Get-Help Get-Process -Example
```

## Pipeline do PowerShell `|`

Às vezes, ao executar Get-ChildItem ou "dir", você deseja obter uma lista de arquivos e pastas em ordem decrescente.
Para conseguir isso, digite:

```powershell
PS /> dir | Sort-Object -Descending
```

Digamos que você queira obter o maior arquivo de um diretório

```powershell
PS /> dir | Sort-Object -Property Length -Descending | Select-Object -First 1


    Directory: /


Mode                LastWriteTime       Length  Name
----                -------------       ------  ----
-a----        5/16/2016   1:15 PM        32972  test.log

```

## Como criar e executar scripts do PowerShell

Você pode usar o Visual Studio Code ou seu editor favorito para criar um script PowerShell e salvá-lo com uma extensão de arquivo `.ps1`.
Para obter mais detalhes, consulte [Criar e executar PowerShell Script Guide] [create-run-script]

## Treinamento e Leitura Recomendados

- Vídeo: [Introdução ao PowerShell][remoting] do Channel9
- [eBooks do PowerShell.org](https://leanpub.com/u/devopscollective)
- [Lista de eBooks][ebook-list] de Martin Schvartzman
- [Tutorial do MVP][tutorial]
- Script Guy blog: [The best way to Learn PowerShell][to-learn]
- [Understanding PowerShell Module][ps-module]
- [How and When to Create PowerShell Module][create-ps-module] by Adam Bertram
- Video: [PowerShell Remoting in Depth][in-depth] from Channel9
- [PowerShell Basics: Remote Management][remote-mgmt] from ITPro
- [Running Remote Commands][remote-commands] from PowerShell Web Docs
- [Samples for Writing a PowerShell Script Module][examples-ps-module]
- [Writing a PowerShell module in C#][writing-ps-module]
- [Examples of Cmdlets Code][sample-code]

## Recursos Comerciais

- [Windows PowerShell in Action][in-action] by Bruce Payette
- [Windows PowerShell Cookbook][cookbook] by Lee Holmes

[in-action]: https://www.amazon.com/Windows-PowerShell-Action-Bruce-Payette/dp/1633430294
[cookbook]: http://shop.oreilly.com/product/9780596801519.do
[ebook-list]: https://martin77s.wordpress.com/2014/05/26/free-powershell-ebooks/
[tutorial]: https://www.computerperformance.co.uk/powershell/index-13/
[to-learn]:https://blogs.technet.microsoft.com/heyscriptingguy/2015/01/04/weekend-scripter-the-best-ways-to-learn-powershell/
[ps-module]:https://docs.microsoft.com/powershell/scripting/developer/module/understanding-a-windows-powershell-module
[create-ps-module]:https://www.business.com/articles/powershell-modules/
[remoting]:https://channel9.msdn.com/Series/GetStartedPowerShell3/06
[in-depth]: https://channel9.msdn.com/events/MMS/2012/SV-B406
[remote-mgmt]:https://www.itprotoday.com/powershell/powershell-basics-remote-management
[remote-commands]:https://docs.microsoft.com/powershell/scripting/learn/remoting/running-remote-commands
[examples-ps-module]:https://docs.microsoft.com/powershell/scripting/developer/module/how-to-write-a-powershell-script-module
[writing-ps-module]:https://www.powershellmagazine.com/2014/03/18/writing-a-powershell-module-in-c-part-1-the-basics/
[sample-code]:https://docs.microsoft.com/powershell/scripting/developer/cmdlet/examples-of-cmdlet-code
[create-run-script]:./create-powershell-scripts.md
