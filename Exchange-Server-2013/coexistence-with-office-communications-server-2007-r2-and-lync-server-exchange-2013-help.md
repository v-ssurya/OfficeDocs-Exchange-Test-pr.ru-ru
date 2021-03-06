﻿---
title: 'Сосуществование с Office Communications Server 2007 R2 и Lync Server: Exchange 2013 Help'
TOCTitle: Сосуществование с Office Communications Server 2007 R2 и Lync Server
ms:assetid: f12d65c7-0b2c-46a1-a14a-802a76296fa1
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ851069(v=EXCHG.150)
ms:contentKeyID: 50556501
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Сосуществование с Office Communications Server 2007 R2 и Lync Server

 

_**Применимо к:** Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:** 2015-03-09_

Communications Server 2007 R2 и Lync Server предоставляют широкие функциональные возможности, включая обмен мгновенными сообщениями (IM), сведения о присутствии, многопользовательские сеансы мгновенных сообщений, и их функции голосовой почты можно интегрировать с единой системой обмена сообщениями Exchange. В развертываниях, которые интегрируются с Lync Server 2010 или 2013, у пользователей можно включить для корпоративную голосовую связь, которая позволяет пользователям, для которых включена поддержка доступа к голосовой почте, использовать для доступа к голосовой почте компоненты Lync Server.

При интеграции единой системы обмена сообщениями с более ранними версиями Office Communications Server или Lync Server будут доступны не все средства. Чтобы пользователи могли использовать все новые и улучшенные функциональные возможности, такие как фотографии с высоким разрешением, универсальное хранилище контактов и интеграция с архивом Lync, они должны иметь учетные записи пользователей Lync Server 2013 и Exchange Server 2013, а также им необходимо использовать последнюю версию клиента Lync 2013. Например, единое хранилище контактов недоступно для пользователей с включенной поддержкой корпоративной голосовой связи в Lync Server 2010, а фотографии с высоким разрешением не могут быть отображены в Lync 2010.

При интеграции единой системы обмена сообщениями с Office Communications Server 2007 R2 или Lync Server 2010, возможно, потребуется установить дополнительные исправления, накопительные обновления и пакеты обновления на Office Communications Server 2007 R2 или Lync 2010 в вашей организации. Что именно нужно установить, будет зависеть от топологии развертывания, а также версий продуктов, интегрируемых с единой системой обмена сообщениями Exchange.

## Необходимые исправления, накопительные пакеты обновления, накопительные обновления и пакеты обновления

В следующей таблице показаны исправления, необходимые для каждой версии продуктов при интеграции с единой системой обмена сообщениями.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Office Communications Server 2007 R2</p></td>
<td><p>Накопительное обновление 10 для Office Communications Server 2007 R2 или более позднее.</p></td>
</tr>
<tr class="even">
<td><p>Lync Server 2010</p></td>
<td><p>Накопительное обновление 3 для Lync Server 2010 или более позднее.</p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p>Никакие обновления не нужны.</p></td>
</tr>
</tbody>
</table>

