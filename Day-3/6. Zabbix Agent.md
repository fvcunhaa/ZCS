## **Zabbix Agent Intro**<br>
   **Link:**https://www.zabbix.com/documentation/current/en/manual/concepts/agent<br>

   O agente Zabbix é implantado em um alvo de monitoramento para monitorar ativamente recursos e aplicativos locais (discos rígidos, memória, estatísticas do processador, etc.).<bbr>
   O agente coleta informações operacionais localmente e relata os dados ao servidor Zabbix para processamento adicional. Em caso de falhas (como um disco rígido cheio ou um processo de serviço travado), o servidor Zabbix pode alertar ativamente os administradores sobre a máquina específica que relatou a falha.Os agentes Zabbix são extremamente eficientes devido ao uso de chamadas de sistema nativas para coleta de informações estatísticas. <br>

## **Agent Checks**
   Existem verificações de agentes passivos e ativos. Ao configurar um item, você pode selecionar o tipo necessário:<br>
   Agente Zabbix - para verificações passivas<br>
   Agente Zabbix (ativo) - para verificações ativas<br>

## **Passive and active checks**<br>
   
   Os agentes Zabbix podem realizar verificações passivas e ativas. Em uma verificação passiva, o agente responde a uma solicitação de dados. O servidor Zabbix (ou proxy) solicita dados, por exemplo, carga da CPU, e o agente Zabbix envia de volta o resultado. <br>
   As verificações ativas requerem um processamento mais complexo. O agente deve primeiro recuperar uma lista de itens do servidor Zabbix para processamento independente. Em seguida, ele enviará periodicamente novos valores para o servidor.A execução de verificações passivas ou ativas é configurada selecionando o respectivo tipo de item de monitoramento. O agente Zabbix processa itens do tipo 'agente Zabbix' ou 'agente Zabbix (ativo)'.<br>

   *Supported platforms*<br>
   Zabbix agent is supported for:<br>
   - Linux<br>
   - IBM AIX<br>
   - FreeBSD<br>
   - NetBSD<br>
   - OpenBSD<br>
   - HP-UX<br>
   - Mac OS X<br>
   - Solaris: 9, 10, 11<br>
   - Windows: all desktop and server versions since XP<br>

## **Agent on UNIX-like systems**<br>
   O agente Zabbix em sistemas do tipo UNIX é executado no host que está sendo monitorado.<br>

   **Installation**<br>
    Veja a seção de instalação do pacote para instruções sobre como instalar o agente Zabbix como pacote.<br>
    **Link:** https://www.zabbix.com/documentation/current/en/manual/installation/install_from_packages<br>

   **If installed as package**<br>
   O agente Zabbix é executado como um processo daemon. O agente pode ser iniciado executando:<br>
   - *shell> serviço zabbix-agent start*<br>
   Isso funcionará na maioria dos sistemas GNU/Linux. Em outros sistemas, você pode precisar executar:<br>
   *shell> /etc/init.d/zabbix-agent start*<br>
   Da mesma forma, para parar/reiniciar/visualizar o status do agente Zabbix, use os seguintes comandos:<br>
   *shell> serviço zabbix-agent stop*<br>
   *shell> reinicialização do agente zabbix do serviço*<br>
   *shell> status do agente zabbix do serviço*<br>
   **Obs.:** Se for preciso iniciar manualmente, se o de acima não funcionar, você deve iniciá-lo manualmente. Encontre o caminho para o binário zabbix_agentd e execute:<br> 
   *shell> zabbix_agentd*

## **Agent on Windows**
   O agente Zabbix no Windows é executado como um serviço do Windows.<br>
   Preparação: O agente Zabbix é distribuído como um arquivo zip. Depois de baixar o arquivo, você precisa descompactá-lo. Escolha qualquer pasta para armazenar o agente Zabbix e o arquivo de configuração, e. g.<br>

   C:\zabbix<br>

   Copie os arquivos bin\zabbix_agentd.exe e conf\zabbix_agentd.conf para c:\zabbix.<br>
   Edite o arquivo c:\zabbix\zabbix_agentd.conf de acordo com suas necessidades, certificando-se de especificar um parâmetro "Hostname" correto.<br>
   
   **Installation**
   Feito isso, use o seguinte comando para instalar o agente Zabbix como serviço do Windows:<br>
   C:\> c:\zabbix\zabbix_agentd.exe -c c:\zabbix\zabbix_agentd.conf -i<br>
   Agora você deve poder configurar o serviço "agente Zabbix" normalmente como qualquer outro serviço do Windows.<br>
   Veja mais detalhes sobre como instalar e executar o agente Zabbix no Windows.<br>
   **Link:**https://www.zabbix.com/documentation/6.2/en/manual/appendix/install/windows_agent#installing-agent-as-windows-service <br>

## **Agent 2**<br>
   **Link:**https://www.zabbix.com/documentation/6.2/en/manual/concepts/agent2<br>
   O agente Zabbix 2 é uma nova geração do agente Zabbix e pode ser usado no lugar do agente Zabbix. O agente Zabbix 2 foi desenvolvido para:<br>
   - reduzir o número de conexões TCP<br>
   - fornecer simultaneidade aprimorada de cheques<br>
   - ser facilmente extensível com plugins. Um plugin deve ser capaz de:fornecer verificações triviais que consistem em apenas algumas linhas simples de código; fornecer verificações complexas que consistem em scripts de longa execução e coleta de dados independente com envio periódico dos dados; ser um substituto para o agente Zabbix (na medida em que suporta todas as funcionalidades anteriores).<br>
     O agente 2 é escrito em linguagem de programação Go (com algum código C do agente Zabbix reutilizado). Um ambiente Go configurado com uma versão Go atualmente suportada é necessário para construir o agente Zabbix 2.O Agente 2 não possui suporte de daemonização integrado no Linux; ele pode ser executado como um serviço do Windows.<br>
     As verificações passivas funcionam de maneira semelhante ao agente Zabbix. As verificações ativas suportam intervalos programados/flexíveis e verificam a simultaneidade em um servidor ativo.<br>

## **Command line options**<br>
   Recomendações gerais: Comece entendendo qual componente atua como um cliente TLS e qual atua como um servidor TLS no caso de problema.<br>
   Servidor Zabbix, proxies e agentes, dependendo da interação entre eles, todos podem funcionar como servidores e clientes TLS.<br>
   Por exemplo, o servidor Zabbix conectando-se ao agente para uma verificação passiva, atua como um cliente TLS. O agente está na função de servidor TLS.<br>
   O agente Zabbix, solicitando uma lista de verificações ativas do proxy, atua como um cliente TLS. O proxy está na função de servidor TLS.<br>
   Os utilitários zabbix_get e zabbix_sender sempre atuam como clientes TLS.<br>
   O Zabbix usa autenticação mútua.<br>
   Cada lado verifica seu par e pode recusar a conexão.<br>
   Por exemplo, o servidor Zabbix conectado ao agente pode encerrar a conexão imediatamente se o certificado do agente for inválido. E vice-versa - o agente Zabbix aceitando uma conexão do servidor pode fechar a conexão se o servidor não for confiável para o agente.
   Examine os arquivos de log em ambos os lados - no cliente TLS e no servidor TLS.<br>
   O lado que recusa a conexão pode registrar uma razão precisa pela qual foi recusada. O outro lado geralmente relata um erro bastante geral (por exemplo, "Conexão fechada por peer", "conexão não foi encerrada corretamente").<br>
   Às vezes, a criptografia mal configurada resulta em mensagens de erro confusas que não apontam para a causa real.<br>
   Nas subseções abaixo, tentamos fornecer uma coleção (longe de ser exaustiva) de mensagens e possíveis causas que podem ajudar na solução de problemas.<br>
   Observe que diferentes kits de ferramentas de criptografia (OpenSSL, GnuTLS) geralmente produzem mensagens de erro diferentes nas mesmas situações de problema.<br>
   Às vezes, as mensagens de erro dependem até mesmo de uma combinação específica de kits de ferramentas de criptografia em ambos os lados.<br>

## **Zabbix_get**<br>
   DESCRIÇÃO: zabbix_get é um utilitário de linha de comando para obter dados do agente Zabbix.<br>

   SYNOPSIS: zabbix_get -s host-name-or-IP [-p port-number] [-I IP-address] [-t timeout] -k item-key<br>

   EXAMPLES: 
   - zabbix_get -s 127.0.0.1 -p 10050 -k "system.cpu.load[all,avg1]"<br>
   - zabbix_get -s 127.0.0.1 -p 10050 -k "system.cpu.load[all,avg1]" --tls-connect psk --tls-psk-identity "PSK ID Zabbix agentd" --tls-psk-file /home/zabbix/zabbix_agentd.psk <br>

## **User Parameters**<br>
   **Link:** https://www.zabbix.com/documentation/6.2/en/manual/config/items/userparameters<br>

   Às vezes você pode querer executar uma verificação de agente que não vem pré-definida com o Zabbix. É aqui que os parâmetros do usuário vêm para ajudar.Você pode escrever um comando que recupere os dados necessários e inclua-os no parâmetro do usuário no arquivo de configuração do agente (parâmetro de configuração 'UserParameter').<br>
   Um parâmetro de usuário tem a seguinte sintaxe:<br>

   UserParameter=<key>,<command><br>

   Como você pode ver, um parâmetro de usuário também contém uma chave. A chave será necessária ao configurar um item. Insira uma chave de sua escolha que seja fácil de consultar (deve ser exclusiva em um host).<br>
   Reinicie o agente ou use a opção de controle de tempo de execução do agente para selecionar o novo parâmetro, por exemplo. g.:<br>

   zabbix_agentd -R userparameter_reload<br>

   Em seguida, ao configurar um item, insira a chave para referenciar o comando do parâmetro do usuário que deseja executar.
   Os parâmetros do usuário são comandos executados pelo agente Zabbix. Até 512 KB de dados podem ser retornados antes das etapas de pré-processamento do item. Observe, no entanto, que o valor de texto que pode ser eventualmente armazenado no banco de dados é limitado a 64 KB no MySQL (veja informações sobre outros bancos de dados na tabela).<br>

   /bin/sh é usado como um interpretador de linha de comando em sistemas operacionais UNIX. Os parâmetros do usuário obedecem ao tempo limite de verificação do agente; se o tempo limite for atingido, o processo de parâmetro do usuário bifurcado será encerrado.<br>

   Veja também:<br>

   Tutorial passo a passo sobre como usar os parâmetros do usuário<br>
   Execução do comando<br>
   Exemplos de parâmetros de usuário simples<br>
   Um comando simples:<br>

   UserParameter=ping,echo 1<br>

   O agente sempre retornará '1' para um item com a chave 'ping'.<br>
   Um exemplo mais complexo:<br>

   UserParameter=mysql.ping,mysqladmin -uroot ping | grep -c alive<br>

   O agente retornará '1', se o servidor MySQL estiver ativo, '0' - caso contrário.<br>







