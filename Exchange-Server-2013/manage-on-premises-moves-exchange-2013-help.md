﻿---
title: 'Управление локальными перемещениями: Exchange 2013 Help'
TOCTitle: Управление локальными перемещениями
ms:assetid: 1691b658-f5af-49c6-9170-5c3cb66c7306
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ150487(v=EXCHG.150)
ms:contentKeyID: 50487517
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Управление локальными перемещениями

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2013-02-25_

Запрос на перемещение — это процесс перемещения почтового ящика из одной базы данных почтовых ящиков в другую. Запрос на локальное перемещение — это перемещение почтового ящика, происходящее в одном лесу. В Microsoft Exchange Server 2013 почтовые ящики и почтовые ящики с личными архивами могут находиться в отдельных базах данных. Используя запрос на перемещение, можно переместить основной почтовый ящик и связанный с ним архив в одну базу данных или в разные. Процедуры, описанные в этом разделе, помогут вам выполнить перемещения локальных почтовых ящиков.

Используйте приведенные ниже процедуры для перемещения почтовых ящиков в локальной организации. В этих процедурах используется командная консоль Exchange и Центр администрирования Exchange.

При использовании запросов на перемещение для перемещения почтовых ящиков, запросы обрабатываются следующими двумя службами.

  - Служба репликации почтовых ящиков Microsoft Exchange

  - Прокси-сервер репликации почтовых ящиков Microsoft Exchange

Дополнительные сведения о сервере репликации почтовых ящиков и прокси-сервере см. в разделе [Дополнительные сведения о прокси-сервере MRS](https://technet.microsoft.com/ru-ru/library/jj156451\(v=exchg.150\)).

Для получения дополнительных сведений о перемещении почтовых ящиков см. раздел [Перемещение почтовых ящиков в Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

## Что нужно знать перед началом работы

  - Предполагаемое время для завершения каждой процедуры: 20 минут.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись "Разрешения на перемещение и миграцию почтовых ящиков" в разделе [Разрешения получателей](recipients-permissions-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>.


## Что необходимо сделать?

## Проверка готовности почтового ящика к перемещению

В этом примере переключатель *WhatIf* используется, чтобы проверить, готов ли почтовый ящик пользователя Tony Smith к перемещению в новую базу данных DB01 и нет ли ошибок в команде. При использовании параметра *WhatIf* система выполняет проверку почтового ящика. Если почтовый ящик не готов к перемещению, возвращается ошибка.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase DB01 -WhatIf

Дополнительные сведения о синтаксисе и параметрах см. в разделах [New-MigrationBatch](https://technet.microsoft.com/ru-ru/library/jj219166\(v=exchg.150\)) и [New-MoveRequest](https://technet.microsoft.com/ru-ru/library/dd351123\(v=exchg.150\)).

## Создание запроса на локальное перемещение

## Использование Центра администрирования Exchange для создания запроса на локальное перемещение

Чтобы создать запрос на локальное перемещение, войдите в Центр администрирования Exchange и выполните следующие действия.

1.  В Центре администрирования Exchange откройте раздел **Получатели** \> **Миграция** и нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления").

2.  В мастере **нового перемещения локальных почтовых ящиков** выберите перемещаемого пользователя, нажмите кнопку **ОК** и затем кнопку **Далее**.

3.  На странице **Конфигурация перемещения** укажите имя нового пакета. Выберите параметры для архивного почтового ящика, а также расположение базы данных почтовых ящиков, и нажмите кнопку **Создать**.

## Использование командной консоли для создания локального запроса на перемещение

Образец создания локального запроса на перемещение приведен в примере 2 из раздела [New-MoveRequest](https://technet.microsoft.com/ru-ru/library/dd351123\(v=exchg.150\)).

## Как проверить, что все получилось?

Чтобы убедиться, что вы успешно завершили миграцию, выполните следующие действия.

  - В Центре администрирования Exchange перейдите к разделу **Получатели** \> **Миграция**

  - Проверьте, успешно ли прошло перемещение, выбрав команду **Состояние всех пакетов** в Центре администрирования Exchange.

  - В консоли выполните следующую команду для извлечения информации о перемещении почтовых ящиков.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Подробнее см. в разделе [Get-MigrationUserStatistics](https://technet.microsoft.com/ru-ru/library/jj218695\(v=exchg.150\)).

## Создание пакетного запроса на перемещение

## Использование Центра администрирования Exchange для создания запроса на перемещение пакетов

Войдите в Центр администрирования Exchange и выполните следующие действия.

1.  В Центре администрирования Exchange откройте раздел **Получатели** \> **Миграция** и нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления").

2.  В мастере **нового перемещения локальных почтовых ящиков** выберите перемещаемых пользователей, нажмите кнопку **ОК** и затем кнопку **Далее**.

3.  На странице **Конфигурация перемещения** укажите имя нового пакета. Выберите параметры для архивного почтового ящика, а также расположение базы данных почтовых ящиков, и нажмите кнопку **Создать**.

> [!WARNING]  
> Убедитесь, что вы не установили предельное количество неправильных элементов свыше 50. Если это так, то при перемещении возможен сбой. Если требуется установить предельное количество неправильных элементов свыше 50, необходимо использовать командную консоль Exchange и установить параметр –<em>AcceptLargeDataLoss</em> со значением TRUE.


## Использование командной консоли для создания запроса на перемещение пакетов

В данном примере создается пакет миграции для локального перемещения, при котором почтовые ящики, указанные в CSV-файле, перемещаются в другую базу данных почтовых ящиков. Этот файл состоит из одного столбца, содержащего адрес электронной почты каждого из перемещаемых почтовых ящиков. Для заголовка этого столбца должно быть назначено имя **EmailAddress**. Пакет миграции в этом примере следует запустить вручную с помощью командлета **Start-MigrationBatch** или Центра администрирования Exchange. Кроме того, запустить пакет миграции автоматически можно с помощью параметра *AutoStart*.

    New-MigrationBatch -Local -Name LocalMove1 -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\LocalMove1.csv")) -TargetDatabases MBXDB2 -TimeZone "Pacific Standard Time"

    Start-MigrationBatch -Identity LocalMove1

Дополнительные сведения о синтаксисе и параметрах см. в разделах [New-MigrationBatch](https://technet.microsoft.com/ru-ru/library/jj219166\(v=exchg.150\)) и [Start-MigrationBatch](https://technet.microsoft.com/ru-ru/library/jj219165\(v=exchg.150\)).

## Как проверить, что все получилось?

Чтобы убедиться, что вы успешно завершили миграцию, выполните следующие действия.

  - Проверьте, успешно ли прошло перемещение, выбрав команду **Состояние всех пакетов** в Центре администрирования Exchange.

  - В консоли выполните следующую команду для извлечения информации о перемещении почтовых ящиков.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Подробнее см. в разделе [Get-MigrationUserStatistics](https://technet.microsoft.com/ru-ru/library/jj218695\(v=exchg.150\)).

## Отображение пакетов миграции

Пример использования командной консоли для отображения пакета миграции см. в примере 2 в разделе [Get-MigrationBatch](https://technet.microsoft.com/ru-ru/library/jj219164\(v=exchg.150\)).

## Перемещение только основного почтового ящика пользователя

## Использование Центра администрирования Exchange для перемещения только основного почтового ящика пользователя

1.  В Центре администрирования Exchange откройте раздел **Получатели** \> **Миграция** и нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления").

2.  В мастере **нового перемещения локальных почтовых ящиков** выберите пользователя, для которого требуется переместить основной почтовый ящик, нажмите кнопку **ОК** и затем кнопку **Далее**.

3.  На странице **Конфигурация перемещения** укажите имя нового пакета. Выберите элемент **Переместить только основной почтовый ящик**, выберите параметры для расположения базы данных почтовых ящиков и нажмите кнопку **Создать**.

## Использование командной консоли для перемещения только основного почтового ящика пользователя

В этом примере перемещается только основной почтовый ящик "Tony Smith" на сервер DB01. Архив не перемещается.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -PrimaryOnly -TargetDatabase "DB01"

Подробные сведения о синтаксисе и параметрах см. в разделе [New-MoveRequest](https://technet.microsoft.com/ru-ru/library/dd351123\(v=exchg.150\)).

## Как проверить, что все получилось?

Чтобы убедиться, что вы успешно завершили миграцию, выполните следующие действия.

  - В Центре администрирования Exchange выберите пункт **Состояние всех пакетов**.

  - В консоли выполните следующую команду для извлечения информации о перемещении почтовых ящиков.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Подробнее см. в разделе [Get-MigrationUserStatistics](https://technet.microsoft.com/ru-ru/library/jj218695\(v=exchg.150\)).

## Создание межлесного перемещения с помощью пакетного CSV-файла

В этом примере настраивается конечная точка миграции, а затем создается межлесное перемещение — из исходного в целевой лес — с помощью CSV-файла.

```
    New-MigrationEndpoint -Name Fabrikam -ExchangeRemote -Autodiscover -EmailAddress tonysmith@fabrikam.com -Credentials (Get-Credential fabrikam\tonysmith) 
```
```    
    $csvData=[System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\batch.csv")
    New-MigrationBatch -CSVData $csvData -Timezone "Pacific Standard Time" -Name FabrikamMerger -SourceEndpoint Fabrikam -TargetDeliveryDomain "mail.contoso.com"
```
Дополнительные сведения о подготовке леса к межлесному перемещению см. в следующих разделах.

  - [Подготовка почтовых ящиков для запросов на перемещение между лесами](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [Подготовка почтовых ящиков для перемещения между лесами с помощью примера кода](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

  - [Подготовка почтовых ящиков к перемещению между лесами с использованием в консоли сценария Prepare-MoveRequest.ps1](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

Дополнительные сведения о синтаксисе и параметрах см. в разделах [New-MigrationBatch](https://technet.microsoft.com/ru-ru/library/jj219166\(v=exchg.150\)) и [New-MoveRequest](https://technet.microsoft.com/ru-ru/library/dd351123\(v=exchg.150\)).

## Как проверить, что все получилось?

Чтобы убедиться, что вы успешно завершили миграцию, выполните следующие действия.

  - В консоли выполните следующую команду для извлечения информации о перемещении почтовых ящиков.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Подробнее см. в разделе [Get-MigrationUserStatistics](https://technet.microsoft.com/ru-ru/library/jj218695\(v=exchg.150\)).

## Перемещение только архивного почтового ящика

## Использование Центра администрирования Exchange для перемещения только архивного почтового ящика

1.  В Центре администрирования Exchange откройте раздел **Получатели** \> **Миграция** и нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления").

2.  В мастере **нового локального перемещения почтовых ящиков** выберите пользователя, чей архивный почтовый ящик требуется переместить, нажмите кнопку **ОК** и затем кнопку **Далее**.

3.  На странице **Конфигурация перемещения** укажите имя нового пакета. Выберите элемент **Переместить только архивный почтовый ящик**, выберите параметры для расположения базы данных почтовых ящиков и нажмите кнопку **Создать**.

## Использование командной консоли для перемещения только архивного почтового ящика

В этом примере перемещается только архивный почтовый ящик "Tony Smith" на сервер DB03. Основной почтовый ящик не перемещается.

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -ArchiveOnly -ArchiveTargetDatabase "DB03"

Дополнительные сведения о синтаксисе и параметрах см. в разделах [New-MigrationBatch](https://technet.microsoft.com/ru-ru/library/jj219166\(v=exchg.150\)) и [New-MoveRequest](https://technet.microsoft.com/ru-ru/library/dd351123\(v=exchg.150\)).

## Как проверить, что все получилось?

Чтобы убедиться, что вы успешно завершили миграцию, выполните следующие действия.

  - В консоли выполните следующую команду для извлечения информации о перемещении почтовых ящиков.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Подробнее см. в разделе [Get-MigrationUserStatistics](https://technet.microsoft.com/ru-ru/library/jj218695\(v=exchg.150\)).

## Перемещение основного почтового ящика пользователя и архивного почтового ящика в разные базы данных

В этом примере основной почтовый ящик и архивный почтовый ящик пользователя Юлии перемещаются в разные базы данных. Основной ящик перемещается в DB01, а архив — в DB03.

    New-MoveRequest -Identity 'ayla@humongousinsurance.com' -TargetDatabase DB01 -ArchiveTargetDatabase -DB03

Дополнительные сведения о синтаксисе и параметрах см. в разделах [New-MigrationBatch](https://technet.microsoft.com/ru-ru/library/jj219166\(v=exchg.150\)) и [New-MoveRequest](https://technet.microsoft.com/ru-ru/library/dd351123\(v=exchg.150\)).

## Как проверить, что все получилось?

Чтобы убедиться, что вы успешно завершили миграцию, выполните следующие действия.

  - В консоли выполните следующую команду для извлечения информации о перемещении почтовых ящиков.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Подробнее см. в разделе [Get-MigrationUserStatistics](https://technet.microsoft.com/ru-ru/library/jj218695\(v=exchg.150\)).

## Перемещение основного почтового ящика пользователя и разрешение высокого предела неправильных элементов

## Использование Центра администрирования Exchange для перемещения основного почтового ящика пользователя и увеличения предельного количества неправильных элементов

1.  В Центре администрирования Exchange откройте раздел **Получатели** \> **Миграция** и нажмите кнопку **Добавить**![Значок добавления](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Значок добавления").

2.  В мастере **нового перемещения локальных почтовых ящиков** выберите пользователя, для которого требуется переместить основной почтовый ящик, нажмите кнопку **ОК** и затем кнопку **Далее**.

3.  На странице **Конфигурация перемещения** укажите имя нового пакета. Выберите элемент **Переместить только основной почтовый ящик** и выберите параметры для расположения базы данных почтовых ящиков.

4.  Щелкните элемент **Дополнительные параметры**![Значок дополнительных параметров](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Значок дополнительных параметров"), введите предельное количество неправильных элементов и нажмите кнопку **ОК**.

## Использование командной консоли для перемещения основного почтового ящика пользователя и увеличения предельного количества неправильных элементов

В этом примере основной почтовый ящик пользователя Елизаветы перемещается в базу данных DB01 почтовых ящиков, а для предельного количества неправильных элементов устанавливается значение `100`. Чтобы установить высокий предел неправильных элементов, необходимо использовать параметр *AcceptLargeDataLoss*.

    New-MoveRequest -Identity 'Lisa' -PrimaryOnly -TargetDatabase "DB01" -BadItemLimit 100 -AcceptLargeDataLoss

Дополнительные сведения о синтаксисе и параметрах см. в разделах [New-MigrationBatch](https://technet.microsoft.com/ru-ru/library/jj219166\(v=exchg.150\)) и [New-MoveRequest](https://technet.microsoft.com/ru-ru/library/dd351123\(v=exchg.150\)).

## Как проверить, что все получилось?

Чтобы убедиться, что вы успешно завершили миграцию, выполните следующие действия.

  - В консоли выполните следующую команду для извлечения информации о перемещении почтовых ящиков.
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

Подробнее см. в разделе [Get-MigrationUserStatistics](https://technet.microsoft.com/ru-ru/library/jj218695\(v=exchg.150\)).

