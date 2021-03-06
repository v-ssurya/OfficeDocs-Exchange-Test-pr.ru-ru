﻿---
title: 'Управление фильтрацией получателей на пограничных транспортных серверах: Exchange 2013 Help'
TOCTitle: Управление фильтрацией получателей на пограничных транспортных серверах
ms:assetid: f2d0041f-2872-4669-95ec-443233f4956d
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb125187(v=EXCHG.150)
ms:contentKeyID: 50489500
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Управление фильтрацией получателей на пограничных транспортных серверах

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2015-04-08_

Фильтрация получателей обеспечивается агентом фильтра получателей. Когда на сервере Exchange включена фильтрация получателей, она фильтрует входящие сообщения из Интернета, проверка подлинности которых не проведена. Такие сообщения обрабатываются как внешние сообщения.

> [!NOTE]  
> Хотя агент фильтра получателей доступен на серверах почтовых ящиков, его не следует настраивать. Если при фильтрации получателей на сервере почтовых ящиков обнаружен один недопустимый или заблокированный получатель в сообщении, содержащем других допустимых получателей, сообщение отклоняется. При установке агентов защиты от нежелательной почты на сервере почтовых ящиков агент фильтра получателей активируется по умолчанию. Однако он не настраивается на блокировку получателей. Дополнительные сведения см. в разделе <a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">Включение функции защиты от нежелательной почты на сервере почтовых ящиков</a>.


## Что нужно знать перед началом работы

  - Предполагаемое время для завершения каждой процедуры: 5 минут

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись «Функции защиты от нежелательной почты» в разделе [Разрешения для защиты от нежелательной почты и вредоносных программ](anti-spam-and-anti-malware-permissions-exchange-2013-help.md).

  - Для выполнения этой процедуры можно использовать только командную консоль.

  - По умолчанию функции защиты от нежелательной почты в транспортной службе на сервере почтовых ящиков не включены. Как правило, функции защиты от нежелательной почты на сервере почтовых ящиков включают, только если организация Exchange не выполняет никакую предварительную фильтрацию нежелательной почты до приема входящих сообщений. Дополнительную информацию см. в статье [Включение функции защиты от нежелательной почты на сервере почтовых ящиков](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

  - Параметр *AddressBookEnabled* командлета **Set-AcceptedDomain** позволяет включить или отключить фильтрацию получателей для получателей в обслуживаемом домене. По умолчанию фильтрация получателей включена для уполномоченных доменов и отключена для доменов внутренней и внешней ретрансляции. Чтобы просмотреть состояние параметра *AddressBookEnabled* для обслуживаемых доменов в своей организации, выполните следующую команду.
    
        Get-AcceptedDomain | Format-List Name,AddressBookEnabled

  - Если отключить фильтрацию получателей с помощью описанной в данном разделе процедуры, функция фильтрации получателей будет отключена, но соответствующий агент фильтра получателей будет оставаться включенным.

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Что необходимо сделать?

## Использование командной консоли для включения и отключения фильтрации получателей

Чтобы отключить фильтрацию получателей, выполните следующую команду:

    Set-RecipientFilterConfig -Enabled $false

Чтобы включить фильтрацию получателей, выполните следующую команду:

    Set-RecipientFilterConfig -Enabled $true

> [!NOTE]  
> В случае отключения фильтрации получателей соответствующий агент фильтра получателей будет оставаться включенным. Чтобы выключить агент фильтра получателей, выполните следующую команду. <code>Disable-TransportAgent &quot;Recipient Filter Agent&quot;</code>.


## Как проверить, что все получилось?

Чтобы убедиться в успешном включении или выключении фильтрации получателей, выполните указанное ниже.

1.  Выполните следующую команду:
    
        Get-RecipientFilterConfig | Format-List Enabled

2.  Убедитесь, что отображается значение, которое вы настроили.

## Использование командной консоли для включения или отключения списка заблокированных получателей

Выполните следующую команду:

    Set-RecipientFilterConfig -BlockListEnabled <$true | $false>

В этом примере демонстрируется, как включить список заблокированных получателей.

    Set-RecipientFilterConfig -BlockListEnabled $true

## Как проверить, что все получилось?

Чтобы убедиться в успешном включении или выключении списка заблокированных получателей, выполните указанное ниже.

1.  Выполните следующую команду:
    
        Get-RecipientFilterConfig | Format-List BlockListEnabled

2.  Убедитесь, что отображается значение, которое вы настроили.

## Использование командной консоли для настройки списка заблокированных получателей

Чтобы заменить существующие значения, выполните следующую команду:

    Set-RecipientFilterConfig -BlockedRecipients <recipient1,recipient2...>

В этом примере демонстрируется настройка списка заблокированных получателей для valuesmark@contoso.com и kim@contoso.com.

    Set-RecipientFilterConfig -BlockedRecipients mark@contoso.com,kim@contoso.com

Чтобы добавить или удалить записи, не изменив существующие значения, выполните следующую команду:

    Set-RecipientFilterConfig -BlockedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...}

В данном примере адрес chris@contoso.com добавляется в список получателей, а адрес michelle@contoso.com удаляется из списка получателей в списке заблокированных получателей.

    Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"; Remove="michelle@contoso.com"}

## Как проверить, что все получилось?

Чтобы убедиться в успешной настройке списка заблокированных получателей, выполните указанное ниже.

1.  Выполните следующую команду:
    
        Get-RecipientFilterConfig | Format-List BlockedRecipients

2.  Убедитесь, что отображаются значения, которые вы настроили.

## Использование командной консоли для включения и отключения поиска получателей

Выполните следующую команду:

    Set-RecipientFilterConfig -RecipientValidationEnabled <$true | $false>

Чтобы заблокировать сообщения получателям, не существующим в организации, выполните следующую команду:

    Set-RecipientFilterConfig -RecipientValidationEnabled $true

## Как проверить, что все получилось?

Чтобы убедиться в успешном включении или выключении поиске получателей, выполните указанное ниже.

1.  Выполните следующую команду:
    
        Get-RecipientFilterConfig | Format-List RecipientValidationEnabled

2.  Убедитесь, что отображается значение, которое вы настроили.

