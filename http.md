# НТТР 
НТТР (HyperText Transfer Protocol) — протокол передачи данных на прикладном уровне [модели OSI](https://ru.wikipedia.org/wiki/%D0%A1%D0%B5%D1%82%D0%B5%D0%B2%D0%B0%D1%8F_%D0%BC%D0%BE%D0%B4%D0%B5%D0%BB%D1%8C_OSI), который обеспечивает обмен данными между пользовательским приложением (веб-браузером) и веб-сервером. 
## Особенности протокола НТТР
- **Обмен данными** происходит по схеме «вопрос-ответ»: клиентское приложение формирует запрос и отправляет его на сервер, где серверное программное обеспечение обрабатывает этот запрос, формирует ответ и отправляет его обратно клиенту.
- **Идентификация ресурса** определяется при помощи URI (Uniform Resource Identifier) — последовательности символов, определяющей адрес сетевого ресурса, которую указывает клиент при запросе.
- **Сохранение состояния**. Протокол НТТР осуществляет только передачу, но не сохранение состояния клиентского соединения. Это означает, что обработка каждого HTTP-запроса происходит в полной изоляции от других, без учета запросов, обработанных ранее.
- **Области применения**. HTTP часто используется в качестве транспорта для передачи информации вышележащих протоколов прикладного уровня, таких как [SOAP](https://ru.wikipedia.org/wiki/SOAP), [XML-RPC](https://ru.wikipedia.org/wiki/XML-RPC) и [WebDAV](https://ru.wikipedia.org/wiki/WebDAV).
## Аутентификация протокола НТТР
- **Базовая аутентификация («basic access authentication»)** — имя пользователя и пароль включаются напрямую в текстовую строку веб-запроса.
- **Дайджест-аутентификация («digest access authentication»)** или «аутентификация по контрольной сумме» — в этом случае пароль пользователя передается в хешированном виде.
## Хронология развития протокола НТТР
- **[НТТР/0.9](https://www.w3.org/Protocols/HTTP/AsImplemented.html)** — стандарт от 1991 года;
- **[НТТР/1.0](https://www.w3.org/Protocols/HTTP/1.0/spec.html)** — стандарт от 1996 года;
- **[НТТР/1.1](https://tools.ietf.org/html/rfc2616)** — стандарт от 1999 года;
- **[НТТР/2](https://tools.ietf.org/html/rfc7540)** — стандарт от 2015 года;  

В двух первых версиях протокола TCP-соединение разрывалось после каждой пары «вопрос-ответ».  
В версии НТТР/1.1 было предусмотрено «постоянное соединение»: клиент мог посылать сразу несколько HTTP-запросов в пределах одного  TCP-соединения.   
Основными нововведениями НТТР/2 стали бинарность, расстановка приоритетов для запросов, сжатие заголовков, загрузка нескольких элементов параллельно.
## Программное обеспечение протокола НТТР
- **Серверы** — поставщики услуг хранения и предоставления информации;
- **Клиенты** — конечные потребители;
- **Прокси** — программы-посредники, осуществляющие перенаправление HTTP-запросов.
## Структура протокола HTTP
| *Запрос клиента*       | *Ответ сервера*               | 
|:------------- |:------------------| 
| 1. Стартовая строка     | 1. Версия, Код Состояния, Пояснение    | 
| 2. Заголовок    | 2. Заголовок | 
| 3. Пустая строка   | 3. Пустая строка          |
| 4. Тело сообщения (опционально)  | 4. Тело сообщения (опционально)          |
## Элементы структуры протокола НТТР
### Стартовая строка («Starting line»)
Определяет тип сообщения, различный для запроса клиента и ответа сервера.   

Пример строки *запроса клиента*: **Метод URI НТТР/Версия**  
Где **Метод** — тип запроса, указывает на тип операции. Обычно представляет из себя одно слово, написанное заглавными буквами. В НТТР/1.0 были определены три метода: GET, POST и HEAD. В НТТР/1.1 были добавлены еще пять: OPINIONS, PUT, DELETE, TRACE и CONNECT;  
**URI** — последовательность символов, идентифицирующая абстрактный или физический ресурс;  
**Версия** (версия протокола) — пара разделенных точкой цифр, например «1.1».  

Пример строки *ответа сервера*: **НТТР/Версия Код_Состояния Пояснение**  
Где **Версия** — пара разделенных точкой цифр, как и в запросе клиента;  
**Код Состояния** — три цифры, определяющие дальнейшее содержимое сообщения и поведение клиента. Коды состояния делятся на пять основных групп: «Информационный» 1XX, «Успех» 2XX, «Перенаправление» 3XX, «Ошибка клиента» 4XX и «Ошибка сервера» 5XX;  
**Пояснение** — текстовое короткое пояснение к коду ответа для пользователя.
### Заголовки («Headers»)
Строки, содержащие разделенную двоеточием пару имя-значение. Они могут содержать описание данных и служебную информацию, необходимую для взаимодействия между клиентом и сервером.  

Заголовок имеет следующий вид: **name: value**  
Где **name** — название параметра, состоит минимум из одного печатного символа;  
**value** — значение параметра.
#### Четыре основные группы заголовков:
- **General Headers** («Заголовки основного типа») — могут быть включены в любое сообщение клиента и сервера;
- **Request Headers** («Заголовки запроса») — используются только в запросах клиента;
- **Response Headers** («Заголовки ответа») — только для ответов от сервера;
- **Entity Headers** («Заголовки сущности») — сопровождают каждую сущность сообщения (полезную информацию, передаваемую в запросе или ответе).
### Тело сообщения («Message Body»)
Текстовые или бинарные данные сообщения.
## Основные механизмы протокола НТТР
- **Частичные GET-запросы** («partial GET») — позволяют запросить указанный фрагмент ресурса;
- **Условные GET-запросы** («conditional GET») — позволяет проверить изменяемость запрошенной информации с определенного момента времени и передать тело запрашиваемого ресурса только в случае его изменения;
- **Согласование содержимого** («Content Negotiation») — механизм автоматического определения необходимого ресурса при наличии нескольких разнотипных версий документа. Подразделяется на два типа:
        - **Управляемое сервером**: при наличии нескольких версий ресурса сервер может анализировать заголовки запроса клиента, чтобы выдать, по его мнению, наиболее подходящую;
        - **Управляемое клиентом**: тип содержимого определяется только на стороне клиента;
- **Множественное содержимое** («Multiple Content») — возможность передачи нескольких сущностей в пределах одного сообщения.
## Список использованных источников
Википедия: [https://ru.wikipedia.org/wiki/HTTP](https://ru.wikipedia.org/wiki/HTTP); [https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)  
Хабрахаб: [https://habrahabr.ru/post/215117/](https://habrahabr.ru/post/215117/)  
RFC: 2068: [https://rfc2.ru/2068.rfc; https://tools.ietf.org/html/rfc2616](https://rfc2.ru/2068.rfc; https://tools.ietf.org/html/rfc2616)
