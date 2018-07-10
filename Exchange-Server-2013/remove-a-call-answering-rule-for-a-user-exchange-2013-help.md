﻿---
title: 'Удаление правила автоответчика для пользователя: Exchange 2013 Help'
TOCTitle: Удаление правила автоответчика для пользователя
ms:assetid: 1da3c5bc-7227-4b37-96f6-67ceefc084d5
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ898497(v=EXCHG.150)
ms:contentKeyID: 51408010
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Удаление правила автоответчика для пользователя

 

_**Применимо к:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:**2015-04-08_

С помощью командной консоли можно удалить одно или несколько правил автоответчика для пользователя. Кроме того, в сценарии командной консоли Exchange можно использовать командлет **Remove-UMCallAnsweringRule**, чтобы удалить одно или несколько правил автоответчика для нескольких пользователей.

Способ, которым правила автоответчика применяются ко входящим вызовам, аналогичен способу, которым правила для папки "Входящие" применяются к входящим сообщениям электронной почты. По умолчанию при включения для пользователя единой системы обмена сообщениями ни одно правило автоответчика не настроено. Но даже в этом случае почтовая система отвечает на входящие вызовы, и абоненты получают приглашение оставить голосовое сообщение.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ126620.note(EXCHG.150).gif" title="Примечание" alt="Примечание" />Примечание.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Пользователи, включенные в единую систему обмена сообщениями, могут войти в Outlook Web App, чтобы создавать и удалять правила ответа на вызовы, а также управлять ими.</td>
</tr>
</tbody>
</table>


Сведения о дополнительных задачах управления, связанных с правилами ответа на вызовы, см. в статье [Переадресация звонков процедур](forwarding-calls-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: менее 1 минуты.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись "Правила ответа на вызовы единой системы обмена сообщениями" в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Перед выполнением этой процедуры убедитесь, что абонентская группа единой системы обмена сообщениями создана. Дополнительные сведения см. в статье [Создание абонентской группы единой системы обмена сообщениями](create-a-um-dial-plan-exchange-2013-help.md).

  - Перед выполнением этой процедуры убедитесь, что политика почтовых ящиков единой системы обмена сообщениями создана. Дополнительные сведения см. в статье [Создание политики почтовых ящиков единой системы обмена сообщениями](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Перед выполнением этой процедуры убедитесь, что для почтового ящика пользователя включена поддержка единой системы обмена сообщениями. Дополнительные сведения см. в статье [Включение для пользователя поддержки голосовой почты](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Для выполнения этой процедуры можно использовать только командную консоль. Сведения о том, как открыть командную консоль Exchange в локальной организации Exchange, см. в статье [Открытие командной консоли Exchange](https://technet.microsoft.com/ru-ru/library/dd638134\(v=exchg.150\)). Сведения о том, как с помощью Оболочка Windows PowerShell подключаться к Exchange Online, см. в статье [Подключение к PowerShell для Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="Совет" alt="Совет" />Совет.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..</td>
</tr>
</tbody>
</table>


## Удаление правила автоответчика с помощью командной консоли

В этом примере показано, как удалить правило автоответчика `MyUMCallAnsweringRule` из почтового ящика пользователя. Почтовый ящик пользователя – это почтовый ящик пользователя, запустившего командлет.

    Remove-UMCallAnsweringRule -Identity MyUMCallAnsweringRule

В этом примере показано, как удалить правило автоответчика `MyUMCallAnsweringRule` из почтового ящика пользователя Tony Smith.

    Remove-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith
