﻿---
title: 'Рекомендации по выбору размера развертывания Exchange 2013 и его настройке: Exchange 2013 Help'
TOCTitle: Рекомендации по выбору размера развертывания Exchange 2013 и его настройке
ms:assetid: 4c4ba2fc-014a-46fb-949a-2dabba92c4a5
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Dn879075(v=EXCHG.150)
ms:contentKeyID: 63892240
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Рекомендации по выбору размера развертывания Exchange 2013 и его настройке

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2017-03-27_

Выпуск Exchange 2013 является более ресурсоемким, чем предыдущие версии Exchange. Правильно определив размер инфраструктуры Exchange 2013 и использовав некоторые рекомендуемые конфигурации для компонентов ИТ-инфраструктуры, связанных с Exchange, можно создать основу для развертывания обеспечивающего оптимальную производительность.

## Изменение размера Exchange 2013

Выбор правильного размера Exchange 2013 является одним из наиболее эффективных способов предотвращения проблем с производительностью. Калькулятор для расчета требований для роли сервера Exchange 2013 [доступен здесь](https://go.microsoft.com/fwlink/p/?linkid=523844). Последняя версия — 6.6, но мы рекомендуем вам периодически проверять наличие обновлений. Чтобы правильно использовать калькулятор, обратитесь к рекомендациям в записях блога [Калькулятор требований для роли сервера Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=386677) и [Изменение размера развертывания Exchange 2013](https://go.microsoft.com/fwlink/p/?linkid=301990).

Крайне важно сначала воспользоваться калькулятором, прежде чем приобретать оборудование и приступать к его развертыванию; в первую очередь определите общие требования к ресурсам на основе результатов, полученных с помощью калькулятора. В калькуляторе можно указать потребности вашей организации и использовать полученные результаты в качестве указаний по масштабированию оборудования. Калькулятор не предоставит сведения о том, сколько серверов использовать, однако он позволяет оценить влияние рабочей нагрузки Exchange на заданный набор серверов. Поэкспериментируйте с различными конфигурациями и оцените влияние на производительность, чтобы развертывание соответствовало потребностям и бизнес-требованиям, характерным для вашей среды.

Для упрощения развертывания и наиболее эффективного использования оборудования группа по продуктам Exchange рекомендует использовать серверы с несколькими ролями. Использование серверов с несколькими ролями обеспечивает лучшую доступность на уровне сервера клиентского доступа, поскольку для обработки запросов во случае сбоев имеется несколько серверов клиентского доступа. Ключевой аспект при проектировании развертывания Exchange 2013 заключается в том, чтобы использовать менее мощные серверы обычных типов (горизонтальное масштабирование вместо вертикального). При проектировании и тестировании использовались компьютеры с двумя сокетами, имеющие до двадцати ядер процессора и ОЗУ объемом до 96 ГБ. Если характеристики имеющегося оборудования выше указанных, следует рассмотреть другие варианты, например использование этого оборудования для решения других задач и приобретение менее мощных серверов для среды Exchange 2013 или виртуализация.

Рекомендуется создавать дополнительные серверы (горизонтальное масштабирование), чем добавлять вычислительные ресурсы в существующие, больше мощные серверы (вертикальное масштабирование). Горизонтальное масштабирование позволяет реализовать в среде преимущества функций высокой доступности, встроенные в Exchange 2013. Чтобы понять, почему рекомендуется использовать именно эту конфигурацию, ознакомьтесь более подробно с записями блога [Предпочтительная архитектура](https://go.microsoft.com/fwlink/p/?linkid=523782) и [Влияние устойчивости сайта на обеспечение доступности](https://go.microsoft.com/fwlink/p/?linkid=523845).

Калькулятор не учитывает наличие на серверах Exchange продуктов сторонних производителей или продуктов, которые взаимодействуют с Exchange (включая приложения, разработанные внутри компании), это означает, что при выборе размера развертывания следует обязательно учитывать такие продукты. Например, сервер Lync Server, сторонние приложения веб-служб Exchange (EWS) и устройства ActiveSync значительно повышают требования к ЦП на одного пользователя. Сведения о влиянии продуктов сторонних производителей на работу Exchange см. в документации к соответствующему продукту. Прежде чем реализовывать решения сторонних производителей, рекомендуется установить базовое значение производительности.

## Рекомендуемые конфигурации производительности

Ниже представлены рекомендации по оптимизации производительности для среды Exchange 2013.

## Питание

Настройте BIOS таким образом, чтобы управление питанием осуществлялось операционной системой (ОС).

В операционной системе выберите схему управления питанием "Высокое быстродействие".

## Процессоры

Отключите технологию Hyper-Threading на физических серверах Exchange. Если применяется виртуализация, на физическом сервере можно включить технологию Hyper-Threading, однако при этом каждому виртуальному серверу необходимо выделить только необходимое количество виртуальных процессоров (не допускайте избыточного распределения виртуальных процессоров), а для расчета размера используйте только количество ядер физических процессоров.

В Exchange Server 2013 пакетом обновления 1 (SP1) или более поздней версии можно разрешить разгрузку SSL, чтобы уменьшить использование ресурсов ЦП серверами клиентского доступа, однако сложные настройки разгрузки SSL могут не оказать преимущества.

## Платформа .NET Framework


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Версия Exchange</th>
<th>.NET Framework 4.7.1</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU19</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU16 - CU18</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


Если не удается установить платформу .NET 4.5.2, обратитесь к статье 2995145 базы знаний Майкрософт "[Проблемы производительности или задержки при подключении к серверу Exchange Server 2013, который работает под управлением Windows Server](https://go.microsoft.com/fwlink/p/?linkid=524159)". Исправления, представленные в этой статье, были разработаны на основе внутренних результатов при использовании памяти рабочего процесса хранилища. Применив эти исправления, вы сможете снизить общее потребление памяти для всех управляемых процессов (включая рабочий процесс хранилища), а также уменьшить общее время ЦП, затрачиваемое на сборку мусора .NET.

## Исправления

Команда специалистов по производительности Exchange рекомендует установить все указанные ниже исправления, связанные с производительностью.

  - [Доступно обновление, которое улучшает устойчивость кластеров в Windows Server 2012](https://go.microsoft.com/fwlink/p/?linkid=524088)

  - [Рекомендуемые исправления и обновления для отказоустойчивых кластеров под управлением Windows Server 2012](https://go.microsoft.com/fwlink/p/?linkid=524089)

  - [Рекомендуемые исправления и обновления для отказоустойчивых кластеров под управлением Windows Server 2012 R2](https://go.microsoft.com/fwlink/p/?linkid=524090)

  - [Неверное назначение процессора RSS на компьютере с многоядерными процессорами под управлением Windows 8 или Windows Server 2012](https://go.microsoft.com/fwlink/p/?linkid=324140)

  - [Проблемы производительности или задержки при подключении к серверу Exchange Server 2013, который работает под управлением Windows Server](https://go.microsoft.com/fwlink/p/?linkid=312962)

  - [Проблемы с подключением Outlook, когда в Exchange 2013 для параметра SSLOffloading задано значение "True"](https://go.microsoft.com/fwlink/p/?linkid=524091)

  - [Долгое подключение Outlook к серверу после отработки отказа базы данных в Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=524092)

  - [Снижение производительности в Outlook Web App в случае интеграции Lync с Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=524093)

  - [Службам аварийного управления требуется много времени на выполнение первой команды в среде Exchange Server 2013 с накопительным пакетом обновления 5 (CU5)](https://go.microsoft.com/fwlink/p/?linkid=524094)

  - [Задержка маршрутизации сообщений при включении протокола IPv6 в Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=524095)

  - [Активное использование ЦП приложением, зависящим от клиента Microsoft LDAP в Windows Server 2008 R2 с пакетом обновления 1 (SP1)](https://go.microsoft.com/fwlink/p/?linkid=530287)

  - [Большая загрузка ЦП при использовании RPC по протоколу HTTP в Windows 8.1 или Windows Server 2012 R2](https://go.microsoft.com/fwlink/p/?linkid=619127)

## Сеть

Для работы с Exchange 2013 рекомендуется использовать один сетевой адаптер, поскольку теперь больше не требуется разделять MAPI и сети для репликации. Дополнительные сведения см. в разделе [Network requirements](planning-for-high-availability-and-site-resilience-exchange-2013-help.md).

По возможности используйте параметры разгрузки SNP, а также убедитесь, что включена функция RSS (по умолчанию в Windows Server 2012 и более поздних версиях). RSS обеспечивает поддержку масштабирования загрузки ЦП, особенно в сетях 10GbE.

Убедитесь, что в операционной системе не применяются параметры отключения сетевого адаптера для экономии электроэнергии.

Проверяйте актуальность драйверов сетевого адаптера. Каждый месяц обращайтесь к поставщику для получения соответствующих обновлений драйверов.

## Службы IIS (Internet Information Services)

Во время установки Exchange изменяет некоторые ограничения числа подключений для служб IIS. Дальнейшая настройка служб IIS не рекомендуется.

Избегайте настройки, когда это возможно. Любые изменения в файле web.config или разделов реестра могут быть перезаписаны при установке накопительных пакетов обновления для Exchange или обновлений Windows.

## Хранилище

Рекомендации для хранилища Exchange 2013 представлены в статье [Параметры конфигурации хранилища Exchange 2013](exchange-2013-storage-configuration-options-exchange-2013-help.md).

## Виртуализация

См. раздел [Requirements for hardware virtualization](exchange-2013-virtualization-exchange-2013-help.md). Кроме того, обратите внимание, что архитектура Exchange не является архитектурой NUMA. Поэтому рекомендуется использовать настройки NUMA по умолчанию, заданные изготовителем оборудования.

## Служба каталогов Active Directory

Следите за производительностью сервера каталогов, потому что запросы службы Active Directory напрямую влияют на развертывание Exchange.

Время поиска LDAP — важный счетчик для измерения в отношении работоспособности службы каталогов Active Directory. Следите за загрузкой ЦП на контроллерах домена. Проблемы с ЦП на контроллерах домена будут сказываться как снижение производительности серверов Exchange.

Воспользуйтесь встроенными средствами диагностики Active Directory на контроллере домена в системном мониторе (в разделе "Набор сборщиков данных"), которые помогают выявить причины проблем с производительностью контроллера домена.

Запланируйте использование достаточного объема оперативной памяти на контроллерах домена, чтобы обеспечить кэширование файла базы данных AD целиком.

Рекомендуется развертывать 1 ядро глобального каталога Active Directory для каждых 8 ядер почтовых ящиков, которые обрабатывают активную нагрузку (на основе 64-разрядных ядер глобального каталога).

## Балансировка нагрузки

Все серверы клиентского доступа должны получать примерно одинаковое количество входящих подключений.

Для всех протоколов Exchange 2013 не требует привязки сеанса между заданным сервером клиентского доступа и подсистемой балансировки нагрузки.

Для управления всем входящим на серверы клиентского доступа трафиком следует использовать устройство балансировки нагрузки или программную подсистему балансировки нагрузки. Целевой сервер может выбираться различными способами, например циклически, когда каждое входящее подключение переходит на следующий целевой сервер в циклическом списке, или по методу "наименьших подключений", когда подсистема балансировки нагрузки отправляет новое подключение на сервер, у которого на текущий момент меньше всего установленных подключений. Более подробно эти способы рассмотрены в статье [Балансировка нагрузки](load-balancing-exchange-2013-help.md). Также необходимо учесть указанные ниже моменты.

  - Циклический перебор имеет недостаток — медленная сходимость с долгоживущими подключениями (например, RPC/HTTP). По мере подключения новых компьютеров обеспечение сходимости баланса подключений, обслуживаемых на целевых компьютерах, будет занимать очень много времени.

  - При использовании метода "наименьших подключений" будьте внимательны, поскольку сервер клиентского доступа может оказаться перегруженным и не отвечать во время сбоя или установки исправлений. В контексте производительности Exchange проверка подлинности является ресурсоемкой операцией.

Поскольку существуют различные ограничения на использование балансировки сетевой нагрузки Windows (NLB) в среде Exchange 2013, которые подробно описаны в статье [Балансировка нагрузки](load-balancing-exchange-2013-help.md), не рекомендуется использовать балансировку сетевой нагрузки Windows.

## Распределение пользователей и баз данных

Необходимо обеспечить хорошо сбалансированное распределение пользователей для каждой базы данных и активных баз данных на один сервер. Следует равномерно распределить использование пространства диска базы данных, а также сбалансировать пользователей с высокой нагрузкой между всеми базами данных.

Чтобы понять, как пользователи взаимодействуют с Exchange (с устройств, через Outlook и OWA), а также оценить влияние этих действий на производительность, необходимо профилировать базу пользователей. Воспользуйтесь ссылками на блоги, посвященные калькулятору, из раздела 2, чтобы получить лучшее понимание того, как профилировать использование Exchange каждым пользователем.

Настройте приоритет активации копии базы данных и параметры "MaximumPreferredActiveDatabases" (на каждом сервере) для обеспечения балансировки во время отработки отказа или переключения.

Сценарий RedistributeActiveDatabases.ps1 позволяет перераспределить активные базы данных на узлах группы обеспечения доступности баз данных.

Применяйте строгие ограничения на количество элементов в соответствии с требованиями Office 365. Это можно сделать с помощью командлета Set-Mailbox и сведений, представленных в статье [Ограничения для папок почтовых ящиков](https://go.microsoft.com/fwlink/p/?linkid=398779).

## Файл подкачки

Задайте максимальный размер 32 778 МБ для файла подкачки, если вы используете более 32 ГБ ОЗУ.

Файл подкачки не должен находиться на том же диске, что и файлы базы данных Exchange или файлы журнала базы данных.

Крайне важно использовать фиксированный размер файла подкачки и отключить для системы Windows возможность управлять размером этого файла. Увеличение размера файла подкачки может оказаться весьма ресурсоемкой задачей, что, в свою очередь, может привести к проблемам, когда Exchange находится под нагрузкой.

Если вам требуется полный дамп ядра, воспользуйтесь инструкциями в статье [Как создать файл дампа памяти ядра или файл полного дампа памяти в Windows Server 2008 и Windows Server 2008 R2](https://go.microsoft.com/fwlink/p/?linkid=524044).

## Режим Outlook

Рекомендуется использовать режим кэширования. Сведения о преимуществе режима кэширования см. в статье [Выбор между режимом кэширования Exchange и сетевым режимом для Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=524045).

Важно отметить, что на производительность сервера влияют как надстройки сервера, так надстройки для Outlook сторонних производителей. При использовании сетевого режима клиенты могут ожидать возникновения некоторых проблем с производительностью, вызванных надстройками сторонних производителей, наличием большего числа элементов, ограниченных представлений, количеством пользователей, обращающихся к почтовому ящику, а также другими факторами. На производительность устаревших клиентов, в отличие от Outlook 2013, большее влияние может оказать наличие большого числа элементов.

Если основная причина кроется в том, что Outlook в организации настроен на работу в сетевом режиме в целях обеспечения безопасности, рекомендуется вместо этого использовать BitLocker.

В Outlook 2013 представлена новая функция "Ползунок синхронизации", которая позволяет сократить время загрузки и размер OST-файла. Дополнительные сведения см. в статье [Настройка режима кэширования Exchange в Outlook 2013](https://go.microsoft.com/fwlink/p/?linkid=390456).

Ежемесячно проверяйте наличие обновлений для клиентов Outlook, поддерживаемых в вашей среде.

## Программное обеспечение сторонних производителей

При устранении неполадок с производительностью Exchange рекомендуется удалить или отключить программное обеспечение сторонних производителей. Ниже перечислены типы программного обеспечения сторонних производителей, которое, по данным службы технической поддержки корпорации Майкрософт, чаще всего влияет на производительность Exchange 2013.

  - Решения для защиты от вирусов

  - Программное обеспечение для предотвращения вторжений

  - Программы для резервного копирования

  - Программное обеспечения для аудита (как файлов, так и пользователей)

  - Решения для архивации

