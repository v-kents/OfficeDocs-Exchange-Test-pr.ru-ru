﻿---
title: 'Создайте соединитель отправки для маршрутизации исходящей почты через промежуточный узел: Exchange 2013 Help'
TOCTitle: Создайте соединитель отправки для маршрутизации исходящей почты через промежуточный узел
ms:assetid: 4a9ef08e-bd62-4c6b-8790-d24fb0f8f24b
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ673059(v=EXCHG.150)
ms:contentKeyID: 50488006
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Создайте соединитель отправки для маршрутизации исходящей почты через промежуточный узел

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2013-02-07_

В некоторых ситуациях необходимо для пересылки сообщений электронной почты через сторонний промежуточный сайт, например, в экземпляре, где находятся Network Appliance, которые нужно регистрировать в журнале проверок правил исходящих сообщений.

> [!NOTE]  
> Сторонний промежуточный узел должен использовать SMTP для транспортировки. Если этого не произошло, необходимо использовать внешние соединители или соединителя агента доставки.


Хотите узнать о сценариях, где используется эта процедура? См. следующие разделы:

  - [Настройка потока обработки почты и клиентского доступа](configure-mail-flow-and-client-access-exchange-2013-help.md)

## Что нужно знать перед началом работы?

  - Осталось времени до завершения: 15 минут

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись «Соединители отправки» в разделе [Разрешения потока обработки почты](mail-flow-permissions-exchange-2013-help.md).

  - Если вы находитесь на начальном этапе установки, см. [Развертывание новой установки Exchange 2013](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md). После установки следуйте шагам, описанным в этом разделе, чтобы создать внешний соединитель.

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Используйте EAC для создания соединителя отправки для маршрутизации исходящей электронной почты через промежуточный сайт

1.  На консоли администрирования Exchange перейдите в раздел **Поток почты** \> **Соединители отправки** и нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления").

2.  В **создать соединитель отправки** мастера, укажите имя соединителя отправки и выберите **обычай** для **напечатать** . Обычно, когда вы хотите выбрать этот выбор маршрута сообщений на компьютеры без операционной системы Microsoft Exchange Server 2013. Нажмите кнопку **Далее**.

3.  Выбрать **Маршрутизация почты через промежуточные сайты** , а затем **добавить** ![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления"). В окно **Добавить промежуточный сайте** , задания IP-адреса, такие как 192.168.100.1, или полностью определенное имя домена (FQDN), например contoso.com. Щелкните **сохранить** .
    
    Для **подлинности промежуточного узла** , выбрать необходимый тип проверки подлинности промежуточного узла по. Если выбрано **обычная проверка подлинности** , необходимо ввести имя пользователя и пароль.
    
    > [!NOTE]  
    > Если выбрать обычную проверку подлинности, настоятельно рекомендуется использовать зашифрованное подключение, так как имя пользователя и пароль отправляются в виде открытого текста.


4.  В разделе **Адресное пространство** нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления"). В окне **Добавить домен** укажите SMTP как **Тип**. Для **(FQDN) полным доменным именем** , введите \*, чтобы указать, что этот соединитель отправки применяется к сообщениям, отправленным на любом домене. Нажмите кнопку **Сохранить**.

5.  Для **Исходный сервер** нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления"). В окне **Выбор сервера** выберите сервер почтовых ящиков, который будет использоваться для отправки почты в Интернет через сервер клиентского доступа, и нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления"). Выбрав членов, нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления"). Нажмите кнопку **ОК**.

6.  Нажмите кнопку **Готово**.

После создания он появится в списке соединителей получения.

## Как проверить, что все получилось?

Чтобы убедиться в том, что Вы успешно создали соединителя отправки для маршрутизации исходящей электронной почты через промежуточный сайт, отправки сообщения от пользователя в организации (можно использовать Outlook Web App) в домен был указан для **адресного пространства** . Если пользователь получает такое сообщение, то правильной настройке отправляющего соединителя.

## Дополнительные сведения

[Создание соединителя отправки для электронной почты, отправляемой в Интернет](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[Соединители отправки](send-connectors-exchange-2013-help.md)

