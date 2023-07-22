## **Triggers**<br>
  **Link:** https://www.zabbix.com/documentation/6.2/en/manual/config/triggers<br>

  Triggers são expressões lógicas que "avaliam" os dados coletados por itens e representam o estado atual do sistema.<br>

  Embora os itens sejam usados ​​para coletar dados do sistema, é altamente impraticável seguir esses dados o tempo todo aguardando uma condição que seja alarmante ou que mereça atenção. O trabalho de "avaliar" os dados pode ser deixado para acionar expressões.<br>

  As expressões de gatilho permitem definir um limite de qual estado de dados é "aceitável". Portanto, caso os dados recebidos ultrapassem o estado aceitável, um gatilho é "disparado" - ou altera seu estado para PROBLEMA.<br>

## **Trigger dependencies**<br>
   **Link:** https://www.zabbix.com/documentation/6.2/en/manual/config/triggers/dependencies<br>

   Às vezes, a disponibilidade de um host depende de outro. Um servidor que está atrás de algum roteador ficará inacessível se o roteador cair. Com gatilhos configurados para ambos, você pode receber notificações sobre dois hosts inativos - enquanto apenas o roteador era o culpado. É aqui que alguma dependência entre hosts pode ser útil. Com o conjunto de dependências, as notificações dos dependentes poderiam ser retidas e apenas a notificação do problema raiz enviada.<br>

   Embora o Zabbix não suporte dependências entre hosts diretamente, elas podem ser definidas com outro método mais flexível - dependências de gatilho. Um gatilho pode ter um ou mais gatilhos dos quais depende.Então, em nosso exemplo simples, abrimos o formulário de configuração do gatilho do servidor e definimos que ele depende do respectivo gatilho do roteador. Com tal dependência, o gatilho do servidor não mudará de estado enquanto o gatilho do qual ele depende estiver no estado 'PROBLEM' - e, portanto, nenhuma ação dependente será executada e nenhuma notificação será enviada.<br>

   Se o servidor e o roteador estiverem inativos e houver dependência, o Zabbix não executará ações para o gatilho dependente.<br>

   As ações em gatilhos dependentes não serão executadas se o gatilho do qual dependem:<br>

   - hanges its state from 'PROBLEM' to 'UNKNOWN'<br>
   - is closed manually, by correlation or with the help of time- based functions<br>
   - is resolved by a value of an item not involved in dependent trigger<br>
   - is disabled, has disabled item or disabled item host <br>

    Observe que o gatilho "secundário" (dependente) nos casos mencionados acima não será atualizado imediatamente. Enquanto o gatilho pai estiver no estado PROBLEMA, seus dependentes podem relatar valores nos quais não podemos confiar. Assim, o gatilho dependente só será reavaliado e mudará seu estado, somente depois que o gatilho pai estiver no estado OK e recebermos métricas confiáveis.<br>

    Também:<br>

    Trigger dependency may be added from any host trigger to any other host trigger, as long as it wouldn't result in a circular dependency.<br>

    Trigger dependency may be added from a template to a template. If a trigger from template A depends on a trigger from template B, template A may only be linked to a host (or another template) together with template B, but template B may be linked to a host (or another template) alone.<br>

    Trigger dependency may be added from template trigger to a host trigger. In this case, linking such a template to a host will create a host trigger that depends on the same trigger template trigger was depending on. This allows to, for example, have a template where some triggers depend on router (host) triggers. All hosts linked to this template will depend on that specific router.<br>

    Trigger dependency from a host trigger to a template trigger may not be added.<br>

    Trigger dependency may be added from a trigger prototype to another trigger prototype (within the same low-level discovery rule) or a real trigger. A trigger prototype may not depend on a trigger prototype from a different LLD rule or on a trigger created from trigger prototype. Host trigger prototype cannot depend on a trigger from a template.<br>

    A configuração está na documentação, sendo assim sempre abra o link e veja a documentação.<br>

## **Operational data**<br>
   **Link:** https://www.zabbix.com/documentation/6.2/en/manual/web_interface/frontend_sections/configuration/hosts/triggers?hl=Operational%2Cdata<br>
    
   Definição de dados operacionais do gatilho, contendo strings e macros arbitrárias que serão resolvidas dinamicamente em Monitoramento → Problemas.<br>

## **Trigger expression**<br>
   **Link:** https://www.zabbix.com/documentation/6.2/en/manual/config/triggers/expression<br>

   As expressões usadas nos gatilhos são muito flexíveis. Você pode usá-los para criar testes lógicos complexos sobre estatísticas monitoradas.Uma expressão simples usa uma função que é aplicada ao item com alguns parâmetros. A função retorna um resultado que é comparado ao limite, usando um operador e uma constante.<br>
   
   A sintaxe de uma expressão útil simples é function(/host/key,parameter)<operator><constant>.<br>

   Por exemplo:<br>

   min(/Zabbix server/net.if.in[eth0,bytes],5m)>100K<br>

   será acionado se o número de bytes recebidos durante os últimos cinco minutos foi sempre superior a 100 kilobytes.<br>

   Embora a sintaxe seja exatamente a mesma, do ponto de vista funcional existem dois tipos de expressões de gatilho:<br>

   expressão do problema - define as condições do problema<br>
   expressão de recuperação (opcional) - define condições adicionais da resolução do problema<br>
   Ao definir uma expressão de problema sozinha, essa expressão será usada como o limite do problema e o limite de recuperação do problema. Assim que a expressão do problema for avaliada como TRUE, há um problema. Assim que a expressão do problema for avaliada como FALSE, o problema será resolvido.<br>

   Ao definir a expressão do problema e a expressão de recuperação suplementar, a resolução do problema se torna mais complexa: não apenas a expressão do problema deve ser FALSE, mas também a expressão de recuperação deve ser TRUE. Isso é útil para criar histerese e evitar a oscilação do gatilho.<br>

   **Functions**
   As funções permitem calcular os valores coletados (média, mínimo, máximo, soma), encontrar strings, tempo atual de referência e outros fatores. Uma lista completa de funções suportadas está disponível. <br>

   Normalmente, as funções retornam valores numéricos para comparação. Ao retornar strings, a comparação é possível com os operadores = e <>.<br>

   Na documentação possui exemplos e o restante da leitura das functions.<br>

## **Recovery expression**
     
   Expressão lógica (opcional) definindo condições adicionais que devem ser atendidas antes que o problema seja resolvido, após a expressão do problema original já ter sido avaliada como FALSE.<br>

   Expressão de recuperação é útil para histerese de disparo. Não é possível resolver um problema apenas pela expressão de recuperação se a expressão do problema ainda for TRUE.<br>

   Este campo só está disponível se 'Expressão de recuperação' for selecionada para geração de evento OK.<br>

## **Dynamic problem names**<br>
   **Link:** https://www.zabbix.com/documentation/6.2/en/manual/config/items/itemtypes/snmp/dynamicindex?hl=Dynamic%2Cdynamic%2Citem<br>

   Embora você possa encontrar o número de índice necessário (por exemplo, de uma interface de rede) entre os OIDs SNMP, às vezes você pode não confiar completamente no número de índice que permanece sempre o mesmo.<br>

   Os números de índice podem ser dinâmicos - eles podem mudar com o tempo e seu item pode parar de funcionar como consequência.<br>

   Para evitar este cenário, é possível definir um OID que leve em consideração a possibilidade de alteração de um número de índice.<br>

   Por exemplo, se você precisar recuperar o valor de índice para anexar a ifInOctets que corresponde à interface GigabitEthernet0/1 em um dispositivo Cisco, use o seguinte OID:<br>

   ifInOctets["index","ifDescr","GigabitEthernet0/1"]<br>

   Uma sintaxe especial para OID é usada:<br>

   <OID of data>["index","<base OID of index>","<string to search for>"]<br>

   Parameter e Description<br>
   OID of data: OID principal a ser usado para recuperação de dados no item.<br>
   Index: Método de processamento. Atualmente, um método é suportado: index – procure por índice e anexe-o ao OID de dados<br>
   Base OID of index: Este OID será procurado para obter o valor do índice correspondente à string.<br>
   String to search for: A string a ser usada para uma correspondência exata com um valor ao fazer uma pesquisa. Maiúsculas e minúsculas.<br>

## **Closing and acknowledging problems**<br>
**Link:** https://www.zabbix.com/documentation/6.2/en/manual/acknowledgment?hl=problems%2CDashboard%2CProblems<br>

   Eventos de problemas no Zabbix podem ser reconhecidos pelos usuários.<br>

   Se um usuário for notificado sobre um evento de problema, ele poderá acessar o frontend do Zabbix, abrir a janela pop-up de atualização do problema usando uma das formas listadas abaixo e reconhecer o problema. Ao reconhecer, eles podem inserir seu comentário para isso, dizendo que estão trabalhando nisso ou qualquer outra coisa que tenham vontade de dizer sobre isso.<br>

   Dessa forma, se outro usuário do sistema detectar o mesmo problema, ele verá imediatamente se ele foi reconhecido e os comentários até o momento.<br>

   Dessa forma, o fluxo de trabalho de resolução de problemas com mais de um usuário do sistema pode ocorrer de forma coordenada.<br>

   O status de confirmação também é usado ao definir operações de ação. Você pode definir, por exemplo, que uma notificação seja enviada a um gerente de nível superior somente se um evento não for reconhecido por algum tempo.<br>

   Para reconhecer eventos e comentar sobre eles, um usuário deve ter pelo menos permissões de leitura para os gatilhos correspondentes. Para alterar a gravidade do problema ou fechar o problema, um usuário deve ter permissões de leitura e gravação para os gatilhos correspondentes.<br>

  - Existem várias maneiras de acessar a janela pop-up de atualização do problema, que permite reconhecer um problema.<br>

  - Você pode selecionar problemas em Monitoramento → Problemas e clicar em Atualização em massa abaixo da lista<br>

  - Você pode clicar na coluna Ack mostrando o status de confirmação de problemas em:<br>

  - Monitoramento → Painel (Problemas e Problemas por widgets de gravidade)<br>

  - Monitoramento → Problemas<br>

  - Monitoramento → Problemas → Detalhes do evento<br>

    A coluna Ack contém um link 'Sim' ou 'Não', indicando um problema reconhecido ou não reconhecido, respectivamente. Clicar nos links levará você à janela pop-up de atualização do problema.<br>

   - Você pode clicar em uma célula de problema não resolvido em:<br>
   - Monitoramento → Painel (widget de visão geral do acionador)<br>

    O menu pop-up contém uma opção Reconhecer que o levará à janela de atualização do problema.<br>
     
    **Close Problem**<br>
    Marque a caixa de seleção para fechar manualmente o(s) problema(s) selecionado(s).<br>
    A caixa de seleção para fechar um problema estará disponível se a opção Permitir fechamento manual estiver marcada na configuração do acionador para pelo menos um dos problemas selecionados. Serão fechados apenas os problemas que podem ser fechados ao clicar em Atualizar.<br>
    Se nenhum problema puder ser fechado manualmente, a caixa de seleção será desativada.<br>
    Problemas já fechados não serão fechados repetidamente.<br>


## **Display**<br>
   **Link:** https://www.zabbix.com/documentation/6.2/en/manual/acknowledgment?hl=problems%2CDashboard%2CProblems#display<br>

   Com base nas informações de confirmação, é possível configurar como a contagem de problemas é exibida no painel ou nos mapas. Para fazer isso, você deve fazer seleções na opção de exibição do problema, disponível na configuração do mapa e no widget do painel Problemas por gravidade. É possível exibir todas as contagens de problemas, contagens de problemas não confirmados como separadas da contagem total ou apenas de problemas não confirmados.<br>

   Com base nas informações de atualização do problema (reconhecimento, etc.), é possível configurar as operações de atualização - enviar uma mensagem ou executar comandos remotos.<br>

## **Date and time functions**
   **Link:** https://www.zabbix.com/documentation/6.2/en/manual/appendix/functions/time?hl=Date%2Cand%2Ctime%2Cfunctions

   Todas as funções listadas aqui são suportadas em:<br>
     Link Trigger expressions: https://www.zabbix.com/documentation/6.2/en/manual/config/triggers/expression<br>
     Link Calculated items: https://www.zabbix.com/documentation/6.2/en/manual/config/items/itemtypes/calculated<br>

   **Atenção:** As funções de data e hora não podem ser usadas apenas na expressão; pelo menos uma função não baseada em tempo referenciando o item de host deve estar presente na expressão.<br>

   Na documentação possui uma tabela que é importante você analisar.<br>

