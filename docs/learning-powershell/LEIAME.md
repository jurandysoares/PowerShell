# Aprendendo Powershell

Quer você seja um desenvolvedor, um DevOps ou um profissional de TI, este documento o ajudará a começar a usar o PowerShell.
Neste documento, cobriremos o seguinte:
instalação do PowerShell, passo a passo de exemplos, editor do PowerShell, depurador, ferramentas de teste e um livro de mapas para usuários experientes do bash para começar a usar o PowerShell mais rapidamente.

Os exercícios neste documento têm como objetivo fornecer uma base sólida sobre como usar o PowerShell.
Você não será um guru do PowerShell ao final da leitura deste material, mas estará no caminho certo com o conjunto certo de conhecimentos para começar a usar o PowerShell.

Se você tem 30 minutos agora, vamos tentar.

## Instalando PowerShell

Primeiro você precisa configurar o ambiente de trabalho do seu computador, caso ainda não tenha feito isso.
Escolha a plataforma abaixo e siga as instruções.
No final deste exercício, você deverá conseguir iniciar a sessão do PowerShell.

- Obtenha o PowerShell instalando o pacote
    * [PowerShell no Linux][inst-linux]
    * [PowerShell no macOS][inst-macos]
    * [PowerShell no Windows][inst-win]

  Para este tutorial, você não precisa instalar o PowerShell se estiver executando no Windows.
  Você pode iniciar o console do PowerShell pressionando a tecla Windows, digitando PowerShell e clicando em Windows PowerShell.
  No entanto, se você quiser experimentar o PowerShell mais recente, siga o [PowerShell no Windows][inst-win].

- Como alternativa, você pode obter o PowerShell [construindo-o][build-powershell]

[build-powershell]:../../README.md#building-the-repository
[inst-linux]: https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux
[inst-win]: https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-windows
[inst-macos]: https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos

## Introdução ao PowerShell

Os comandos do PowerShell seguem uma semântica Verbo-Substantivo com um conjunto de parâmetros.
É fácil aprender e usar o PowerShell.
Por exemplo, `Get-Process` exibirá todos os processos em execução em seu sistema.
Vamos examinar alguns exemplos do [Guia do PowerShell para iniciantes] (powershell-guia-para-iniciante.md).

Agora você aprendeu o básico do PowerShell.
Continue lendo se você deseja fazer algum trabalho de desenvolvimento no PowerShell.

### Editor PowerShell

Nesta seção, você criará um script do PowerShell usando um editor de texto.
Você pode usar seu editor favorito para escrever scripts.
Usamos o Visual Studio Code (VS Code), que funciona no Windows, Linux e macOS.
Clique no link a seguir para criar seu primeiro script PowerShell.

- [Using Visual Studio Code (VS Code)](https://docs.microsoft.com/powershell/scripting/dev-cross-plat/vscode/using-vscode)

### Depurador PowerShell

A depuração pode ajudá-lo a encontrar bugs e corrigir problemas em seus scripts do PowerShell.
Clique no link abaixo para saber mais sobre depuração:

- [Using Visual Studio Code (VS Code)](https://docs.microsoft.com/powershell/scripting/dev-cross-plat/vscode/using-vscode#debugging-with-visual-studio-code)
- [PowerShell Command-line Debugging][cli-debugging]

[cli-debugging]:./debugging-from-commandline.md

### Teste do PowerShell

Recomendamos o uso da ferramenta de teste Pester, que é iniciada pela Comunidade PowerShell para escrever casos de teste.
Para usar a ferramenta, leia os [Guias do Pester](https://github.com/pester/Pester) e [Escrevendo Diretrizes de Testes Pester](https://github.com/PowerShell/PowerShell/blob/master/docs/testing-guidelines/WritingPesterTests.md).

### Livro de mapas para usuários experientes do Bash

A tabela a seguir lista o uso de alguns comandos básicos para ajudá-lo a começar a usar o PowerShell mais rapidamente.
Observe que todos os comandos bash devem continuar funcionando na sessão do PowerShell.

| Bash                            | PowerShell                              | Descrição
|:--------------------------------|:----------------------------------------|:---------------------
| ls                              | dir, Get-ChildItem                      | Listar arquivos e pastas
| tree                            | dir -Recurse, Get-ChildItem -Recurse    | Lista todos os arquivos e pastas
| cd                              | cd, Set-Location                        | Alterar diretório
| pwd                             | pwd, $pwd, Get-Location                 | Mostrar diretório de trabalho
| clear, Ctrl+L, reset            | cls, clear                              | Limpar tela
| mkdir                           | New-Item -ItemType Directory            | Criar uma nova pasta
| touch test.txt                  | New-Item -Path test.txt                 | Crie um novo arquivo vazio
| cat test1.txt test2.txt         | Get-Content test1.txt, test2.txt        | Exibir o conteúdo dos arquivos
| cp ./source.txt ./dest/dest.txt | Copy-Item source.txt dest/dest.txt      | Copiar um arquivo
| cp -r ./source ./dest           | Copy-Item ./source ./dest -Recurse      | Copiar recursivamente de uma pasta para outra
| mv ./source.txt ./dest/dest.txt | Move-Item ./source.txt ./dest/dest.txt  | Mova um arquivo para outra pasta
| rm test.txt                     | Remove-Item test.txt                    | Excluir um arquivo
| rm -r &lt;folderName>           | Remove-Item &lt;folderName> -Recurse    | Apagar uma pasta
| find -name build*               | Get-ChildItem build* -Recurse           | Encontre um arquivo ou pasta começando com 'build'
| grep -Rin "sometext" --include="*.cs" | Get-ChildItem -Recurse -Filter *.cs <br> \| Select-String -Pattern "sometext" | Pesquisa recursivamente sem distinção entre maiúsculas e minúsculas para texto em arquivos
| curl https://github.com         | Invoke-RestMethod https://github.com    | Transferir dados de ou para a web

### Treinamento e Leitura Recomendados

- Microsoft Virtual Academy: [Getting Started with PowerShell][getstarted-with-powershell]
- [Why Learn PowerShell][why-learn-powershell] by Ed Wilson
- PowerShell Web Docs: [Basic cookbooks][basic-cookbooks]
- [The Guide to Learning PowerShell][ebook-from-Idera] by Tobias Weltner
- [PowerShell-related Videos][channel9-learn-powershell] on Channel 9
- [PowerShell Quick Reference Guides][quick-reference] by PowerShellMagazine.com
- [Learn PowerShell Video Library][idera-learn-powershell] from Idera
- [PowerShell 5 How-To Videos][script-guy-how-to] by Ed Wilson
- [PowerShell Documentation](https://docs.microsoft.com/powershell)
- [Interactive learning with PSKoans](https://aka.ms/pskoans)

### Recursos Comerciais

- [Windows PowerShell in Action][in-action] by [Bruce Payette](https://github.com/brucepay)
- [Introduction to PowerShell][powershell-intro] from Pluralsight
- [PowerShell Training and Tutorials][lynda-training] from Lynda.com
- [Learn Windows PowerShell in a Month of Lunches][learn-win-powershell] by Don Jones and Jeffrey Hicks
- [Learn PowerShell in a Month of Lunches][learn-powershell] by Travis Plunk (@TravisEz13),
  Tyler Leonhardt (@tylerleonhardt), Don Jones, and Jeffery Hicks

[in-action]: https://www.amazon.com/Windows-PowerShell-Action-Second-Payette/dp/1935182137
[powershell-intro]: https://www.pluralsight.com/courses/powershell-intro
[lynda-training]: https://www.lynda.com/PowerShell-training-tutorials/5779-0.html
[learn-win-powershell]: https://www.amazon.com/Learn-Windows-PowerShell-Month-Lunches/dp/1617294160
[learn-powershell]: https://www.manning.com/books/learn-powershell-in-a-month-of-lunches-linux-and-macos-edition

[getstarted-with-powershell]: https://channel9.msdn.com/Series/GetStartedPowerShell3
[why-learn-powershell]: https://blogs.technet.microsoft.com/heyscriptingguy/2014/10/18/weekend-scripter-why-learn-powershell/
[ebook-from-Idera]:https://www.idera.com/resourcecentral/whitepapers/powershell-ebook
[channel9-learn-powershell]: https://channel9.msdn.com/Search?term=powershell#ch9Search
[idera-learn-powershell]: https://community.idera.com/database-tools/powershell/video_library/
[quick-reference]: https://www.powershellmagazine.com/2014/04/24/windows-powershell-4-0-and-other-quick-reference-guides/
[script-guy-how-to]:https://blogs.technet.microsoft.com/tommypatterson/2015/09/04/ed-wilsons-powershell5-videos-now-on-channel9-2/
[basic-cookbooks]:https://docs.microsoft.com/powershell/scripting/samples/sample-scripts-for-administration
