# **Real-time export**<br>
  *Link:* https://www.zabbix.com/documentation/6.0/en/manual/appendix/install/real_time_export?hl=Real%2Ctime%2Cexport%2Cdata<br>

## **Visão geral**<br>
   É possível configurarreal-Tempo exportarde eventos de gatilho, valores de itens e tendências em um formato JSON delimitado por nova linha.<br>
   Exportaring é feito em arquivos, onde cada linha doexportararquivo é um objeto JSON. Os mapeamentos de valor não são aplicados.<br>
   Em caso de erros (dadosnão pode ser escrito noexportararquivo ou oexportararquivo não pode ser renomeado ou um novo não pode ser criado após renomeá-lo), odadositem é descartado e nunca gravado noexportarArquivo. Está escrito apenas no Zabbixdadosbase. Escritadadospara oexportararquivo é retomado quando o problema de gravação é resolvido.<br>
   Para obter detalhes precisos sobre quais informações sãoexportared, veja oexportarpágina de protocolo .<br>
   Observe que host/item não pode ter metadados(grupos de hosts, nome do host, nome do item) se o host/item foi removido após odadosfoi recebido, mas antes do servidorexportareddados.<br>
   *Link:*https://www.zabbix.com/documentation/6.0/en/manual/appendix/protocols/real_time_export<br>


