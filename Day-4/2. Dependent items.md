## **Dependent Items**<br>
   **Link:** https://www.zabbix.com/documentation/6.2/en/manual/config/items/itemtypes/dependent_items?hl=Dependent%2Citem%2Cdependent<br>

   Visão Geral: Existem situações em que um item reúne várias métricas ao mesmo tempo ou até faz mais sentido coletar as métricas relacionadas simultaneamente, por exemplo:<br>

   - Utilização da CPU de núcleos individuais<br>
   - Tráfego de rede de entrada/saída/total<br>

    Para permitir a coleta de métricas em massa e o uso simultâneo em vários itens relacionados, o Zabbix suporta itens dependentes. Os itens dependentes dependem do item mestre que coleta seus dados simultaneamente, em uma consulta. Um novo valor para o item mestre preenche automaticamente os valores dos itens dependentes. Os itens dependentes não podem ter um intervalo de atualização diferente do item mestre.<br>

    As opções de pré-processamento do Zabbix podem ser usadas para extrair a parte necessária para o item dependente dos dados do item mestre.<br>

    O pré-processamento é gerenciado por um processo gerenciador de pré-processamento, que foi adicionado no Zabbix 3.4, juntamente com os trabalhadores que executam as etapas de pré-processamento. Todos os valores (com ou sem pré-processamento) de diferentes coletores de dados passam pelo gerenciador de pré-processamento antes de serem incluídos no cache de histórico. A comunicação IPC baseada em soquete é usada entre os coletores de dados (pollers, trappers, etc.) e o processo de pré-processamento.<br>

    O servidor Zabbix ou o proxy Zabbix (se o host for monitorado por proxy) estão realizando etapas de pré-processamento e processando itens dependentes.<br>

    O item de qualquer tipo, mesmo o item dependente, pode ser definido como item mestre. Níveis adicionais de itens dependentes podem ser usados ​​para extrair partes menores do valor de um item dependente existente.<br>

    **Limitações**<br>

    - Only same host (template) dependencies are allowed<br>
    - An item prototype can depend on another item prototype or regular item from the same host<br>
    - Maximum count of dependent items for one master item is limited to 29999 (regardless of the number of dependency levels)<br>
    - Maximum 3 dependency levels allowed<br>
    - Dependent item on a host with master item from template will not be exported to XML<br>

    A documentação sobre item dependente tem todos os topícos e possui muitas imagem devido isso, lembre de abrir a documentação e ver todas as imagens.<br>



