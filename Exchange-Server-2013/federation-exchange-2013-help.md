﻿---
title: 'Федерация: Exchange 2013 Help'
TOCTitle: Федерация
ms:assetid: 0046e2eb-6940-4941-bd5b-cbe6bffa3b94
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dd335047(v=EXCHG.150)
ms:contentKeyID: 50487335
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Федерация

 

_**Применимо к:**Exchange Server 2013_

_**Последнее изменение раздела:**2016-12-09_

Информационным работникам часто необходимо взаимодействовать с внешними получателями, поставщиками, партнерами и клиентами, а также обмениваться с ними сведениями о доступности (доступности в календаре). Наличие федерации в системе Microsoft Exchange Server 2013 способствует этому взаимодействию. Под *федерацией* подразумевается базовая инфраструктура отношений доверия, поддерживающая *федеративный общий доступ*, — простой способ обмена данными календаря с получателями во внешних федеративных организациях. Дополнительные сведения о федеративном общем доступе см. в разделе [Общий доступ](sharing-exchange-2013-help.md).

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.important(EXCHG.150).gif" title="Важно" alt="Важно" />Важно!</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Эта возможность Exchange Server 2013 не совместима полностью со службой Office 365, предоставляемой компанией 21Vianet в Китае. Кроме того, возможны некоторые ограничения. <a href="https://go.microsoft.com/fwlink/?linkid=313640">Дополнительные сведения о службе Office 365, предоставляемой компанией 21Vianet</a>.</td>
</tr>
</tbody>
</table>


**Содержание**

Основные термины

Система проверки подлинности Azure AD

Доверие федерации

Идентификатор федеративной организации

Пример федерации

Требования к сертификатам для федерации

Переход на новый сертификат

Рекомендации относительно брандмауэра для федерации

## Основные термины

В следующей таблице определяются основные компоненты, связанные с федерацией в системе Exchange 2013.

  - **идентификатор приложения (AppID)**  
    Уникальный номер, сгенерированный системой проверки подлинности Azure Active Directory для идентификации организаций Exchange. AppID автоматически создается при создании отношения доверия федерации с системой проверки подлинности Azure Active Directory.

<!-- end list -->

  - **маркер делегирования**  
    Это маркер SAML (Security Assertion Markup Language), выдаваемый системой проверки подлинности Azure Active Directory, который позволяет пользователям из одной федеративной организации получать доверие от другой федеративной организации. Маркер делегирования содержит адрес электронной почты пользователя, неизменяемый идентификатор и сведения, связанные с предложением, по которому для действия выпускается маркер.

<!-- end list -->

  - **внешняя федеративная организация**  
    Внешняя организация Exchange, которая установила доверие федерации с системой проверки подлинности Azure Active Directory.

<!-- end list -->

  - **федеративный общий доступ**  
    Группа функций Exchange, позволяющая отношению доверия с системой проверки подлинности Azure Active Directory работать в различных организациях Exchange, включая нелокальное развертывание Exchange. Совокупность таких функций применяется для создания проверенных на подлинность запросов между серверами от имени пользователей по нескольким организациям Exchange.

<!-- end list -->

  - **федеративный домен**  
    Обслуживаемый уполномоченный домен, который добавляется к идентификатору организации (OrgID) для организации Exchange.

<!-- end list -->

  - **строка шифрования для подтверждения права собственности на домен**  
    Криптографически стойкая строка, используемая организацией Exchange для доказательства того, что данная организация владеет доменом, используемым с системой проверки подлинности Azure Active Directory. Эта строка создается автоматически при использовании мастера **включения доверия федерации**. Также ее можно создать с помощью командлета **Get-FederatedDomainProof**.

<!-- end list -->

  - **политика федеративного общего доступа**  
    Политика на уровне организации, согласно которой выполняется включение устанавливаемого пользователями прямого обмена между сотрудниками данными календаря, а также управление этим процессом.

<!-- end list -->

  - **федерация**  
    Соглашение на основе доверия между двумя организациями Exchange для достижения общей цели. При наличии федерации для каждой организации необходимо, чтобы утверждения проверки подлинности от одной организации распознавались другой организацией.

<!-- end list -->

  - **доверие федерации**  
    Связь с системой проверки подлинности Azure Active Directory, которая определяет следующие компоненты для организации Exchange:
    
      - пространство имен учетных записей;
    
      - идентификатор приложения (AppID);
    
      - идентификатор организации (OrgID);
    
      - федеративные домены.
    
    Для настройки федеративного общего доступа с другими федеративными организациями Exchange, следует создать отношение доверия федерации с системой проверки подлинности Azure Active Directory.

<!-- end list -->

  - **нефедеративная организация**  
    Организация, которая не имеет доверия федерации, установленного с системой проверки подлинности Azure Active Directory.

<!-- end list -->

  - **идентификатор организации (OrgID)**  
    Определяет, какие из уполномоченных обслуживаемых доменов, настроенных в организации, включены для федерации. Система проверки подлинности Azure Active Directory распознает только тех получателей, которые имеют адреса электронной почты с федеративными доменами, настроенными в идентификаторе организации, и только они могут использовать такие функции, как федеративный общий доступ. OrgID — это сочетание заданной заранее строки и первого обслуживаемого домена, выбранного для федерации в мастере **включения доверия федерации**. Например, если вы указали федеративный домен contoso.com как основной SMTP-домен своей организации, в качестве OrgID для доверия федерации будет автоматически создано пространство имен учетных записей FYDIBOHF25SPDLT.contoso.com.

<!-- end list -->

  - **связь организации**  
    Отношение "один к одному" между двумя федеративными организациями Exchange, которое позволяет получателям обмениваться сведениями о доступности (доступности календаря). Связь организации требует доверия федерации с системой проверки подлинности Azure Active Directory и устраняет необходимость в использовании леса Active Directory или доверия федерации между организациями Exchange.

<!-- end list -->

  - **Azure Active Directory система проверки подлинности**  
    Бесплатная облачная служба идентификации, действующая в качестве брокера отношений доверия между федеративными организациями Microsoft Exchange. Он отвечает за выдачу маркеров делегирования получателям Exchange, когда они запрашивают информацию от получателей в других федеративных организациях Exchange. Дополнительные сведения см. в статье [Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500).

## Система проверки подлинности Azure AD

Система проверки подлинности Azure Active Directory — это бесплатная облачная служба, предоставляемая корпорацией Майкрософт, которая действует как брокер доверия между вашей локальной организацией Exchange 2013 и другими федеративными организациями Exchange 2010 и Exchange 2013. Для настройки федеративного делегирования в организации Exchange необходимо установить единовременное доверие федерации с системой проверки подлинности Azure Active Directory, что позволит ему стать партнером по федерации для организации. Это доверие позволяет пользователям, прошедшим проверку подлинности в службе каталогов Active Directory (*поставщики удостоверений*), получать маркеры делегирования SAML (Security Assertion Markup Language) с помощью системы проверки подлинности Azure AD. Эти маркеры дают пользователям из одной федеративной организации Exchange возможность получать доверие от другой такой организации Exchange. Когда система проверки подлинности Azure AD выступает в качестве брокера доверия, для организаций не требуется устанавливать несколько отдельных отношений доверия с другими организациями и пользователи могут получать доступ к внешним ресурсам с помощью функции единого входа (SSO). Дополнительные сведения см. в статье [Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500).

Основные термины

## Доверие федерации

Для настройки федеративного общего доступа Exchange 2013 следует создать отношение доверия федерации вашей организации Exchange 2013 с системой проверки подлинности Azure AD. Создание отношения доверия федерации с системой проверки подлинности Azure AD обеспечивает обмен цифровыми сертификатами безопасности организации с системой проверки подлинности Azure AD и получение сертификата системы проверки подлинности Azure AD и метаданных федерации. Доверие федерации можно установить с помощью мастера **создания доверия федерации** в центре администрирования Exchange (EAC) или командлета **New-FederationTrust** в командной консоли Exchange. Мастер **создания доверия федерации** автоматически создает самозаверяющий сертификат, который используется для подписывания и шифрования маркеров системы проверки подлинности Azure AD, позволяющих внешним федеративным организациям доверять вашим пользователям. Дополнительные сведения о требованиях к сертификатам см. в подразделе Требования к сертификатам для федерации далее в этом разделе.

При создании доверия федерации с системой проверки подлинности Azure AD автоматически создается *идентификатор приложения* (AppID) для вашей организации Exchange, который приводится в выходных данных командлета **Get-FederationTrust**. Идентификатор AppID используется системой проверки подлинности Azure AD для уникальной идентификации организации Exchange. Он также используется организацией Exchange для подтверждения прав владения доменом, используемым для системы проверки подлинности Azure AD. Это достигается путем создания записи ресурса TXT в зоне DNS каждого федеративного домена.

Основные термины

## Идентификатор федеративной организации

*Идентификатор федеративной организации* (OrgID) определяет, какой из уполномоченных обслуживаемых доменов, настроенных в организации, включен для федерации. Система проверки подлинности Azure AD распознает только тех получателей, которые имеют адреса электронной почты с принятыми доменами, настроенными в идентификаторе организации, и только они могут использовать такие функции, как федеративный общий доступ. При создании нового доверия федерации с помощью системы проверки подлинности Azure AD автоматически создается идентификатор OrgID. OrgID — это сочетание заданной заранее строки и обслуживаемого домена, выбранного в качестве основного общего домена в мастере включения доверия федерации. Например, если вы указали в мастере изменения общих доменов федеративный домен **contoso.com** как основной общий домен своей организации, в качестве OrgID для доверия федерации вашей организации Exchange будет автоматически создано пространство имен учетных записей **FYDIBOHF25SPDLT.contoso.com**.

Хотя обычно это основной SMTP-домен организации Exchange, он не обязательно должен быть обслуживаемым и не требует записи типа TXT. (Эта запись подтверждает владение и настраивается в службе доменных имен, или DNS.) Единственное требование заключается в том, что длина имен обслуживаемых доменов, выбранных для федерации, не должна превышать 32 символов. Указанный поддомен служит только в качестве федеративного пространства имен для системы аутентификации Azure AD. Он обслуживает уникальные идентификаторы для получателей, запрашивающих маркеры делегирования SAML. Дополнительные сведения о маркерах SAML см. в статье [Маркеры и утверждения SAML](https://go.microsoft.com/fwlink/?linkid=198561).

Вы можете добавлять и удалять обслуживаемые домены в доверии федерации в любое время. Чтобы включить или выключить все функции федеративного общего доступа в организации, достаточно включить или выключить OrgID для доверия федерации.

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876857.important(EXCHG.150).gif" title="Важно" alt="Важно" />Важно!</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>При изменении OrgID, обслуживаемых доменов или AppID, используемых для доверия федерации затрагиваются все функции федеративного общего доступа в вашей федерации. Изменения также затрагивают внешние федеративные организации Exchange, включая Exchange Online и гибридные развертывания. Рекомендуется уведомлять всех внешних федеративных партнеров о всех изменениях в параметрах конфигурации доверия федерации.</td>
</tr>
</tbody>
</table>


Основные термины

## Пример федерации

Две организации Exchange, Contoso, Ltd. и Fabrikam, Inc., хотят, чтобы их пользователи могли обмениваться сведениями о доступности из календарей. В каждой организации создано доверие федерации с системой проверки подлинности Azure AD и настроено пространство имен учетных записей, включающее в себя домен адресов электронной почты пользователей.

Сотрудники Contoso используют один из следующих доменов адресов электронной почты: contoso.com, contoso.co.uk или contoso.ca. Сотрудники компании Fabrikam используют один из следующих доменов адресов электронной почты: fabrikam.com, fabrikam.org или fabrikam.net. В обеих организациях все обслуживаемые домены электронной почты включены в пространство имен учетных записей для создания доверия федерации с системой проверки подлинности Azure AD. Вместо настройки сложного леса Active Directory или доверия доменов организации создают между собой связь организаций для обмена сведениями о доступности.

На следующем рисунке показана конфигурация федерации между компаниями Contoso, Ltd. и Fabrikam, Inc.

**Пример федеративного общего доступа**

![Доверие федерации и федеративный доступ](images/Dd335047.310f0698-b67d-4b0e-91e4-231c6e9db952(EXCHG.150).gif "Доверие федерации и федеративный доступ")

## Требования к сертификатам для федерации

Чтобы установить доверие федерации с системой проверки подлинности Azure AD, необходимо создать самозаверяющий сертификат или сертификат X.509, подписанный центром сертификации, и установить его на сервере Exchange 2013, использованном для создания доверия. Настоятельно рекомендуется использовать самозаверяющий сертификат, автоматически создаваемый и устанавливаемый мастером **включения доверия федерации** в EAC. Он используется только для подписывания и шифрования маркеров делегирования, используемый при федеративном общем доступе. Для доверия федерации достаточно одного сертификата. Exchange 2013 автоматически распространяет сертификат на всех прочих серверах Exchange 2013 в организации.

Для использования сертификата X.509, подписанного внешним центром сертификации, он должен отвечать следующим требованиям.

  - **Доверенный центр сертификации**. По возможности сертификат SSL X.509 должен быть выдан центром сертификации, доверенным для службы Windows Live. Тем не менее, можно использовать сертификаты, выданные центрами сертификации, которые в настоящее время не сертифицированы корпорацией Майкрософт. Текущий список доверенных центров сертификации см. в разделе [Доверенные корневые центры сертификации для доверия федерации](trusted-root-certification-authorities-for-federation-trusts-exchange-2013-help.md).

  - **Идентификатор ключа субъекта**. В сертификате должно быть поле идентификатора ключа субъекта. Большинство сертификатов X.509, выпускаемых коммерческими центрами сертификации, имеют такой идентификатор.

  - **Поставщик служб шифрования CryptoAPI**. Для сертификата должен использоваться поставщик CryptoAPI. Сертификаты, для которых используются поставщики CNG (Cryptography API: Next Generation), не поддерживаются в случае применения федерации. Если запрос на получение сертификата создается с помощью Exchange, то используется поставщик CryptoAPI. Дополнительные сведения см. в статье [Cryptography API: Next Generation](https://go.microsoft.com/fwlink/?linkid=187890).

  - **Алгоритм подписи RSA**   В качестве алгоритма подписи в сертификате должен использоваться алгоритм RSA.

  - **Экспортируемый закрытый ключ**   Закрытый ключ, используемый для создания сертификата, должен быть экспортируемым. При создании запроса на сертификат с помощью мастера **создания сертификатов Exchange** в центре администрирования Exchange или командлета [New-ExchangeCertificate](https://technet.microsoft.com/ru-ru/library/aa998327\(v=exchg.150\)) в командной консоли можно указать, что закрытый ключ сертификата должен быть экспортируемым.

  - **Текущий сертификат**   Сертификат должен быть действителен. Невозможно использовать истекший или аннулированный сертификат для создания доверия федерации.

  - **Расширенное использование ключа**   В сертификат должен быть включен тип расширенного использования ключа (EKU) **Проверка подлинности клиента (1.3.6.1.5.5.7.3.2)**. Этот тип использования предназначен для подтверждения идентификатора на удаленном компьютере. Если для создания запроса на сертификат используется EAC или командная консоль, то этот тип использования включается по умолчанию.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ126620.note(EXCHG.150).gif" title="Примечание" alt="Примечание" />Примечание.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Так как данный сертификат не используется для проверки подлинности, то для него отсутствуют требования к имени субъекта или альтернативному имени субъекта. Можно использовать сертификат с именем субъекта, которое совпадает с именем узла, доменным или любым другим именем.</td>
</tr>
</tbody>
</table>


Основные термины

## Переход на новый сертификат

Сертификат, используемый для создания доверия федерации, обозначается в качестве текущего. Однако для доверия федерации может потребоваться периодическая установка и использование нового сертификата. Например, новый сертификат может потребоваться, когда истекает срок действия текущего сертификата или необходимо выполнение требований к ведению бизнеса или обеспечению безопасности. Чтобы обеспечить плавное переключение на новый сертификат, необходимо установить его на сервер Exchange 2013 и настроить доверие федерации для обозначения этого сертификата в качестве нового. Exchange 2013 автоматически распространяет следующий сертификат на другие серверы Exchange 2013 в организации. В зависимости от топологии Active Directory, распространение сертификата может занять некоторое время. Проверить состояние сертификата можно с помощью командлета [Test-FederationTrustCertificate](https://technet.microsoft.com/ru-ru/library/dd335228\(v=exchg.150\)) в командной консоли.

После проверки состояния распространения сертификата можно настроить доверие для переключения на следующий сертификат. Когда это произойдет, текущий сертификат будет обозначен как предыдущий, а новый — как текущий. Новый сертификат публикуется в системе проверки подлинности Azure AD, а все новые маркеры, которыми выполнен обмен с системой проверки подлинности Azure AD, шифруются с помощью нового сертификата.

<table>
<thead>
<tr class="header">
<th><img src="images/JJ126620.note(EXCHG.150).gif" title="Примечание" alt="Примечание" />Примечание.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Этот процесс перехода на новый сертификат используется только в федерации. Если этот же сертификат используется в других компонентах Exchange 2013, применяющих сертификаты, необходимо учитывать требования этих компонентов при планировании получения и установки нового сертификата, а также перехода на новый сертификат.</td>
</tr>
</tbody>
</table>


Основные термины

## Рекомендации относительно брандмауэра для федерации

Чтобы использовать функции федерации, необходимо настроить для серверов почтовых ящиков и клиентского доступа в организации доступ к Интернету по протоколу HTTPS. Необходимо разрешить доступ по протоколу HTTPS (порт 443 для TCP) для всех серверов почтовых ящиков и клиентского доступа Exchange 2013 в организации.

Чтобы разрешить внешней организации получать доступ к сведениям о доступности пользователей вашей организации, необходимо опубликовать один сервер клиентского доступа в Интернете. Для этого требуется настройка для сервера клиентского доступа исходящего доступа в Интернет с помощью протокола HTTPS. Серверы клиентского доступа на сайтах Active Directory, на которых не опубликован сервер клиентского доступа в Интернете, могут использовать серверы клиентского доступа на других сайтах Active Directory, которые доступны в Интернете. Серверы клиентского доступа, которые не опубликованы в Интернете, должны иметь внешний URL-адрес виртуального каталога веб-служб, настроенного с помощью URL-адреса, отображаемого для внешних организаций.

[В начало](sharing-exchange-2013-help.md)
