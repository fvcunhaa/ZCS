## **Custom intervals**<br>
**Link:** https://www.zabbix.com/documentation/6.2/en/manual/config/items/item/custom_intervals?hl=interval%2Cupdate#scheduling-intervals
   Overview: É possível criar regras personalizadas em relação aos horários em que um item é verificado. Os dois métodos para isso são Intervalos Flexíveis, que permitem redefinir o intervalo de atualização padrão, e Agendamento, pelo qual uma verificação de item pode ser executada em um horário específico ou sequência de horários.<br>

## **Flexible intervals**<br>

   Intervalos flexíveis permitem redefinir o intervalo de atualização padrão para períodos de tempo específicos. Um intervalo flexível é definido com Intervalo e Período onde:<br>
   Intervalo – o intervalo de atualização para o período de tempo especificado<br>
   Período – o período de tempo em que o intervalo flexível está ativo (consulte os períodos de tempo para obter uma descrição detalhada do formato do período)<br>
   Até sete intervalos flexíveis podem ser definidos. Se vários intervalos flexíveis se sobrepuserem, o menor valor de intervalo será usado para o período de sobreposição. Observe que se o menor valor de intervalos flexíveis sobrepostos for '0', nenhuma sondagem ocorrerá. Fora dos intervalos flexíveis, o intervalo de atualização padrão é usado.<br>

   Observe que se o intervalo flexível for igual à duração do período, o item será verificado exatamente uma vez. Se o intervalo flexível for maior que o período, o item pode ser verificado uma vez ou pode não ser verificado (portanto, essa configuração não é aconselhável). Se o intervalo flexível for menor que o período, o item será verificado pelo menos uma vez.<br>

   Se o intervalo flexível for definido como '0', o item não será pesquisado durante o período de intervalo flexível e retomará a pesquisa de acordo com o intervalo de atualização padrão assim que o período terminar. Exemplos:<br>

   *Interval: 10 Period: 1-5,09:00-18:00	Descrição: O item será verificado a cada 10 segundos durante o horário de trabalho.*<br>
   Outros exemplos na documentação no link acima.<br>

## **Scheduling intervals**

   Os intervalos de agendamento são usados ​​para verificar itens em horários específicos. Enquanto os intervalos flexíveis são projetados para redefinir o intervalo de atualização de item padrão, os intervalos de agendamento são usados ​​para especificar um agendamento de verificação independente, que é executado em paralelo.<br>

   Um intervalo de agendamento é definido como: md<filter>wd<filter>h<filter>m<filter>s<filter> onde:<br>

   md - dias do mês<br>
   wd - dias da semana<br>
   h - horas<br>
   m - minutos<br>
   s – segundos<br>

   <filter> é usado para especificar valores para seu prefixo (dias, horas, minutos, segundos) e é definido como: [<from>[-<to>]][/<step>][,<filter>] onde:<br>

   <from> e <to> definem o intervalo de valores correspondentes (incluídos). Se <to> for omitido, o filtro corresponderá a um intervalo <from> - <from>. Se <from> também for omitido, o filtro corresponderá a todos os valores possíveis.<br>
   <step> define os saltos do valor numérico pelo intervalo. Por padrão, <step> tem o valor 1, o que significa que todos os valores do intervalo definido são correspondidos.<br>
   Embora as definições de filtro sejam opcionais, pelo menos um filtro deve ser usado. Um filtro deve ter um intervalo ou o valor <step> definido.<br>

   Um filtro vazio corresponde a '0' se nenhum filtro de nível inferior for definido ou a todos os valores possíveis caso contrário. Por exemplo, se o filtro de hora for omitido, apenas a hora '0' corresponderá, desde que os filtros de minutos e segundos também sejam omitidos, caso contrário, um filtro de hora vazio corresponderá a todos os valores de hora.<br>

   Os valores <from> e <to> válidos para seus respectivos prefixos de filtro são:<br>

   Prefix: md Descrição: Dias do mês <from>:1-31 <to>1-31<br>
   Demais exemplos na documentação<br>

   O valor <from> deve ser menor ou igual ao valor <to>. O valor <step> deve ser maior ou igual a 1 e menor ou igual a <to> - <from>.<br>

   Os valores de dias, horas, minutos e segundos do mês de um dígito podem ser prefixados com 0. Por exemplo, md01-31 e h/02 são intervalos válidos, mas md01-031 e wd01-07 não são.<br>

   No frontend do Zabbix, vários intervalos de agendamento são inseridos em linhas separadas. Na API do Zabbix, eles são concatenados em uma única string com ponto e vírgula; como separador.<br>

   Se um tempo corresponder a vários intervalos, ele será executado apenas uma vez. Por exemplo, wd1h9;h9 será executado apenas uma vez na segunda-feira às 9h.<br>

   Exemplos:<br>
   Interval: m0-59   Will be Executed: todo minuto<br>
   Demais exemplos na documentação no link acima.<br>

   



