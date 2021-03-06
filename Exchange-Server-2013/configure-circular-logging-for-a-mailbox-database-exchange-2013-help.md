﻿---
title: 'Настройка циклического ведения журнала для базы данных почтовых ящиков: Exchange 2013 Help'
TOCTitle: Настройка циклического ведения журнала для базы данных почтовых ящиков
ms:assetid: 29cbd7cd-382b-4e0d-8368-2e49e75df2fc
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dn756374(v=EXCHG.150)
ms:contentKeyID: 62524847
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Настройка циклического ведения журнала для базы данных почтовых ящиков

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2014-06-24_

При включении циклического ведения журнала для базы данных почтовых ящиков его тип зависит от того, выполняется ли непрерывная репликация этой базы данных или нет.

  - Если база данных почтовых ящиков не реплицируется, будет использоваться циклическое ведение журнала JET. В таком случае для активации (или дезактивации) циклического ведения журнала JET нужно будет отключить, а затем повторно подключить базу данных.

  - Если база данных почтовых ящиков реплицируется, будет использоваться циклическое ведение журнала при непрерывной репликации (CRCL). В этом случае активация или дезактивация CRCL выполняется динамически и нет необходимости отключать и повторно подключать базу данных.

Дополнительные сведения о циклическом ведении журнала и CRCL см. в статье [Exchange Native Data Protection](backup-restore-and-disaster-recovery-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: 1 минута

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись "Разрешения базы данных почтовых ящиков" в разделе [Разрешения получателей](recipients-permissions-exchange-2013-help.md).

## Настройка циклического ведения журнала для базы данных с помощью Центра администрирования Exchange

1.  В Центре администрирования Exchange последовательно выберите пункты **Серверы** \> **Базы данных**.

2.  Выберите базу данных почтовых ящиков, которую необходимо настроить, и выберите команду ![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

3.  Установите или снимите флажок **Включить циклическое ведение журнала** и нажмите кнопку **Сохранить**.

4.  Если необходимо выполнить операцию по отключению и подключению, появится предупреждающее сообщение. Нажмите кнопку **ОК**, чтобы закрыть окно предупреждающего сообщения.
    
    1.  Чтобы отключить базу данных, нажмите **Дополнительно**![Значок дополнительных параметров](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Значок дополнительных параметров") и выберите пункт **Отключить**. Нажмите **Да**, когда появится предупреждающее сообщение.
    
    2.  Чтобы подключить базу данных, нажмите **Дополнительно**![Значок дополнительных параметров](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Значок дополнительных параметров") и выберите пункт **Подключить**. Нажмите **Да**, когда появится предупреждающее сообщение.

## Настройка циклического ведения журнала для базы данных с помощью командной консоли

В этом примере включается циклическое ведение журнала для базы данных DB1.

    Set-MailboxDatabase DB1 -CircularLoggingEnabled $True

В этом примере выключается циклическое ведение журнала для базы данных DB1.

    Set-MailboxDatabase DB1 -CircularLoggingEnabled $False

Сведения о других параметрах базы данных почтовых ящиков, которые можно настроить, см. в разделе [Set-MailboxDatabase](https://technet.microsoft.com/ru-ru/library/bb123971\(v=exchg.150\)).

