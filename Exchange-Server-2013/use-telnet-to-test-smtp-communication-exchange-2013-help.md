﻿---
title: 'Тестирование связи по протоколу SMTP с помощью Telnet: Exchange 2013 Help'
TOCTitle: Тестирование связи по протоколу SMTP с помощью Telnet
ms:assetid: 8a5f6715-baa4-48dd-8600-02c6b3d1aa9d
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb123686(v=EXCHG.150)
ms:contentKeyID: 52061268
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Тестирование связи по протоколу SMTP с помощью Telnet

 

_**Применимо к:**Exchange Server 2013_

_**Последнее изменение раздела:**2016-12-09_

В этом разделе объясняется, как использовать Telnet для проверки связи по протоколу SMTP (Simple Mail Transfer Protocol) между серверами обмена сообщениями. По умолчанию протокол SMTP осуществляет прослушивает на порту 25. При использовании Telnet на порту 25 можно ввести команды SMTP, используемые для подключения к SMTP-серверу и отправить сообщение так, как будто сеанс Telnet является SMTP-сервером обмена сообщениями. При этом можно видеть успешный или неудачный результат каждого действия в процессе подключения и отправки сообщения.

Ниже представлены сценарии, в которых Telnet используется для проверки связи по протоколу SMTP с имеющимися в организации Microsoft Exchange транспортными серверами.

  - Подключение к вашему серверу Exchange с выходом в Интернет с узла, расположенного за пределами сети периметра, и отправка тестового сообщения.

  - Подключение к удаленному серверу обмена сообщениями с вашего сервера Exchange с выходом в Интернет и отправка тестового сообщения.

Процедура, приведенная в данном разделе, показывает, как использовать клиент Telnet, являющийся компонентом Microsoft Windows. Для клиентов Telnet сторонних разработчиков может требоваться синтаксис, отличный от синтаксиса компонента Telnet Windows.

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: 30 минут.

  - Разрешения Exchange не применяются к процедурам, описанным в этом разделе. Эти процедуры выполняются в операционной системе сервера Exchange или клиентского компьютера.

  - Процедуры, описанные в этом разделе, лучше всего использовать для подключения к серверам с доступом в Интернет, которые поддерживают анонимные подключения. Обмен сообщениями между внутренними серверами Exchange шифруется и проходит проверку подлинности. Чтобы использовать Telnet для подключения к службе транспортного сервера-концентратора на сервере почтовых ящиков, нужно создать соединитель получения, настроенный на поддержку анонимного доступа или обычную проверку подлинности для получения сообщений. Если соединитель поддерживает обычную проверку подлинности, необходима служебная программа для преобразования текстовых строк, используемых для имени пользователя и пароля, в формат Base64. Поскольку имя пользователя и пароль при использовании обычной проверки подлинности легко перехватываются, обычную проверку подлинности не рекомендуется использовать без шифрования.

  - Если вы подключаетесь к удаленному серверу обмена сообщениями, рекомендуется выполнить описанные в этом разделе процедуры на сервере Exchange с выходом в Интернет. Это позволит избежать отклонения тестового сообщения удаленными серверами обмена сообщениями, настроенными на проверку IP-адреса источника, соответствующего DNS-имени домена и IP-адреса обратного просмотра любого узла в Интернете, который пытается отправить сообщение на сервер.

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="Совет" alt="Совет" />Совет.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.</td>
</tr>
</tbody>
</table>


## Как это сделать

## Действие 1. Установка клиента Telnet в Windows.

По умолчанию клиент Telnet не установлен в большинстве клиентских и серверных версий операционных систем Microsoft Windows. Сведения о его установке см. в статье [Установка клиента Telnet](https://go.microsoft.com/fwlink/p/?linkid=179054).

## Действие 2. Поиск полного доменного имени или IP-адреса в записи MX удаленного сервера SMTP с помощью средства командной строки Nslookup.

Для подключения к конечному серверу SMTP с помощью протокола Telnet на порте 25 необходимо использовать полное доменное имя или IP-адрес сервера SMTP. Если полное доменное имя или IP-адрес неизвестны, самым простым способом получения этих сведений является использование средства командной строки Nslookup для поиска записи MX конечного домена.

1.  В командной строке введите **nslookup** и нажмите клавишу ВВОД. Эта команда открывает сеанс Nslookup.

2.  Введите **set type=mx** и нажмите клавишу ВВОД.

3.  Введите **set timeout=20** и нажмите клавишу ВВОД. По умолчанию DNS-серверы Windows отводят 15-секундный интервал для выполнения рекурсивного DNS-запроса.

4.  Введите имя домена, для которого требуется найти MX-запись. Например, чтобы найти запись MX для домена fabrikam.com, введите **fabrikam.com.** и нажмите клавишу ВВОД.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ126620.note(EXCHG.150).gif" title="Примечание" alt="Примечание" />Примечание.</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Конечная точка ( <strong>.</strong> ) означает, что используется полное доменное имя. Использование завершающей точки препятствует непреднамеренному добавлению к имени домена каких-либо DNS-суффиксов по умолчанию, настроенных для сети.</td>
    </tr>
    </tbody>
    </table>
    
    Выходные данные команды выглядят следующим образом:
    
        fabrikam.com mx preference=10, mail exchanger = mail1.fabrikam.com
        fabrikam.com mx preference=20, mail exchanger = mail2.fabrikam.com
        mail1.fabrikam.com internet address = 192.168.1.10
        mail2 fabrikam.com internet address = 192.168.1.20
    
    В качестве SMTP-сервера назначения можно использовать любые имена узлов или IP-адреса, связанные с MX-записями. Меньшее значение приоритета означает более предпочтительный SMTP-сервер. В целях балансировки нагрузки и отказоустойчивости можно использовать несколько MX-записей и различные значения приоритета.

5.  Для завершения сеанса Nslookup введите **exit** и нажмите клавишу ВВОД.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ126620.note(EXCHG.150).gif" title="Примечание" alt="Примечание" />Примечание.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Ограничения брандмауэра и прокси-сервера Интернета, установленные для внутренней сети организации, могут препятствовать использованию средства Nslookup для опроса публичных DNS-серверов в Интернете.</td>
</tr>
</tbody>
</table>


## Действие 3. Использование протокола Telnet на порте 25 для проверки связи по протоколу SMTP.

В этом примере используются следующие значения.

  - **SMTP-сервер назначения**   mail1.fabrikam.com

  - **Исходный домен**   contoso.com

  - **Адрес электронной почты отправителя**   chris@contoso.com

  - **Адрес электронной почты получателя**   kate@fabrikam.com

  - **Тема сообщения**   Test from Contoso

  - **Текст сообщения**   This is a test message

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/JJ126620.note(EXCHG.150).gif" title="Примечание" alt="Примечание" />Примечание.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Команды клиента Telnet вводятся без учета регистра. Команды SMTP набраны заглавными буквами для большей ясности.</p></li>
<li><p>После подключения к SMTP-серверу назначения в сеансе Telnet нельзя использовать клавишу BACKSPACE. Если при вводе команды SMTP допущена ошибка, следует нажать клавишу ВВОД и повторно ввести команду. Неизвестные команды SMTP или синтаксические ошибки приведут к появлению сообщения об ошибке следующего вида:</p>
<pre><code>500 5.3.3 Unrecognized command</code></pre></li>
</ul></td>
</tr>
</tbody>
</table>


1.  В командной строке введите **telnet** и нажмите клавишу ВВОД. Эта команда открывает сеанс Telnet.

2.  Введите **set localecho** и нажмите клавишу ВВОД. Эта необязательная команда позволяет видеть вводимые знаки. Этот параметр может быть необходим для некоторых SMTP-серверов.

3.  Введите **set logfile***\<имя файла\>*. Это необязательная команда включает ведение журнала сеанса Telnet в указанный файл журнала. Если указать только имя файла, местоположением файла журнала будет текущий рабочий каталог. При указании пути и имени файла путь должен быть локальным для компьютера. Путь и имя файла необходимо вводить в формате Microsoft DOS 8.3. Указанный путь должен уже существовать. Если указать файл журнала, который не существует, он будет создан.

4.  Введите **open mail1.fabrikam.com 25** и нажмите клавишу ВВОД.

5.  Введите **EHLO contoso.com** и нажмите клавишу ВВОД.

6.  Введите **MAIL FROM:chris@contoso.com** и нажмите клавишу ВВОД.

7.  Введите **RCPT TO:kate@fabrikam.com NOTIFY=success,failure** и нажмите клавишу ВВОД. Необязательная команда NOTIFY определяет конкретные уведомления о доставке, которые SMTP-сервер назначения должен предоставить отправителю. Уведомления о доставке определены в стандарте RFC 1891. В данном случае запрашивается уведомление об успешной доставке или невозможности доставки сообщения.

8.  Введите **DATA** и нажмите клавишу ВВОД. Появится отклик, подобный приведенному ниже:
    
        354 Start mail input; end with <CLRF>.<CLRF>

9.  Введите **Subject: Test from Contoso** и нажмите клавишу ВВОД.

10. Нажмите клавишу ВВОД. RFC 2822 требует, чтобы между полем заголовка `Subject:` и текстом сообщения была пустая строка.

11. Введите **This is a test message** и нажмите клавишу ВВОД.

12. Нажмите клавишу ВВОД, введите точку ( **.** ) и нажмите клавишу ВВОД. Появится отклик, подобный приведенному ниже:
    
        250 2.6.0 <GUID> Queued mail for delivery

13. Чтобы отключиться от конечного сервера SMTP, введите **QUIT** и нажмите клавишу ВВОД. Появится отклик, подобный приведенному ниже:
    
        221 2.0.0 Service closing transmission channel

14. Чтобы закрыть сеанс Telnet, введите **quit** и нажмите клавишу ВВОД.

## Действие 4. Оценка результатов сеанса Telnet.

В этом разделе приведены подробные сведения о возможных откликах на команды, введенные в предыдущем примере.

  - Open mail1.fabrikam.com 25

  - EHLO contoso.com

  - MAIL FROM:chris@contoso.com

  - RCPT TO:kate@fabrikam.com NOTIFY=success,failure
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ126620.note(EXCHG.150).gif" title="Примечание" alt="Примечание" />Примечание.</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Трехзначные коды отклика SMTP, определенные в RFC 2821, одинаковы для всех SMTP-серверов обмена сообщениями. Текстовые описания могут слегка отличаться для некоторых SMTP-серверов обмена сообщениями.</td>
    </tr>
    </tbody>
    </table>


## Open mail1.fabrikam.com 25

**Отклик об успешном выполнении**   `220 mail1.fabrikam.com Microsoft ESMTP MAIL Service ready at <day-date-time>`

**Отклик о сбое**   `Connecting to mail1.fabrikam.com...Could not open connection to the host, on port 25: Connect failed`

**Возможные причины сбоя**

  - SMTP-служба назначения недоступна.

  - На брандмауэре назначения установлены ограничения.

  - На брандмауэре источника установлены ограничения.

  - Указано неверное полное доменное имя или IP-адрес для SMTP-сервера назначения.

  - Указан неверный номер порта.

## EHLO contoso.com

**Отклик об успешном выполнении**   `250 mail1.fabrikam.com Hello [<sourceIPaddress>]`

**Отклик о сбое**   `501 5.5.4 Invalid domain name`

**Возможные причины сбоя**   В имени домена содержатся недопустимые знаки. Кроме того, на SMTP-сервере назначения установлены ограничения на подключение.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ126620.note(EXCHG.150).gif" title="Примечание" alt="Примечание" />Примечание.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>EHLO — это команда протокола ESMTP (Extended Simple Message Transfer Protocol), определенная в RFC 2821. ESMTP-серверы могут объявлять о своих возможностях в процессе начального подключения. Эти возможности включают максимально допустимый размер сообщения и поддерживаемые методы проверки подлинности. HELO — это более старая команда SMTP, определенная в RFC 821. Большинство SMTP-серверов обмена сообщениями поддерживают ESMTP и EHLO.</td>
</tr>
</tbody>
</table>


## MAIL FROM:chris@contoso.com

**Отклик об успешном выполнении**   `250 2.1.0 Sender OK`

**Отклик о сбое**   `550 5.1.7 Invalid address`

**Возможные причины сбоя**   Синтаксическая ошибка в адресе электронной почты отправителя.

**Отклик о сбое**   `530 5.7.1 Client was not authenticated`

**Возможные причины сбоя**   Сервер назначения не принимает анонимную отправку сообщений. Эта ошибка возникает при попытке использовать Telnet для отправки сообщения напрямую на транспортный сервер-концентратор.

## RCPT TO:kate@fabrikam.com NOTIFY=success,failure

**Отклик об успешном выполнении**   `250 2.1.5 Recipient OK`

**Отклик о сбое**   `550 5.1.1 User unknown`

**Возможные причины сбоя.**   Указанный получатель не существует в организации.
