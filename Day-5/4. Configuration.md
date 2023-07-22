# **Configuration export/import**
  **Link:** https://www.zabbix.com/documentation/6.0/en/manual/xml_export_import

   A funcionalidade de exportação/importação do Zabbix possibilita a troca de várias entidades de configuração entre um sistema Zabbix e outro. Casos de uso típicos para esta funcionalidade:<br>
   - Compartilhar templates ou mapas de rede - os usuários do Zabbix podem compartilhar seus parâmetros de configuração<br>
   - Compartilhe cenários da web em share.zabbix.com - exporte um modelo com os cenários da web e faça o upload para share.zabbix.com. Em seguida, outros podem baixar o modelo e importar o arquivo para o Zabbix.<br>
   - Integração com ferramentas de terceiros - formatos universais YAML, XML e JSON possibilitam a integração e importação/exportação de dados com ferramentas e aplicativos de terceiros<br>

   **O que pode ser exportado/importado**<br>

   Os objetos que podem ser exportados/importados são:<br>
   - Host groups<br>
   - template groups<br>
   - templates<br>
   - hosts<br>
   - network maps<br>
   - media types<br>
   - images<br>

   **Export format**<br>

    Os dados podem ser exportados usando o frontend web do Zabbix ou a API do Zabbix. Os formatos de exportação suportados são YAML, XML e JSON.<br>

    **Detalhes sobre a exportação**<br>
 
    - Todos os elementos suportados são exportados em um arquivo<br>
    - As entidades de host e modelo (itens, acionadores, gráficos, regras de descoberta) que são herdadas de modelos vinculados não são exportadas. Quaisquer alterações feitas nessas entidades em um nível de host (como intervalo de item alterado, expressão regular modificada ou protótipos adicionados à regra de descoberta de baixo nível) serão perdidas durante a exportação; ao importar, todas as entidades dos modelos vinculados são recriadas como no modelo vinculado original.<br>
    - Entidades criadas pela descoberta de baixo nível e quaisquer entidades que dependam delas não são exportadas. Por exemplo, um gatilho criado para um item gerado pela regra LLD não será exportado.<br>

    **Detalhes sobre a importação**<br>

    - A importação para no primeiro erro<br>
    - Ao atualizar imagens existentes durante a importação de imagens, o campo "imagetype" é ignorado, ou seja, é impossível alterar o tipo de imagem via importação. <br>
    - Ao importar hosts/modelos usando a opção "Excluir ausentes", as macros de host/modelo não presentes no arquivo de importação também serão excluídas.<br>
    - Tags vazias para itens, gatilhos, gráficos, aplicativos de host/modelo, discoveryRules, itemPrototypes, triggerPrototypes, graphPrototypes não têm sentido, ou seja, é o mesmo que se estivesse faltando. Outras tags, por exemplo, aplicativos de item, são significativas, ou seja, tag vazia significa que não há aplicativos para o item, tag ausente significa não atualizar aplicativos.<br>
    - A importação é compatível com YAML, XML e JSON, o arquivo de importação deve ter uma extensão de arquivo correta: .yaml e .yml para YAML, .xml para XML e .json para JSON.<br>
    - Consulte as informações de compatibilidade sobre as versões XML com suporte.<br>
