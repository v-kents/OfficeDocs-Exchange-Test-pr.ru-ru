﻿---
title: 'Настройка отслеживания сообщений: Exchange 2013 Help'
TOCTitle: Настройка отслеживания сообщений
ms:assetid: 50eb5213-cf27-4179-b427-38d751ee4a70
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Aa997984(v=EXCHG.150)
ms:contentKeyID: 51408026
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Настройка отслеживания сообщений

 

_**Применимо к:**Exchange Server 2013_

_**Последнее изменение раздела:**2013-02-18_

Отслеживание сообщений записывает действия, выполняемые транспортом SMTP, для всех сообщений, передаваемых и получаемых транспортной службой или почтовыми ящиками, находящимися на сервере почтовых ящиков Microsoft Exchange Server 2013. Журналы отслеживания сообщений можно использовать для изучения сообщений, анализа потока почты, создания отчетов и устранения неполадок.

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: 15 минут.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Записи "Транспортная служба" в разделе [Разрешения потока обработки почты](mail-flow-permissions-exchange-2013-help.md) или запись "Настройка сервера почтовых ящиков" в разделе [Разрешения получателей](recipients-permissions-exchange-2013-help.md).

  - Можно использовать Центр администрирования Exchange, чтобы включать или выключать отслеживание сообщений, а также чтобы задать путь к журналу отслеживания сообщений. Чтобы настроить все остальные параметры отслеживания сообщений, необходимо использовать командную консоль Exchange.

  - На сервере почтовых ящиков Exchange 2013 можно использовать командлеты **Set-TransportService** или **Set-MailboxServer**, чтобы настроить параметры отслеживания сообщений. В процедурах, описанных в этом разделе, используется командлет **Set-TransportService**.

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


## Настройка отслеживания сообщений на серверах почтовых ящиков с помощью Центра администрирования Exchange

1.  В Центре администрирования Exchange перейдите к разделу **Серверы** \> **Серверы**.

2.  Выберите необходимый сервер почтовых ящиков и нажмите кнопку **Изменить**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

3.  На странице свойств сервера щелкните **Журналы транспорта**.

4.  В разделе **Журнал отслеживания сообщений** измените один из следующих параметров.
    
      - **Включить журнал отслеживания сообщений**   Чтобы отключить отслеживание сообщений на сервере, снимите этот флажок. Чтобы включить отслеживание сообщений на сервере, установите этот флажок.
    
      - **Путь к журналу отслеживания сообщений**   Указываемый путь должен вести на локальный сервер Exchange. Если папка не существует, она будет создана после нажатия кнопки **Сохранить**.

5.  Нажмите кнопку **Сохранить**.

## Настройка отслеживания сообщений с помощью командной консоли

Чтобы настроить отслеживание сообщений, выполните следующую команду.

    Set-TransportService <ServerIdentity> -MessageTrackingLogEnabled <$true | $false> -MessageTrackingLogMaxAge <dd.hh:mm:ss> -MessageTrackingLogMaxDirectorySize <Size> -MessageTrackingLogMaxFileSize <Size> -MessageTrackingLogPath <LocalFilePath> -MessageTrackingLogSubjectLoggingEnabled <$true|$false>

В этом примере показано, как установить следующие параметры журнала отслеживания сообщений на сервере почтовых ящиков с именем Mailbox01.

  -  
    Задает для файлов журнала отслеживания сообщений расположение D:\\Message Tracking Log. Обратите внимание, что если папка не существует, она будет создана.

  -  
    Задает максимальный размер файла журнала отслеживания сообщений равным 20 МБ.

  -  
    Задает максимальный размер каталога журнала отслеживания сообщений равным 1,5 ГБ.

  -  
    Задает максимальный срок хранения файла журнала отслеживания сообщений равным 45 дням.

<!-- end list -->

    Set-TransportService Mailbox01 -MessageTrackingLogPath "D:\Hub Message Tracking Log" -MessageTrackingLogMaxFileSize 20MB -MessageTrackingLogMaxDirectorySize 1.5GB -MessageTrackingLogMaxAge 45.00:00:00

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
<li><p>Если для параметра <em>MessageTrackingLogPath</em> задать значение <code>$null</code>, отслеживание сообщений будет выключено. Однако если параметру <em>MessageTrackingLogEnabled</em> задано значение <code>$true</code>, возникают ошибки журнала событий.</p></li>
<li><p>Если для параметра <em>MessageTrackingLogMaxAge</em> задать значение <code>00:00:00</code>, то автоматическое удаление файлов журнала отслеживания сообщений по истечении срока их хранения не будет выполняться.</p></li>
<li><p>Для серверов почтовых ящиков Exchange 2013 максимальный размер каталога журнала отслеживания сообщений в три раза больше значения параметра <em>MessageTrackingLogMaxDirectorySize</em>. Несмотря на то что файлы журнала отслеживания сообщений, создаваемые четырьмя различными службами, имеют четыре различных префикса имен, количество и частота данных, записываемых в файлы журнала <strong>MSGTRKMA</strong>, являются незначительными по сравнению с тремя другими префиксами. Дополнительные сведения см. в статье &quot;Структура файлов журнала отслеживания сообщений&quot; в разделе <a href="message-tracking-exchange-2013-help.md">Отслеживание сообщений</a>.</p></li>
</ul></td>
</tr>
</tbody>
</table>


В этом примере показано, как выключить ведение журнала темы сообщений в журнале отслеживания сообщений на сервере почтовых ящиков с именем Mailbox01.

    Set-TransportService Mailbox01 -MessageTrackingLogSubjectLoggingEnabled $false

В этом примере показано, как выключить отслеживание сообщений на сервере почтовых ящиков с именем Mailbox01.

    Set-TransportService Mailbox01 -MessageTrackingLogEnabled $false

## Как проверить, что все получилось?

Чтобы убедиться, что отслеживание сообщений настроено успешно, сделайте следующее.

1.  В командной консоли выполните следующую команду:
    
        Get-TransportService <ServerIdentity> | Format-List MessageTrackingLog*

2.  Убедитесь, что отображаются именно те значения, которые вы задали.
