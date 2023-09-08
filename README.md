# db-otus

## Взаимодействие операторов связи

### Схема данных

**БД состоит из ряда свзяанных таблиц:** 

*operators_code* - Информация о занятых def оператором \
*country* - Информация о кодах стран \
*operators* - Информация у идентификаторе, имени и инн оператора \
*numbers* - Информация о номерах абонентов \
*operation_call* - информация о звонках абонента \
*operation_sms* - информация о смс абонента \
*operation_site* - информация о потраченном трафике абонентом \
*wallet* - информация о текущем состоянии счёта абонента \
*price* - стоимость услуг \
*operation* - сводная информация о абоненте (без агрегации) 

**Схемы**

*operators_code* - Информация о занятых def оператором \
id smallint \
city text 

*country* - Информация о кодах стран \
code smallint \
country text 

*operators* - Информация у идентификаторе, имени и инн оператора \
opr_name text \
country_code smallint \
inn long UNQUE 

*numbers* - Информация о номерах абонентов \
number bigint PRIMARY KEY (индекс создаётся автоматически, нужен для быстрого получения инфы по номеру) \
country_name text \
opr_name text \
date_start timestamp \
date_end timestamp индексированное поле, нужно для получения из таблицы только акутальные номера. Должен быть больше date_start

*operation_call* - информация о звонках абонента \
number bigint PRIMARY KEY (индекс создаётся автоматически, нужен для быстрого получения инфы по номеру) \
number_b bigint \
traffic smallint больше 0

*operation_sms* - информация о смс абонента \
number bigint PRIMARY KEY (индекс создаётся автоматически, нужен для быстрого получения инфы по номеру) \
number_b bigint \
sms text Не пустой

*operation_site* - информация о потраченном трафике абонентом \
number bigint PRIMARY KEY (индекс создаётся автоматически, нужен для быстрого получения инфы по номеру) \
site text \
traffic real Больше 0

*wallet* - информация о текущем состоянии счёта абонента \
number bigint PRIMARY KEY (индекс создаётся автоматически, нужен для быстрого получения инфы по номеру) \
wallet numeric(10,3) больше -100

*price* - стоимость услуг 
call_price numeric(10,3) \
sms_price numeric(10,3) \
traffic_price numeric(10,3) \

*operation* - сводная информация о абоненте (без агрегации) \
number bigint PRIMARY KEY (индекс создаётся автоматически, нужен для быстрого получения инфы по номеру) \
operation char(5) индексированное поле для быстрого получения операций определённого типа \
operator_number text индексированное поле для быстрого получения операций определённого оператора \
country_number text индексированное поле для быстрого получения операций определённой страны \
city_number text индексированное поле для быстрого получения операций определённого города \
site text
sms_text text
number_b bigint
operator_number_1 text
country_number_b text
city_number_b text
traffic_mb real
traffic_sec smallint


### Решаемые задачи

Точное и своевременное определение потребляемых абонентом услуг - международные и внутренние вызовы, смс, траффик. Тарификация и отслеживание счёта абонента

[Диаграмма](https://app.sqldbm.com/PostgreSQL/Diagrams/p272769)

![image](https://github.com/SacredDiablo/db-otus/assets/56549314/7f662039-01e1-4472-b089-535c4b30844c)
