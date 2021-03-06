﻿---
title: 'Интервалы повторной отправки, повторной передачи и истечения срока действия сообщений: Exchange 2013 Help'
TOCTitle: Интервалы повторной отправки, повторной передачи и истечения срока действия сообщений
ms:assetid: 03020e6f-4c01-4c6e-ae47-fd74d4c4f96a
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ891103(v=EXCHG.150)
ms:contentKeyID: 51407996
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Интервалы повторной отправки, повторной передачи и истечения срока действия сообщений

 

_**Применимо к:** Exchange Server 2013_

_**Последнее изменение раздела:** 2015-03-09_

В Microsoft Exchange Server 2013 сообщения, которые не могут быть успешно доставлены, ограничены различными крайними сроками повторных попыток, повторной отправки и истечения срока действия в зависимости от источника и назначения сообщения. *Повторить попытку* является обновленной попыткой соединения с получателем. *Повторная отправка* — это передача сообщений обратно в очередь отправки для повторной обработки классификатором. Срок действия сообщения *истекает* после неудачного завершения всех попыток доставки сообщения в течение указанного периода времени. После истечения срока действия сообщения отправитель получает сообщение о недоставке. Затем данное сообщение удаляется из очереди.

При возникновении любого из трех событий — повторной передачи, повторной отправки и истечения срока действия, — прежде чем над сообщениями будут совершены соответствующие автоматические действия, можно выполнить некоторые действия вручную.

Инструкции по настройке этих интервалов см. в разделе [Настройка интервалов повторной отправки, повторной передачи и истечения срока действия сообщений](configure-message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md).

## Параметры конфигурации для повторной передачи сообщений

Когда транспортный сервер не может подключиться к следующему переходу, очередь переходит в состояние повтора. Попытки подключения продолжаются до тех пор, пока не истечет срок очереди или не будет установлено подключение.

## Параметры конфигурации для автоматической повторной отправки сообщений

Параметры конфигурации, доступные для настройки интервалов повторной отправки сообщений, приведены в следующей таблице.

### Параметры конфигурации, доступные для настройки интервалов повторной отправки сообщений

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Имя параметра или ключа</th>
<th>Значение по умолчанию</th>
<th>Где настраивать</th>
<th>Описание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueGlitchRetryCount</em></p></td>
<td><p>4</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>Этот ключ указывает количество попыток соединения, которые производятся сразу после возникновения неполадок на транспортном сервере при установке связи с конечным сервером. Такие неполадки с подключением обычно вызываются короткими перебоями в работе сети.</p>
<p>Допустимое значение для этого ключа — целое число от 0 до 15.</p>
<p>Обычно нет необходимости изменять этот ключ, если только сеть не оказалась ненадежной и случайные разрывы подключений в ней не случаются регулярно.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueGlitchRetryInterval</em></p></td>
<td><p><code>00:01:00</code> или 1 минута</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>С помощью этого ключа контролируется интервал проверки между попытками подключения, задаваемых ключом <em>QueueGlitchRetryCount</em>.</p>
<p>Обычно нет необходимости изменять этот параметр, если только сеть не оказалась ненадежной и случайные разрывы подключений в ней не случаются регулярно.</p></td>
</tr>
<tr class="odd">
<td><p><em>TransientFailureRetryCount</em></p></td>
<td><p>6</p></td>
<td><p>Командлет <strong>Set-TransportService</strong> или свойства сервера в Центре администрирования Exchange</p></td>
<td><p>В этом параметре указывается количество попыток подключений после неудачных попыток подключения, управляемых ключами <em>QueueGlitchRetryCount</em> и <em>QueueGlitchRetryInterval</em>. Проблемы с подключениями, которые приводят к обнулению ключей <em>QueueGlitchRetryCount</em> и <em>QueueGlitchRetryInterval</em>, могут быть вызваны перезагрузкой сервера или сбоями при поиске в кэшированном DNS.</p>
<p>Допустимое значение для этого параметра — целое число от 0 до 15. Если установить этот параметр на 0, следующая попытка подключения будет контролироваться параметром <em>OutboundConnectionFailureRetryInterval</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>TransientFailureRetryInterval</em></p></td>
<td><ul>
<li><p>Транспортная служба на серверах почтовых ящиков: <code>00:05:00</code> или 5 минут</p></li>
<li><p>Пограничные транспортные серверы: <code>00:01:00</code> или 10 минут</p></li>
</ul></td>
<td><p>Командлет <strong>Set-TransportService</strong> или свойства транспортного сервера в Центре администрирования Exchange</p></td>
<td><p>С помощью этого параметра контролируется интервал подключения между попытками подключения, задаваемыми параметром <em>TransientFailureRetryCount</em>.</p>
<p>Чтобы указать значение, введите его как промежуток времени: дд.чч:мм:сс, где дд — дни, чч — часы, мм — минуты и сс — секунды.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundConnectionFailureRetryInterval</em></p></td>
<td><ul>
<li><p>Транспортная служба на серверах почтовых ящиков: <code>00:10:00</code> или 10 минут</p></li>
<li><p>Пограничные транспортные серверы: <code>00:30:00</code> или 30 минут</p></li>
</ul></td>
<td><p>Командлет <strong>Set-TransportService</strong> или свойства транспортного сервера в Центре администрирования Exchange</p></td>
<td><p>В этом параметре указывается интервал повторных попыток для исходящих подключений, которые до этого завершились неудачно. Предыдущие неудачные попытки подключения контролируются параметрами <em>TransientFailureRetryCount</em> и <em>TransientFailureRetryInterval</em>.</p>
<p>Чтобы указать значение, введите его как промежуток времени: дд.чч:мм:сс, где дд — дни, чч — часы, мм — минуты и сс — секунды.</p></td>
</tr>
<tr class="even">
<td><p><em>MessageRetryInterval</em></p></td>
<td><p><code>00:15:00</code> или 15 минут</p></td>
<td><p>Командлет <strong>Set-TransportService</strong></p></td>
<td><p>В этом параметре указывается интервал повтора для отдельных сообщений в состоянии повтора. Рекомендуется изменять значение по умолчанию только после получения соответствующих указаний от службы технической поддержки Майкрософт.</p></td>
</tr>
<tr class="odd">
<td><p><em>MailboxDeliveryQueueRetryInterval</em></p></td>
<td><p><code>00:05:00</code> или 5 минут</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>Этот ключ определяет периодичность, с которой очереди пытаются подключиться к службе транспорта доставки почтовых ящиков для хранилища почтовых ящиков назначения, к которому не удалось подключиться.</p>
<p>Чтобы указать значение, введите его как промежуток времени: дд.чч:мм:сс, где дд — дни, чч — часы, мм — минуты и сс — секунды.</p>
<p>Допустимое значение для этого ключа — от 00:00:01 до 1.00:00:00.</p></td>
</tr>
</tbody>
</table>


В начало

## Параметры конфигурации для ручной повторной отправки сообщений

Если очередь доставки находится в состоянии повтора, можно вручную выполнить принудительную попытку немедленного подключения с помощью средства просмотра очереди в инструментах Exchange или с помощью командлета **Retry-Queue** в командной консоли. Ручная попытка повторной передачи имеет приоритет над следующей попыткой передачи по расписанию. Если попытка подключения не удалась, таймер интервала повторения сбрасывается. Чтобы это действие было выполнено, очередь доставки должна находиться в состоянии повтора.

Дополнительные сведения см. в разделе "Очереди повторов" в [Управление очередями](manage-queues-exchange-2013-help.md).

В начало

## Параметры конфигурации для сообщений DSN о задержке

После каждого сбоя доставки отправленных сообщений пограничный транспортный сервер или служба транспорта на сервере почтовых ящиков создает сообщение с уведомлением о задержке доставки и ставит его в очередь на доставку отправителю недоставленного сообщения. Это сообщение DSN о задержке доставки отправляется только по истечении указанного интервала времени ожидания уведомления о задержке и только если сообщение со сбоем не было успешно доставлено в течение этого времени. По умолчанию интервал времени ожидания уведомления о задержке равен 4 часам. Данная задержка предотвращает отправку ненужных уведомлений о состоянии задержанной доставки, причинами которой могут быть временные сбои в передаче сообщений. Отправка сообщений DSN с уведомлением о задержке доставки может избирательно включаться или отключаться для сообщений, создаваемых внутри или вне организации Exchange.

Параметры конфигурации, доступные для уведомлений о состоянии задержанной доставки, приведены в следующей таблице.

### Параметры конфигурации, доступные для уведомлений о состоянии задержанной доставки

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Имя параметра</th>
<th>Значение по умолчанию</th>
<th>Место</th>
<th>Описание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code>4 часа</p></td>
<td><p>Командлет <strong>Set-TransportService</strong> или свойства сервера в Центре администрирования Exchange</p></td>
<td><p>Этот параметр указывает время ожидания сервера, перед тем как он отправит отправителю сообщение DSN о задержке. Значение этого параметра всегда должно быть больше значения параметра <em>TransientFailureRetryCount</em>, умноженного на значение параметра <em>TransientFailureRetryInterval</em>.</p>
<p>Чтобы указать значение, введите его как промежуток времени: дд.чч:мм:сс, где дд — дни, чч — часы, мм — минуты и сс — секунды.</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>С помощью этого параметра указывается, следует ли отправлять сообщения DSN о задержке отправителям сообщений, которые находятся вне организации Exchange.</p>
<p>Для этого параметра допускаются значения <code>$true</code> и <code>$false</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>С помощью этого параметра указывается, следует ли отправлять сообщения DSN о задержке отправителям сообщений, которые находятся внутри организации Exchange.</p>
<p>Для этого параметра допускаются значения <code>$true</code> и <code>$false</code>.</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> На транспортных серверах-концентраторах Exchange 2007 все параметры <em>ExternalDSN*</em> и <em>InternalDSN*</em> доступны в командлете <strong>Set-TransportServer</strong>, а не в командлете <strong>Set-TransportConfig</strong>. Если в вашей организации есть транспортные серверы-концентраторы Exchange 2007, необходимо изменить эти значения с помощью командлета <strong>Set-TransportServer</strong> на каждом транспортном сервере-концентраторе Exchange 2007.


В начало

## Параметры конфигурации для повторной отправки сообщений

Повторная отправка сообщений отсылает сообщения обратно в очередь отправки для повторной обработки классификатором.

## Автоматическая повторная отправка сообщений

Недоставленные сообщения автоматически отправляются повторно, если очередь доставки находится в состоянии повтора и не смогла успешно доставить сообщения в указанный период времени. Этот промежуток времени контролируется ключом *MaxIdleTimeBeforeResubmit* в файле конфигурации приложения EdgeTransport.exe.config. Только сообщения в очередях доставки являются кандидатами для автоматической повторной отправки сообщений.

Чтобы указать значение, введите его как промежуток времени: дд.чч:мм:сс, где дд — дни, чч — часы, мм — минуты и сс — секунды.

Значением по умолчанию является `12:00:00` или 12 часов.

## Повторная отправка сообщений вручную

Вы можете повторно отправить вручную сообщения, имеющие следующее состояние в службе транспорта на сервере почтовых ящиков или пограничном транспортном сервере:

  - Очереди доставки в состоянии повтора. Сообщения в очередях не должны находиться в состоянии Suspended («Приостановка»).

  - Сообщения, находящиеся в очереди недоставленных сообщений, состояние которых отличается от приостановки.

  - Сообщения, находящиеся в очереди подозрительных сообщений.

Дополнительные сведения об очереди подозрительных сообщений и очереди недоставленных сообщений см. в пункте "Сведения об очереди подозрительных сообщений и очереди недоставленных сообщений" раздела [Очереди](queues-exchange-2013-help.md).

Если необходимо вручную передать сообщения, расположенные в очередях доставки или в очереди недоставленных сообщений, не дожидаясь истечения срока, указанного в параметре *MaxIdleTimeBeforeResubmit*, необходимо использовать командлет **Retry-Queue** с параметром *Resubmit*. Чтобы вручную передать сообщения, находящиеся в очереди подозрительных сообщений, можно использовать средство просмотра очередей или командлет **Resume-Message** для возобновления отправки сообщений. Дополнительные сведения см. в разделе "Повторная отправка сообщений в очереди" в [Управление очередями](manage-queues-exchange-2013-help.md).

Другим способом повторной отправки сообщений вручную является приостановка отправки сообщений, экспорт сообщений в текстовые файлы с расширением EML и последующим копированием этих файлов в каталог преобразования на любом транспортном сервере почтовых ящиков или пограничном транспортном сервере. Этот способ повторной отправки действует в отношении всех сообщений, расположенных в очередях отправки или в очереди недоставленных сообщений. Сообщения, находящиеся в очереди подозрительных сообщений, уже находятся в состоянии приостановки. Сообщения, которые находятся в очереди отправки, не могут быть приостановлены или экспортированы.

> [!NOTE]  
> При экспорте сообщений из очереди само сообщение в очереди не удаляется. После успешного завершения экспорта и повторной подачи сообщений с помощью каталога преобразования рекомендуется удалить приостановленные сообщения во избежание дублирования доставки сообщений.


Подробнее см. в разделе [Экспорт сообщений из очередей](export-messages-from-queues-exchange-2013-help.md).

В начало

## Параметры конфигурации для срока действия сообщения

*Интервал времени ожидания сообщений* определяет максимальную продолжительность времени, в течение которого пограничный транспортный сервер или служба транспорта на сервере почтовых ящиков пытается доставить сообщение со сбоем. Если сообщение не удается успешно доставить до истечения интервала времени ожидания, отправителю доставляется отчет о недоставке, содержащий исходное сообщение или заголовки сообщений.

## Автоматическое окончание срока действия сообщений

Интервал времени ожидания сообщений управляется параметром *MessageExpirationTimeOut* в командлете **Set-TransportService** или в свойствах сервера в Центре администрирования Exchange.

Чтобы указать значение, введите его как промежуток времени: дд.чч:мм:сс, где дд — дни, чч — часы, мм — минуты и сс — секунды.

Значение по умолчанию: `2.00:00:00` или 2 дня. Допустимый диапазон вводимых значений для этого параметра: от `00:00:05` до `90.00:00:00`.

## Окончание срока действия сообщений вручную

Несмотря на то, что закончить срок действия сообщений вручную невозможно, можно вручную удалить сообщения из любой очереди, кроме очереди отправки, с отчетом о недоставке или без него.

Дополнительные сведения см. в разделе "Удаление сообщений из очередей" в [Управление сообщениями в очередях](manage-messages-in-queues-exchange-2013-help.md).

В начало

