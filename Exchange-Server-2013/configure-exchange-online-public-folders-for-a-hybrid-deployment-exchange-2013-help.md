﻿---
title: 'Настройка общедоступных папок Exchange Online для гибридного развертывания: Exchange 2013 Help'
TOCTitle: Настройка общедоступных папок Exchange Online для гибридного развертывания
ms:assetid: d979edb3-967b-4431-8beb-0c236bf7f56d
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Mt729076(v=EXCHG.150)
ms:contentKeyID: 72768733
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Настройка общедоступных папок Exchange Online для гибридного развертывания

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2016-12-15_

**Сводка.** Инструкции по предоставлению пользователям локальной среды Exchange 2013 доступа к общедоступным папкам в Exchange Online.

В гибридном развертывании пользователи могут подключаться к Exchange Online или работать локально, и ваши общедоступные папки могут храниться в Exchange Online или локально. Иногда подключенным пользователям может потребоваться доступ к общедоступным папкам в локальной среде Exchange Server 2013. Аналогично пользователям Exchange 2013 может потребоваться доступ к общедоступным папкам в Office 365 или Exchange Online.

В этой статье описано, как предоставить пользователям локальной среды Exchange 2013 доступ к общедоступным папкам Exchange Online или Office 365. Сведения о том, как предоставить пользователям Exchange Online или Office 365 доступ к общедоступным папкам в локальной среде Exchange 2013, см. в статье [Настройка общедоступных папок Exchange 2013 для гибридного развертывания](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md).

> [!NOTE]  
> Если у вас есть общедоступные папки Exchange 2010 или Exchange 2007, ознакомьтесь с разделом <a href="configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md">Настройка локальных общедоступных папок прежних версий для гибридного развертывания</a>.


## Что нужно знать перед началом работы

1.  Эти указания предполагают, что использовался мастер гибридных конфигураций для настройки и синхронизации ваших локальных сред и сред Exchange Online и что записи DNS, которые использовались для ссылок AutoDiscover большинства пользователей, относятся к локальной конечной точке. Подробнее см. в разделе [Мастер гибридной конфигурации](https://technet.microsoft.com/ru-ru/library/hh529921\(v=exchg.150\)).

2.  Эти указания предполагают, что мобильный Outlook включен и работает на локальных серверах Exchange. Сведения о включении мобильного Outlook см. в разделе [Мобильный Outlook](outlook-anywhere-exchange-2013-help.md).

3.  Настраивая сосуществование общедоступных папок для гибридного развертывания Exchange с Office 365, возможно, понадобится устранять конфликты, возникающие в процессе импорта. Не поддерживающий маршрутизацию адрес электронной почты, назначенный общедоступным папкам, поддерживающим почту, может конфликтовать с другими пользователями и группами в Office 365, а также другими атрибутами.

4.  Чтобы получать доступ к общедоступным папкам на различных площадках, пользователям необходимо обновить свои клиенты Outlook с помощью общедоступного обновления Outlook за ноябрь 2012 г. или более поздней версии.
    
    1.  Чтобы скачать обновление за ноябрь 2012 г. для Outlook 2010, см. статью с [обновлением для 32-разрядного выпуска Microsoft Outlook 2010 (KB2687623)](https://www.microsoft.com/ru-ru/download/details.aspx?id=35702).
    
    2.  Чтобы скачать обновление Outlook за ноябрь 2012 г. для Outlook 2007, см. страницу [Обновление для Microsoft Office Outlook 2007 (KB2687404)](https://www.microsoft.com/ru-ru/download/details.aspx?id=35718).

5.  Outlook 2011 для Mac и Outlook для Mac для Office 365 не поддерживаются для общих папок между организациями. Для доступа к общедоступным папкам пользователи Outlook 2011 для Mac или Outlook для Mac для Office 365 должны находиться в том же расположении, что и папки. Кроме того, пользователи, чьи почтовые ящики расположены в службе Exchange Online, не смогут получить доступ к локальным общедоступным папкам с помощью Outlook Web App.
    
    > [!NOTE]  
    > Outlook 2016 для Mac поддерживается в случае общедоступных папок в гибридной среде. Если клиенты в организации используют Outlook 2016 для Mac, убедитесь, что для них установлено обновление за апрель 2016 г. В противном случае такие пользователи не смогут получать доступ к общедоступным папкам при гибридной топологии. Дополнительные сведения см. в статье <a href="accessing-public-folders-with-outlook-2016-for-mac-exchange-2013-help.md">Доступ к общедоступным папкам с помощью Outlook 2016 для Mac</a>.


## Шаг 1. Загрузка скриптов

1.  Скачайте указанные ниже файлы на странице [Общедоступные папки, поддерживающие почту: скрипт синхронизации каталогов в Exchange Online с локальной средой](https://go.microsoft.com/fwlink/p/?linkid=797795).
    
      - `Import-PublicFolderMailboxes.ps1`
    
      - `ImportPublicFolderMailboxes.strings.psd1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.ps1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.strings.psd1`

2.  Сохраните файлы на локальном компьютере, с которого вы планируете запустить PowerShell. Например, в папку C:\\PFScripts.

## Шаг 2. Настройка синхронизации службы каталогов

Запустив скрипт `Sync-MailPublicFoldersCloudToOnprem.ps1`, вы синхронизируете общедоступные папки, поддерживающие почту, между Exchange Online и локальной средой Exchange 2013. Для таких папок необходимо повторно создать специальные разрешения в облаке, так как при гибридном развертывании не поддерживаются гибридные разрешения. Дополнительные сведения см. в статье [Гибридное развертывание Exchange Server 2013](https://technet.microsoft.com/ru-ru/59e32000-4fcf-417f-a491-f1d8f9aeef9b\(exchg.150\)#doc).

> [!NOTE]  
> Синхронизированные общедоступные папки, поддерживающие почту, отображаются как объекты почтовых контактов для потока обработки почты и не видны в Центре администрирования Exchange. См. сведения о команде Get-MailPublicFolder. Чтобы повторно создать разрешения SendAs в облаке, используйте команду Add-RecipientPermission.


1.  На сервере Exchange 2013 выполните указанную ниже команду, чтобы синхронизировать с локальным каталогом Active Directory общедоступные папки Exchange Online или Office 365, поддерживающие почту.
    
        Sync-MailPublicFoldersCloudToOnprem.ps1 -Credential (Get-Credential)
    
    Здесь `Credential` — пароль и имя пользователя Office 365.

> [!NOTE]  
> Рекомендуем запускать этот скрипт ежедневно, чтобы синхронизировать общедоступные папки, поддерживающие почту.


## Шаг 3. Настройка доступа к общедоступным папкам Exchange Online для локальных пользователей

Остается настроить локальную организацию Exchange 2013, чтобы разрешить доступ к общедоступным папкам Exchange Online.

Скрипт `Import-PublicFolderMailboxes.ps1` импортирует объекты почтовых ящиков общедоступных папок в качестве пользователей, поддерживающих почту, из облака в локальную среду. Этот скрипт также настроит импортированные объекты как удаленные почтовые ящики общедоступных папок.

1.  На сервере Exchange 2013 выполните указанную ниже команду, чтобы импортировать объекты почтовых ящиков общедоступных папок из облака в локальный каталог Active Directory.
    
        Import-PublicFolderMailboxes.ps1 -Credential (Get-Credential)
    
    Здесь `Credential` — пароль и имя пользователя Office 365.
    
    > [!NOTE]  
    > Когда почтовые ящики общедоступных папок достигают порогового размера, они автоматически разделяются на несколько новых. Поэтому рекомендуем запускать этот скрипт ежедневно, чтобы обеспечить импорт последних объектов таких почтовых ящиков из облака.


2.  Обеспечьте доступ к общедоступным папкам Exchange Online для локальной организации Exchange 2013.
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote

> [!NOTE]  
> Вы сможете увидеть изменения, когда завершится синхронизация ActiveDirectory. Это может занять до 3-х часов. Если вы не хотите дожидаться повторения синхронизации каждые три часа, можно в любое время выполнить принудительную синхронизацию службы каталогов. Дополнительные сведения о действиях по принудительной синхронизации службы каталогов см. в разделе <a href="http://technet.microsoft.com/ru-ru/library/jj151771.aspx">Принудительная синхронизация служб каталогов</a> соответствующей статьи.


## Как проверить, что это работает

1.  Войдите в Outlook для пользователя, который находится в Exchange Online, и выполните следующие проверки общедоступных папок.
    
      - Просмотр иерархии.
    
      - Проверка разрешений.
    
      - Создание и удаление общедоступных папок.
    
      - Опубликуйте содержимое в общедоступной папке и удалите его.

