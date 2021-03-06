﻿---
title: 'Отключение автосекретаря единой системы обмена СООБЩЕНИЯМИ: Exchange 2013 Help'
TOCTitle: Отключение автосекретаря единой системы обмена СООБЩЕНИЯМИ
ms:assetid: ad79f374-f68f-430b-8b9c-2c841e1c55ae
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb124228(v=EXCHG.150)
ms:contentKeyID: 50488839
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Отключение автосекретаря единой системы обмена СООБЩЕНИЯМИ

 

_**Применимо к:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:** 2012-11-05_

По умолчанию при создании автосекретаря единой системы обмена сообщениями для него устанавливается состояние "выключен". После создания автосекретаря единой системы обмена сообщениями можно изменить его состояние, чтобы управлять его ответом на входящие вызовы. Например, может потребоваться отключить автоматического секретаря единой системы обмена сообщениями при записи или повторной записи пользовательских запросов и сообщений.

Дополнительные задачи управления, связанные с автосекретарями единой системы обмена сообщениями, см. в разделе [Процедуры автосекретаря единой системы обмена сообщениями](um-auto-attendant-procedures-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения: менее 1 минуты.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись «Автосекретари единой системы обмена сообщениями» в разделе [Разрешения единой системы обмена сообщениями](unified-messaging-permissions-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что абонентская группа единой системы обмена сообщениями создана. Дополнительные сведения см. в разделе [Создание абонентской группы единой системы обмена сообщениями](create-a-um-dial-plan-exchange-2013-help.md).

  - Перед выполнением этих процедур убедитесь, что автосекретарь единой системы обмена сообщениями создан. Дополнительные сведения см. в разделе [Создание автосекретаря единой системы обмена сообщениями](create-a-um-auto-attendant-exchange-2013-help.md). Также убедитесь, что состояние автосекретаря единой системы обмена сообщениями задано как «включен».

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Что необходимо сделать?

## Использование центра администрирования Exchange для отключения автосекретаря единой системы обмена сообщениями

1.  В Центре администрирования Exchange последовательно выберите пункты **Единая система обмена сообщениями** \> **Абонентские группы единой системы обмена сообщениями**. В представлении списка выберите абонентскую группу единой системы обмена сообщениями, которую необходимо изменить, и нажмите на панели инструментов кнопку **Редактировать**![Значок редактирования](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Значок редактирования").

2.  На странице **Абонентская группа единой системы обмена сообщениями** в разделе **Автосекретари единой системы обмена сообщениями** выберите автосекретарь единой системы обмена сообщениями, который нужно отключить. На панели инструментов, нажмите клавишу **СТРЕЛКА ВНИЗ**![Значок "Стрелка вниз"](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Значок \"Стрелка вниз\"")

3.  На странице **Предупреждение** нажмите кнопку **Да**.

## Использование командной консоли для отключения автосекретаря единой системы обмена сообщениями

В этом примере показано отключение автосекретаря единой системы обмена сообщениями под названием `MyUMAutoAttendant`.

    Disable-UMAutoAttendant -Identity MyUMAutoAttendant

