﻿---
title: 'Включить предварительный просмотр голосовой почты для пользователей: Exchange 2013 Help'
TOCTitle: Включить предварительный просмотр голосовой почты для пользователей
ms:assetid: 206a5d2b-27c9-4e9b-a29a-6ddffaa07109
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ673514(v=EXCHG.150)
ms:contentKeyID: 51408011
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Включить предварительный просмотр голосовой почты для пользователей

 

_**Применимо к:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:** 2013-02-21_

Вы можете включить функцию просмотра голосовой почты для пользователей, связанных с политикой почтовых ящиков единой системы обмена сообщениями, если эта функция была отключена. Включение данного параметра позволяет пользователям получать текст голосового сообщения в тексте сообщения электронной почты или текстовом сообщении. По умолчанию параметр включен.

Дополнительные сведения об управленческих задачах, связанных с политиками почтовых ящиков единой системы обмена сообщениями, см. в разделе [Процедуры политики почтовых ящиков единой системы обмена СООБЩЕНИЯМИ](um-mailbox-policy-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: менее 1 минуты.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись «Политики почтовых ящиков единой системы обмена сообщениями» в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что абонентская группа единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание абонентской группы единой системы обмена сообщениями](create-a-um-dial-plan-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что политика почтовых ящиков единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание политики почтовых ящиков единой системы обмена сообщениями](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Что необходимо сделать?

## Включение просмотра голосовой почты с помощью Центра администрирования Exchange

1.  В Центре администрирования Exchange выберите **Единая система обмена сообщениями** \> **Абонентские группы единой системы обмена сообщениями**, выберите абонентскую группу, которую нужно изменить, и нажмите **Изменить**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

2.  На странице **Абонентская группа единой системы обмена сообщениями** в разделе **Политики почтовых ящиков единой системы обмена сообщениями** выберите необходимую политику почтовых ящиков этой системы, а затем нажмите кнопку **Изменить**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

3.  На странице **Политика почтовых ящиков единой системы обмена сообщениями** \> **Общие** установите флажок **Разрешить просмотр голосовой почты**.

4.  Нажмите кнопку **Сохранить**.

## Включение просмотра голосовой почты с помощью командной консоли

В этом примере показано, как разрешить пользователям, связанным с политикой почтовых ящиков единой системы обмена сообщениями `MyUMMailboxPolicy`, использовать функцию просмотра голосовой почты.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy - AllowVoiceMailPreview $true

