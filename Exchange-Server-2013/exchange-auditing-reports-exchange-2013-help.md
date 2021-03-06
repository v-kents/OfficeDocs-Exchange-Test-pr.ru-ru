﻿---
title: 'Отчеты аудита Exchange: Exchange 2013 Help'
TOCTitle: Отчеты аудита Exchange
ms:assetid: 2b3e1529-1677-4564-be0b-ce22757ddc0d
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ150497(v=EXCHG.150)
ms:contentKeyID: 50487153
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Отчеты аудита Exchange

 

_**Применимо к:** Exchange Online, Exchange Server 2013_

_**Последнее изменение раздела:** 2016-12-09_

Используйте журнал аудита для устранения проблем с конфигурацией и обеспечения соблюдения нормативных и законодательных требований путем отслеживания отдельных изменений, вносимых администраторами. В Microsoft Exchange доступно два вида журналов аудита:

  - В *журнал аудита администраторов* записываются все действия, выполняемые администратором, на основе командлета консоли управления Exchange. Это позволяет устранять неполадки конфигурации или выявлять причины проблем безопасности или соответствия требованиям. В Exchange Online также записываются действия, которые выполняют администраторы Microsoft и полномочные администраторы.

  - *В журнале аудита почтового ящика* регистрируются случаи доступа к почтовому ящику со стороны его владельца, администратора или делегированного пользователя. Это позволяет определить, кто обращался к почтовому ящику, а также какие действия были выполнены.

В этом разделе рассматривается следующее.

  - Экспорт журналов аудита

  - Запуск отчетов аудита

  - Настройка ведения журнала аудита
    
      - Включение ведения журнала аудита почтовых ящиков
    
      - Предоставление пользователям доступ к отчетам аудита
    
      - Включение XML-вложений в Outlook Web App

## Экспорт журналов аудита

На странице **Управление соответствием требованиям** \> **Аудит** в Центре администрирования Exchange (EAC) можно выполнить поиск и экспорт записей из журнала аудита администратора и журнала аудита почтовых ящиков.

  - **Экспорт журнала аудита действий администратора**   Все действия, выполняемые с помощью командлета командной консоли Exchange, названия которых не начинаются с глаголов **Get**, **Search** и **Test**, заносятся в журнал аудита действий администратора. В записях журнала аудита указывается запущенный командлет, его параметры и их значения, а также успешность выполнения. Записи в журнале аудита администратора можно искать и экспортировать. При экспорте результатов поиска Microsoft Exchange сохраняет их в XML-файл и прикрепляет их к сообщению электронной почты. Дополнительные сведения:
    
      - [Поиск изменений группы ролей или журналов аудита администраторов](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)
    
      - [Просмотр и экспорт журнала аудита действий внешнего администратора](https://technet.microsoft.com/ru-ru/library/dn505728\(v=exchg.150\))
    
    > [!NOTE]  
    > По умолчанию записи журнала аудита действий администратора хранятся в течение 90 дней. Когда срок хранения записи превышает 90 дней, она удаляется. Этот параметр невозможно изменить в облачной организации. Но его можно изменить в локальной организации Exchange с помощью командлета <strong>Set-AdminAuditLog</strong>.


  - **Экспорт журналов аудита почтовых ящиков**. Если для почтового ящика включено ведение журнала аудита почтового ящика, Microsoft Exchange регистрирует в этом журнале действия над данными в почтовом ящике со стороны пользователей, не являющихся владельцами. Журнал аудита почтового ящика хранится в скрытой папке почтового ящика, для которого включен аудит. Ведение журнала аудита почтового ящика можно настроить для регистрации действий владельцев. В записях такого журнала указывается, кто и когда обращался к почтовому ящику, какие действия при этом были выполнены и были ли они успешными. При поиске записей в журнале аудита почтового ящика и их экспорте Microsoft Exchange сохраняет результаты поиска в XML-файл и прикрепляет их к электронному сообщению. Дополнительные сведения см. в статье [Экспорт журналов аудита почтовых ящиков](export-mailbox-audit-logs-exchange-2013-help.md).

## Запуск отчетов аудита

При запуске следующих отчетов на странице **Аудит** в Центре администрирования Exchange результаты отображаются в области сведений отчета.

  - **Отчет о доступе к чужим почтовым ящикам**   Этот отчет используется для поиска почтовых ящиков, к которым обращались пользователи, не владеющие ими. Дополнительные сведения см. в разделе [Запуск отчета об обращениях к почтовым ящикам от пользователей, не являющихся их владельцами](run-a-non-owner-mailbox-access-report-exchange-online-help.md).

  - **Отчет о группе ролей администраторов**   Этот отчет используется для поиска изменений в группах ролей администраторов. Подробнее см. в разделе [Поиск изменений группы ролей или журналов аудита администраторов](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md).

  - **Запуск отчета об обнаружении и хранении данных на месте**   Этот отчет используется для поиска почтовых ящиков, поставленных на хранение на месте или снятых с него. Дополнительные сведения:
    
      - [Хранение на месте и хранение для судебного разбирательства](in-place-hold-and-litigation-hold-exchange-2013-help.md)
    
      - [Обнаружение электронных данных на месте](in-place-ediscovery-exchange-2013-help.md)

  - **Запуск отчета о хранении для судебного разбирательства для каждого почтового ящика в отдельности**   Этот отчет используется для поиска почтовых ящиков, поставленных на хранение для судебного разбирательства или снятых с него. Дополнительные сведения см. в следующих разделах.
    
      - [Запуск отчета судебного удержания отдельного почтового ящика](run-a-per-mailbox-litigation-hold-report-exchange-2013-help.md)
    
      - [Перевод почтового ящика в режим хранения для судебного разбирательства](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - **Запуск отчета журнала аудита действий администратора**   Этот отчет используется для просмотра записей в журнале аудита действий администратора. Вместо того чтобы экспортировать журнал аудита действий администратора, на получение сообщения электронной почты с которым может уйти до 24 часов, вы можете запустить этот отчет в Центре администрирования Exchange. В этот отчет записываются изменения, которые администраторы вашей организации внесли в конфигурацию. На нескольких страницах отображается до 5000 записей. Чтобы сузить поиск, можно указать диапазон дат. Дополнительные сведения:
    
      - [Просмотр журнала аудита администратора](view-the-administrator-audit-log-exchange-2013-help.md)
    
      - [Ведение журнала аудита администратора](administrator-audit-logging-exchange-2013-help.md)

  - **Запуск отчета журнала аудита действий внешнего администратора**   Этот отчет доступен только в Exchange Online и Exchange Online Protection. В журнал аудита действий администратора записываются действия, которые выполняют администраторы Microsoft или полномочные администраторы. Отчет журнала аудита действий внешнего администратора используется для поиска и просмотра действий с конфигурацией организации Exchange Online, которые выполняют администраторы, не входящие в вашу организацию. Дополнительные сведения см. в разделе [Просмотр и экспорт журнала аудита действий внешнего администратора](https://technet.microsoft.com/ru-ru/library/dn505728\(v=exchg.150\)).

## Настройка ведения журнала аудита

Для запуска отчетов аудита и экспорта журналов аудита необходимо настроить ведение журналов аудита для вашей организации.

## Включение ведения журнала аудита почтовых ящиков

Ведение журнала аудита почтовых ящиков включается для всех почтовых ящиков, по которым следует составлять отчет о доступе пользователей, не являющихся владельцами. Если ведения журнала аудита почтовых ящиков не включено для почтового ящика, вы не получите результаты при запуске отчета для него или экспорте журнала аудита почтового ящика.

Чтобы включить ведения журнала аудита для одного почтового ящика, выполните следующую команду в командной консоли.

    Set-Mailbox <Identity> -AuditEnabled $true

Чтобы включить аудит для всех почтовых ящиков пользователей в организации, выполните следующие команды:

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

Дополнительные сведения о настройке регистрации нужных действий в журнале см. в таких статьях:

  - **Exchange 2013**   [Включение и отключение ведения журнала аудита для почтового ящика](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)

  - **Exchange Online**   [Включение аудита почтовых ящиков в Office 365](https://go.microsoft.com/fwlink/p/?linkid=626109)

## Предоставление пользователям доступ к отчетам аудита

По умолчанию администраторы могут получить доступ к любым отчетам и запустить их на странице "Аудит" в EAC. При этом другим пользователям, например юристам или делопроизводителям, также можно назначить нужные разрешения.

Самым простым способом предоставить пользователям доступ является добавление в группу ролей "Управление записями". Вы также можете использовать командную консоль, чтобы предоставить пользователям доступ к странице **Аудит** в Центре администрирования Exchange, назначив им роль "Журналы аудита".

## Добавление пользователя в группу ролей "Управление записями"

1.  Перейдите к разделу **Разрешения** \> **Роли администраторов**.

2.  Выберите **Управление записями** в списке групп ролей и нажмите кнопку **Изменить**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

3.  В области **Члены** нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления").

4.  Укажите пользователя в диалоговом окне **Выбрать членов группы**. Можно выполнить поиск пользователя, введя отображаемое имя (полностью или частично) и нажав кнопку **Поиск**![значок поиска](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "значок поиска"). Можно также отсортировать список, щелкнув заголовок столбца **Имя** или **Отображаемое имя**.

5.  Нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления"), затем кнопку **ОК**, чтобы вернуться на страницу группы ролей.

6.  Нажмите кнопку **Сохранить**, чтобы сохранить изменения в группе ролей.

В области сведений пользователь будет указан в разделе **Члены** и сможет получить доступ к странице аудита в EAC, запустить отчеты аудита и экспортировать журналы аудита.

## Назначение пользователю роли "Журналы аудита"

Чтобы назначить роль "Журналы аудита" пользователю, выполните следующую команду.

    New-ManagementRoleAssignment -Role "Audit Logs" -User <Identity>

Это позволяет пользователю выбрать **Управление соответствием требованиям** \> **Аудит** в EAC для запуска любых отчетов. Пользователь также может экспортировать журнал аудита почтовых ящиков и просматривать журнал аудита администратора.

> [!NOTE]  
> Чтобы позволить пользователю запускать отчеты аудита, но не разрешать экспортировать журналы аудита, используйте предыдущую команду для назначения роли только для просмотра журналов аудита.


## Включение XML-вложений в Outlook Web App

При экспорте журнала аудита почтовых ящиков или журнала аудита администратора Microsoft Exchange прикрепляет XML-файл журнала аудита к сообщению электронной почты. Однако по умолчанию Outlook Web App блокирует XML-вложения. Если вы хотите использовать Outlook Web App для доступа к журналам аудита, вы должны настроить Outlook Web App, чтобы разрешить XML-вложения.

Чтобы разрешить XML-вложения в Outlook Web App, выполните следующую команду:

    Set-OwaMailboxPolicy -Identity Default -AllowedFileTypes '.rpmsg','.xlsx','.xlsm','.xlsb','.tiff','.pptx','.pptm','.ppsx','.ppsm','.docx','.docm','.zip','.xls','.wmv','.wma','.wav','.vsd','.txt','.tif','.rtf','.pub','.ppt','.png','.pdf','.one','.mp3','.jpg','.gif','.doc','.bmp','.avi','.xml'

