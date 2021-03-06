﻿---
title: 'Управление ведением журнала аудита администраторов: Exchange 2013 Help'
TOCTitle: Управление ведением журнала аудита администраторов
ms:assetid: 15c284c0-b8e6-42ca-9913-7c59fdb6885d
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dd335109(v=EXCHG.150)
ms:contentKeyID: 50556340
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Управление ведением журнала аудита администраторов

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2013-05-17_

Ведение журнала аудита администратора в Microsoft Exchange Server 2013 позволяет создавать запись журнала при каждом запуске определенного командлета. В записях журнала уточняется, какой командлет выполнен, какие параметры использованы, кто выполнял командлет, а также какие объекты задействованы. Дополнительные сведения о ведении журнала аудита администратора см. в разделе [Ведение журнала аудита администратора](administrator-audit-logging-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения каждой процедуры: менее 5 минут.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись "Ведение журнала аудита администратора" в разделе [Разрешения инфраструктуры Exchange и командной консоли](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

  - При ведении журнала аудита администратора используется репликация Active Directory для выполнения репликации параметров конфигурации, указанных для контроллеров домена в организации. В зависимости от параметров репликации выполненные изменения не сразу применяются ко всем серверам Exchange 2013 в организации.

  - На компьютерах, на которых во время изменения конфигурации открыта командная консоль, изменения конфигурации журнала аудита обновляются каждые 60 минут. Если изменения необходимо применить немедленно, на каждом компьютере закройте и снова откройте консоль.

  - После запуска команды может пройти до 15 минут, прежде чем она появится в результатах поиска журнала аудита. Это связано с тем, что перед поиском необходимо выполнить индексацию записей журнала аудита. Если команда не появляется в журнале аудита администратора, подождите несколько минут и снова выполните поиск.

  - Для выполнения этих процедур необходимо использовать командную консоль Exchange.

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Что необходимо сделать?

## Укажите командлеты для аудита

По умолчанию в журналах аудита создается запись для каждого выполняемого командлета. Если ведение журнала аудита включено впервые и необходимо, чтобы это действие выполнялось далее, список аудита командлетов изменять не требуется. Если были указаны командлеты для аудита, но теперь необходимо выполнить аудит всех командлетов, это можно сделать с помощью подстановочного знака "звездочка" (\*) с параметром *AdminAuditLogCmdlets* командлета **Set-AdminAuditLogConfig**, как показано в следующей команде:

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets *

Можно указать командлеты для аудита, задав список командлетов с помощью параметра *AdminAuditLogCmdlets*. В списке командлетов для аудита можно указать определенные командлеты, командлеты с подстановочным знаком "звездочка" (\*) или и те и другие. Записи в списке разделяются запятыми. Допустимы следующие значения:

  - `New-Mailbox`

  - `*TransportRule`

  - `*Management*`

  - `Set-Transport*`

В этом примере выполняется аудит командлетов, указанных в предыдущем списке.

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets New-Mailbox, *TransportRule, *Management*, Set-Transport*

Дополнительные сведения о синтаксисе и параметрах см. в разделе [Set-AdminAuditLogConfig](https://technet.microsoft.com/ru-ru/library/dd298169\(v=exchg.150\)).

## Задание параметров для аудита

По умолчанию в журналах аудита создается запись для каждого выполняемого командлета, независимо от указанных параметров. Если ведение журнала аудита включено впервые и необходимо, чтобы это действие выполнялось далее, список аудита параметров изменять не требуется. Если были указаны параметры для аудита, но теперь необходимо выполнить аудит всех параметров, это можно сделать с помощью подстановочного знака "звездочка" (\*) с параметром *AdminAuditLogParameters* командлета **Set-AdminAuditLogConfig**, как показано в следующей команде:

    Set-AdminAuditLogConfig -AdminAuditLogParameters *

Параметры для аудита можно указать с помощью параметра *AdminAuditLogParameters*. В списке параметров для аудита можно указать отдельные параметры, параметры с подстановочным знаком "звездочка" (\*) или и те и другие. Записи в списке разделяются запятыми. Допустимы следующие значения:

  - `Database`

  - `*Address*`

  - `Custom*`

  - `*Region`

> [!NOTE]  
> Для создания записи журнала аудита при выполнении команды эта команда должна включать в себя как минимум один или несколько параметров одного или нескольких командлетов, указанных с помощью параметра <em>AdminAuditLogCmdlets</em>.


В этом примере выполняется аудит параметров, указанных в предыдущем списке.

    Set-AdminAuditLogConfig -AdminAuditLogParameters Database, *Address*, Custom*, *Region

Дополнительные сведения о синтаксисе и параметрах см. в разделе [Set-AdminAuditLogConfig](https://technet.microsoft.com/ru-ru/library/dd298169\(v=exchg.150\)).

## Указание времени хранения журнала аудита

Время хранения журнала аудита определяет период, в течение которого будут храниться записи журнала аудита. При превышении времени хранения записи журнала она удаляется. Значение по умолчанию — 90 дней.

Можно указать число дней, часов, минут и секунд, в течение которых необходимо хранить записи журнала аудита. Чтобы задать значение, используйте формат dd.hh.mm:ss, где:

  - **dd** — количество дней хранения записи журнала аудита

  - **hh** — количество часов хранения записи журнала аудита;

  - **mm** — количество минут хранения записи журнала аудита;

  - **ss** — количество секунд хранения записи журнала аудита.

> [!CAUTION]  
> Для времени хранения журнала аудита можно установить меньшее значение по сравнению с текущим временем хранения. При этом все записи журнала аудита, длительность хранения которых превысит новое время хранения, будут удалены.<br />
Если для времени хранения установлено значение 0, все записи в журнале аудита будут удалены системой Exchange.<br />
Разрешения на настройку времени хранения журнала аудита рекомендуется предоставлять только пользователям с высоким уровнем доверия.


В этом примере указывается время хранения, равное двум годам и шести месяцам.

    Set-AdminAuditLogConfig -AdminAuditLogAgeLimit 913.00:00:00

Дополнительные сведения о синтаксисе и параметрах см. в разделе [Set-AdminAuditLogConfig](https://technet.microsoft.com/ru-ru/library/dd298169\(v=exchg.150\)).

## Включение и отключение ведения журнала командлетов проверки

По умолчанию командлеты, начинающиеся с глагола **Test**, не заносятся в журнал. Причиной этого является то, что командлеты **Test** могут создавать большой объем данных за короткий период времени. Включать ведение журнала командлетов **Test** рекомендуется только на короткий период времени.

Эта команда включает ведение журнала командлетов **Test**.

    Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $True

Эта команда отключает ведение журнала командлетов **Test**.

    Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $False

Дополнительные сведения о синтаксисе и параметрах см. в разделе [Set-AdminAuditLogConfig](https://technet.microsoft.com/ru-ru/library/dd298169\(v=exchg.150\)).

## Отключение ведения журнала аудита администратора

Чтобы отключить ведение журнала аудита администратора, используйте следующую команду.

    Set-AdminAuditLogConfig -AdminAuditLogEnabled $False

## Включение ведения журнала аудита администратора

Чтобы включить ведение журнала аудита администратора, используйте следующую команду.

    Set-AdminAuditLogConfig -AdminAuditLogEnabled $True

## Просмотр параметров ведения журнала аудита администратора

Чтобы просмотреть параметры ведения журнала аудита администратора, настроенного в организации, используйте следующую команду.

    Get-AdminAuditLogConfig

