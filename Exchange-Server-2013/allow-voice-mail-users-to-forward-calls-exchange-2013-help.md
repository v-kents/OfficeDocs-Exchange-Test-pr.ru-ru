﻿---
title: 'Включение переадресации вызовов для пользователей голосовой почты: Exchange 2013 Help'
TOCTitle: Включение переадресации вызовов для пользователей голосовой почты
ms:assetid: 1f8e0a53-3d9d-4f8c-9be3-9f1e2a4347a3
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dd335138(v=EXCHG.150)
ms:contentKeyID: 50556352
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Включение переадресации вызовов для пользователей голосовой почты

 

_**Применимо к:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:**2013-02-22_

Функция правил автоответчика была впервые введена в Exchange 2010. С помощью данной функции пользователи, для которых включена голосовая почта, могут управлять обработкой своих входящих вызовов. Способ, которым правила автоответчика применяются ко входящим вызовам, аналогичен способу, которым правила для папки "Входящие" применяются к входящим сообщениям электронной почты.

Правила автоответчика создаются и настраиваются пользователем с включенной поддержкой голосовой почты с помощью приложения Outlook или Outlook Web App. Правила хранятся вместе с другими настройками голоса в почтовом ящике пользователя. Для каждого почтового ящика с включенной поддержкой единой системы обмена сообщениями можно настроить до девяти правил автоответчика. Эти правила не зависят от правил для папки "Входящие", которые настраиваются пользователями, и не оказывают влияния на расход определенной для пользователя квоты для правил второго типа.

По умолчанию, когда для пользователя включены единая система обмена сообщениями и голосовая почта, правила автоответчика не настраиваются. Если на входящий вызов отвечает система голосовой почты, то вызывающей стороне будет предложено оставить голосовое сообщение. Даже если такой запрос не поступает, эта возможность в любом случае остается.

Если система голосовой почты необходима только для ответов на входящие вызовы и записи голосовых сообщений, правила автоответчика создавать не требуется. Однако если необходимо установить условия или действия, это можно сделать в разделе **Правила автоответчика** на вкладке **Голосовая почта** в приложении Outlook Web App. В разделе **Правила автоответчика** можно создавать, изменять и удалять правила автоответчика.

## Структура правил автоответчика

Правила автоответчика состоят из двух частей: условий и действий. C одним правилом автоответчика можно связать одно или несколько условий. Правило автоответчика обрабатывается только при соблюдении всех условий правила. C одним правилом автоответчика также можно связать одно или несколько действий. Они определяют варианты действий, предлагаемых абонентам при обработке правила автоответчика.

Правила автоответчика поддерживают следующие условия:

  - входящий вызов от

  - время суток

  - сведения календаря о занятости

  - включение и выключение автоматических ответов для электронной почты

Поддерживаются следующие действия:

  - найти меня

  - перенаправить абонента другому пользователю

  - оставить голосовое сообщение

Если для правила автоответчика записано пользовательское приветствие, то при настройке правила в приветствие необходимо включить меню. В противном случае единая система обмена сообщениями не создаст приглашение меню, которое позволяет абоненту выбрать действие. После воспроизведения настраиваемого приветствия сервер будет ожидать ввода варианта абонентом. Если параметр меню не будет включен в приветствие, абонент не сможет выполнить ввод и сервер создаст приглашение с вопросом "Вы на линии?".

## Условия

Условия — это правила, которые можно применить к правилу автоответчика. С помощью сочетания условий можно создать несколько правил автоответчика, которые будут активироваться при выполнении условий. Чтобы создать правило по умолчанию, которое будет применяться к каждому вызову, необходимо создать правило без условий.

Существует три условия, которые можно использовать при установке правил автоответчика. К ним относятся следующие:

  - Идентификатор звонящего

  - время дня

  - сведения о занятости

## Действия

Действия используются, чтобы определить действия, которые должны выполняться при соблюдении условий. Существует два вида действий:

  - Найти меня

  - перевод вызова

**добавление действия "Найти меня"**

Если абонент выбирает действие "Найти меня", система голосовой почты пытается найти вас по двум другим номерам телефона и соединить с ним, если вы ответили.

  - Можно указать текст, который будет читаться вызывающему абоненту. Например, если ввести «Срочный вопрос», чтобы сообщить вызывающим абонентам о необходимости выбрать это действие для обсуждения с пользователем срочного вопроса, система голосовой почты сообщит «По срочному вопросу нажмите клавишу 1».

  - Необходимо связать действие "Найти меня" с цифрой, которую нажимает абонент для выбора данного действия на клавиатуре телефона. В приведенном выше примере клавиша телефона **1** обозначает цифру, который будут нажимать абоненты, чтобы связаться с вами по одному или нескольким указанным телефонным номерам.

  - Далее следует указать 1 или 2 номера телефона, по которым будет звонить система голосовой почты. Если указаны два телефонных номера, второй номер будет набираться, если пользователь недоступен по первому. Каждый указанный телефонный номер связан с длительностью. Длительность — это период времени, в течение которого система голосовой почты будет набирать первый номер телефона перед переходом на следующий номер. Если с пользователем не удалось связаться, система голосовой почты вернется назад к меню параметров.

  - После ввода этих данных нажмите кнопку **Применить**, чтобы сохранить параметры действия "Найти меня".

**Добавление действий по переводу вызова**

После настройки действия «Перевод вызова» абонентам будет предлагаться вариант перевода вызова на другой телефонный номер пользователя. Существует несколько параметров, которые можно настроить для передачи входящего вызова на другой телефон или контакт.

  - Можно указать текст, который будет читаться вызывающему абоненту. Например, если ввести «Важные дела», чтобы сообщить вызывающим абонентам о необходимости выбрать это действие для обсуждения важных дел и необходимости поговорить с кем-либо.

  - Необходимо связать действие **Перевод вызова** с цифрой, которую нажимает абонент для выбора данного действия на клавиатуре телефона.

  - После выбора действия «Перевод вызова» необходимо указать контакт или номер телефона, на который будет переводиться вызов. Можно выбрать номер телефона или контакт, на который поступит вызов при нажатии абонентом соответствующей клавиши на клавиатуре телефона. При указании контакта из справочника компании система голосовой почты будет пытаться передать вызов на добавочный номер контакта.

  - Кроме выбора контакта или номера для перевода вызова, также необходимо указать цифру на клавиатуре телефона, которую должен нажать абонент для выбора действия "Перевод вызова".

  - После ввода этих данных нажмите кнопку **Применить**, чтобы сохранить параметры действия «Перевод вызова».

## Выбор правила автоответчика для каждого входящего вызова

После создания и настройки правил ответа на вызовы единая система обмена сообщениями выполняет следующие действия.

1.  Определяет, созданы ли правила автоответчика. Если нет, единая система обмена сообщениями предложит абоненту оставить голосовое сообщение.

2.  Если настроено одно или несколько правил, единая система обмена сообщениями выполнит оценку каждого правила. Обрабатываться будет первое правило, условия которого будут выполнены.

3.  Если после оценки всех правил единая система обмена сообщениями не найдет правило с выполненными условиями, она предложит абоненту оставить голосовое сообщение.

## правил набора номера

В зависимости от настройки правил автоответчика входящий вызов может быть переведен другому пользователю. В таком случае к номеру телефона, на который выполняется переадресация, применяются правила и ограничения набора номера политики почтовых ящиков единой системы обмена сообщениями, с которой сопоставлена вызываемая сторона. Дополнительные сведения о правилах исходящих звонков и набора номера, а также об ограничениях см. в разделе [Разрешить пользователям совершать звонки](allow-users-to-make-calls-exchange-2013-help.md).

## Включение и отключение правил автоответчика

По умолчанию для пользователей единой системы обмена сообщениями правила автоответчика включены автоматически. Однако их можно отключить, выключив эту функцию в политике почтовых ящиков единой системы обмена сообщениями или почтовом ящике пользователя. Дополнительные сведения о включении и отключении правил автоответчика см. в приведенных ниже разделах.

  - [Разрешить или запретить пользователям в одной политики почтовых ящиков единой системы обмена СООБЩЕНИЯМИ создавать правила ответа на звонок](allow-or-prevent-users-in-the-same-um-mailbox-policy-from-creating-call-answering-rules-exchange-2013-help.md)

  - [Возможность разрешить или запретить пользователю создавать правила автоответчика](allow-or-prevent-a-user-from-creating-call-answering-rules-exchange-2013-help.md)
