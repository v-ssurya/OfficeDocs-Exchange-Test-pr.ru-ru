﻿---
title: 'Разрешить пользователям совершать звонки: Exchange 2013 Help'
TOCTitle: Разрешить пользователям совершать звонки
ms:assetid: b6e696ce-c848-475b-a598-9035677497e2
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/Bb232172(v=EXCHG.150)
ms:contentKeyID: 51408067
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Разрешить пользователям совершать звонки

 

_**Применимо к:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Последнее изменение раздела:**2015-03-09_

*Исходящий звонок* — это процесс, при котором пользователи звонят в абонентскую группу единой системы обмена сообщениями, используя номер голосового доступа к Outlook, и совершают или переводят звонок на внутренний или внешний номер телефона. Для обработки звонков пользователей в единой системе обмена сообщениями используется много параметров исходящих звонков. Чтобы настроить исходящие звонки, необходимо настроить правила набора номера, группы правил набора номера и авторизацию набора номера для абонентских групп единой системы обмена сообщениями, а затем разрешить исходящие звонки в абонентских группах единой системы обмена сообщениями, политиках почтовых ящиков единой системы обмена сообщениями и автосекретарях. Кроме того, чтобы контролировать исходящие звонки в организации, можно настроить для абонентских групп единой системы обмена сообщениями телефонные коды или коды доступа, префикс страны и формат местных, междугородных или международных телефонных номеров. В данном разделе рассматриваются правила набора номера, группы правил набора номера и разрешения для набора номера, а также их использование для управления исходящими звонками в организации.

**Содержание**

Общие сведения

Types of users

Outdialing settings

Configuring outdialing

Applying configured dialing rule groups

Applying dialing rules

## Обзор

Исходящие звонки выполняются, когда:

  - совершается звонок на внешний номер телефона;

  - звонок переключается на автосекретарь;

  - звонок переключается на пользователя в вашей организации;

  - пользователь единой системы обмена сообщениями использует функцию воспроизведения по телефону.

Для надлежащего выполнения исходящих звонков необходимо правильно настроить следующие параметры:

  - **Правила набора номеров**   Правила набора номеров определяют номер, набираемый пользователем единой системы обмена сообщениями, и фактический номер, который будет набран УАТС или IP-УАТС.

  - **Группы правил набора номеров**.   Группы правил набора номеров определяют типы звонков, которые могут совершать пользователи из группы набора номеров.

  - **Авторизации набора номера**   Авторизации набора номера — это ограничения, которые будут применяться для предотвращения междугородних звонков или ненужных расходов на телефонную связь.

Чтобы разрешить исходящие вызовы для пользователей, звонящих абонентской группе или автосекретарю, необходимо выполнить следующие действия.

  - Убедитесь, что шлюзы VoIP, представленные IP-шлюзом единой системы обмена сообщениями, связанным с абонентской группой, будут разрешать исходящие вызовы.

  - Создайте группы правил набора номеров, создав правила набора номеров для абонентской группы единой системы обмена сообщениями.

  - Добавьте авторизации набора номеров для групп правил набора номеров внутри страны или региона и международных номеров в абонентской группе единой системы обмена сообщениями, политике почтовых ящиков единой системы обмена сообщениями или автоответчике, связанном с такой же абонентской группой, что и IP-шлюз единой системы обмена сообщениями.

## Типы пользователей

Использовать функцию исходящих звонков в единой системе обмена сообщениями могут пользователи двух типов: прошедшие проверку подлинности и не прошедшие ее. Все пользователи, звонящие автосекретарю единой системы обмена сообщениями, также являются пользователями, не прошедшими проверку подлинности. Когда пользователи набирают номер голосового доступа к Outlook, они считаются не прошедшими проверку подлинности, потому что они не предоставили свой добавочный номер и ПИН-код и не вошли в свой почтовый ящик. Пользователи проходят проверку подлинности после указания добавочного номера и ПИН-кода и успешного входа в почтовый ящик.

Когда пользователи звонят на номер голосового доступа к Outlook, настроенный в абонентской группе единой системы обмена сообщениями, и пытаются совершить или перевести вызов, не выполнив вход в свой почтовый ящик, к вызову применяются только параметры исходящего вызова абонентской группы единой системы обмена сообщениями. Когда анонимные пользователи или пользователи, не прошедшие проверку подлинности, звонят автосекретарю единой системы обмена сообщениями, к этому звонку применяются параметры исходящих звонков, настроенные и для автосекретаря, и для абонентской группы, связанной с автосекретарем.

Когда пользователи звонят на номер голосового доступа к Outlook, настроенный в абонентской группе, и успешно выполняют вход в почтовый ящик, они считаются прошедшими проверку подлинности. В таком случае параметры исходящих звонков используют правила набора номера и параметры авторизации набора номера в политике почтовых ящиков единой системы обмена сообщениями, связанные с такими пользователями.

В начало

## Параметры исходящих звонков

Чтобы применить правила исходящих звонков для своей организации, необходимо настроить несколько параметров. Кроме настройки абонентских групп единой системы обмена сообщениями, автосекретарей единой системы обмена сообщениями и политик почтовых ящиков единой системы обмена сообщениями, которые вы создали с помощью правильных правил набора номера и авторизаций набора номера, необходимо настроить коды доступа, префиксы и форматы номера в абонентских группах единой системы обмена сообщениями. Для абонентских групп, автосекретарей и политик почтовых ящиков единой системы обмена сообщениями настраиваются следующие параметры исходящих звонков:

  - коды доступа к внешней, междугородной и международной телефонным линиям;

  - префиксы страны;

  - форматы местных, междугородных и международных телефонных номеров;

  - настроенные группы правил набора номера местных, междугородных и международных номеров;

  - разрешенные группы правил набора номеров местных, междугородных и международных номеров;

  - Записи правил набора номера

  - Авторизации набора номера

Чтобы успешно настроить исходящие звонки для своей организации, сначала необходимо понять, как можно использовать каждый компонент для исходящих звонков и как необходимо настроить каждый компонент. В таблице ниже приведены все компоненты, которые нужно настроить в абонентских группах единой системы обмена сообщениями, автосекретарях единой системы обмена сообщениями и политиках почтовых ящиков единой системы обмена сообщениями, для правильной работы исходящих звонков.

### Компоненты управления исходящими звонками

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Компонент</th>
<th>Описание</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Телефонные коды, префиксы номеров и форматы номеров</p></td>
<td><p>В единой системе обмена сообщениями используются телефонные коды, префиксы и форматы номеров для определения правильного номера, который нужно использовать при совершении исходящего звонка. С помощью телефонных кодов, префиксов номеров и форматов номеров можно ограничить функцию исходящих звонков для пользователей, звонящих автосекретарю единой системы обмена сообщениями, связанному с абонентской группой единой системы обмена сообщениями, или для пользователей, набирающих номер голосового доступа к Outlook, настроенный для абонентской группы.</p></td>
</tr>
<tr class="even">
<td><p>Группы правил набора номера</p></td>
<td><p>Группы правил набора номера создаются, чтобы при исходящих звонках можно было изменять телефонные номера перед их отправкой УАТС. Группы правил набора номера позволяют удалять из телефонных номеров, задаваемых единой системой обмена сообщениями, цифры или добавлять их в телефонные номера. Например, можно создать группу правил набора номера, добавляющую к семизначному телефонному номеру префикс 9 для доступа к внешней телефонной линии. В этом примере пользователям, звонящим за пределы организации, не придется при наборе номера набирать цифру 9.</p>
<p>Каждая группа правил набора номера содержит правила набора номера, определяющие типы местных, междугородных и международных звонков, которые могут совершать пользователи, входящие в соответствующую группу правил набора номера. Действие групп правил набора номера распространяется на пользователей, связанных с абонентской группой или автосекретарями единой системы обмена сообщениями и политиками почтовых ящиков единой системы обмена сообщениями, связанными с абонентской группой. Каждая группа правил набора номера должна содержать хотя бы одно правило набора номера.</p></td>
</tr>
<tr class="odd">
<td><p>Записи правил набора номера</p></td>
<td><p>Каждое правило набора номера определяет типы звонков, которые могут совершать пользователи из группы правил набора номера. При создании группы правил набора номера необходимо настроить одно или несколько правил набора номера.</p>
<p>Настраивая каждое правило набора номера, необходимо ввести имя правила набора номера, шаблон номера для преобразования (<em>маска номера</em>) и набираемый номер. Кроме того, можно ввести комментарий. С помощью комментариев можно описать способ использования правила набора номера или группу пользователей, для которых будет применяться правило набора номера. При добавлении маски номера и набираемого номера в правило набора номера можно использовать букву &quot;x&quot;, которая представляет одну цифру, например 91425xxxxxxx. Можно также использовать подстановочный знак (*), например 91425*.</p></td>
</tr>
<tr class="even">
<td><p>Авторизации набора номера</p></td>
<td><p>Авторизация набора номера использует группы правил набора номера, чтобы применить ограничения набора номера к пользователям, связанным с определенной политикой почтовых ящиков, абонентской группой или автосекретарем единой системы обмена сообщениями. Ограничения набора номера можно также использовать, если нужно разрешить пользователям звонить по номерам внутри страны или международным телефонным номерам.</p>
<p>После того как вы создадите правила набора номера в абонентской группе единой системы обмена сообщениями, необходимо добавить группу правил набора номера в политику почтовых ящиков единой системы обмена сообщениями, абонентскую группу или автосекретарь. После добавления группы правил набора номера в политику почтовых ящиков единой системы обмена сообщениями все заданные параметры или правила будут применяться к пользователям с включенной поддержкой единой системы обмена сообщениями, связанным с политикой почтовых ящиков единой системы обмена сообщениями.</p></td>
</tr>
</tbody>
</table>


В начало

## Настройка исходящих звонков

Группа правил набора номера — это совокупность правил набора номера, настроенных для абонентской группы единой системы обмена сообщениями. Для абонентской группы единой системы обмена сообщениями можно настроить группы правил набора номера двух типов: для звонков внутри страны и для международных звонков. Действие групп правил набора номера для звонков внутри страны распространяется на набираемые телефонные номера, которые относятся к той же стране или региону. Действие групп правил набора номера для международных звонков распространяется на набираемые телефонные номера, относящиеся к другим странам.

Каждая абонентская группа единой системы обмена сообщениями может содержать одну или несколько групп правил набора номера. Чтобы применить группу правил набора номера к группе пользователей, созданную группу правил набора номера необходимо добавить в список разрешенных групп правил набора номера для абонентской группы и автосекретарей единой системы обмена сообщениями, а также связанных с абонентской группой политик почтовых ящиков единой системы обмена сообщениями.

Группы правил набора номера позволяют администраторам указывать правила набора номера, которые необходимо применить к группе пользователей с включенной поддержкой единой системы обмена сообщениями, относящихся к определенной категории. Например, с помощью групп правил набора номера можно определить группу пользователей, которым разрешается совершать международные звонки, и группу, которой разрешается совершать только местные или междугородные звонки. Создать группу правил набора номера можно в Центре администрирования Exchange или с помощью командлета **Set-UMDialPlan** в командной консоли Exchange. При создании группы правил набора номера необходимо определить для нее хотя бы одно правило набора номера.

Когда пользователь набирает номер телефона, единая система обмена сообщениями ищет соответствие ему в правилах набора номера. Если соответствие найдено, единая система обмена сообщениями с помощью правила набора номера определяет номер, который нужно набрать, по номеру телефона или цифрам, указанным в разделе **Dialed Number** правила набора номера. Будет набран номер, указанный в поле **Dialed Number** правила набора номера.

Примеры правил набора номера и групп правил набора номера приведены в следующей таблице. В этом примере Local-Calls-Only и Low-Rate — это созданные группы правил набора номера. Группа правил набора номера Local-Calls-Only содержит два правила набора номера: 91425\* и 91206\*, а группа правил набора номера Low-Rate также содержит два правила набора номера: 91509\* и 91360\*.

### Правила набора номера и группы правил набора номера

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>NumberMask (Маска номера)</th>
<th>DialedNumber (Набираемый номер)</th>
<th>Комментарий</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Local-Calls-Only</p></td>
<td><p>91425*</p></td>
<td><p>91*</p></td>
<td><p>Местные звонки</p></td>
</tr>
<tr class="even">
<td><p>Local-Calls-Only</p></td>
<td><p>91206*</p></td>
<td><p>91*</p></td>
<td><p>Местные звонки</p></td>
</tr>
<tr class="odd">
<td><p>Low-Rate</p></td>
<td><p>91509*</p></td>
<td><p>9*</p></td>
<td><p>Междугородные звонки</p></td>
</tr>
<tr class="even">
<td><p>Low-Rate</p></td>
<td><p>91360*</p></td>
<td><p>9*</p></td>
<td><p>Междугородные звонки</p></td>
</tr>
</tbody>
</table>


Например, когда пользователь набирает 9-1-425-555-1234, единая система обмена сообщениями набирает 4255551234. Она удаляет все знаки, отличные от цифр (например, дефисы), и применяет маску номера из правила набора номера. В данном примере единая система обмена сообщениями применяет маску номера 91\*. Данная маска указывает, что единая система обмена сообщениями должна пропустить 9 и 1 и набрать все остальные цифры телефонного номера, находящиеся правее цифры 1, в том числе все цифры, представленные звездочкой (\*).

Создавать и настраивать правила набора номера и их группы для местных, междугородных и международных звонков можно с помощью Центра администрирования Exchange или командной консоли. Однако при создании многочисленных или сложных правил набора номера и их групп иногда удобнее использовать CSV-файл в командной консоли. Список правил набора номера и их групп можно импортировать и экспортировать.

Чтобы импортировать список правил набора номера и их групп, определенных в CSV-файле, воспользуйтесь командлетом **Set-UMDialPlan** следующим образом.

    Set-UMDialPlan "MyUMDialPlan" -ConfiguredInCountryOrRegionGroups $(IMPORT-CSV c:\dialrules\InCountryRegion.csv)

Чтобы получить список групп правил набора номера, настроенных для абонентской группы единой системы обмена сообщениями, воспользуйтесь командлетом **Get-UMDialPlan** следующим образом.

    (Get-UMDialPlan -id "MyUMDialPlan").ConfiguredInCountryOrRegionGroups | EXPORT-CSV C:\incountryorregion.csv

CSV-файл необходимо создать и сохранить в правильном формате. Каждая строка в этом файле представляет одно правило набора номера. Тем не менее, каждое правило набора номера настраивается для одной и той же группы правил набора номера. Каждое правило в этом файле состоит из четырех элементов, разделенных запятыми. имя, маска номера, набираемый номер и комментарий. Все эти элементы обязательны и должны содержать корректные данные (за исключением комментария). Между запятыми и следующими за ними элементами не должно быть пробелов, а между правилами и в конце файла не должно быть пустых строк. Ниже приведен пример CSV-файла, который можно использовать, чтобы создать правила набора номера и группы правил набора номера для звонков внутри страны.

**Name,NumberMask,DialedNumber,Comment**

**Low-rate,91425xxxxxxx,9xxxxxxx,Местный звонок**

**Low-rate,9425xxxxxxx,9xxxxxxx,Местный звонок**

**Low-rate,9xxxxxxx,9xxxxxxx,Местный звонок**

**Any,91\*,91\*,Открытие доступа к междугородным номерам**

**Long-distance,91408\*,91408\*,междугородный звонок**

Ниже приведен пример CSV-файла, который можно использовать, чтобы создать группы и записи правил набора номера для международных звонков.

**Name,NumberMask,DialedNumber,Comment**

**International, 901144\*, 901144\*, международный звонок**

**International, 901133\*, 901133\*, международный звонок**

В начало

## Применение настроенных групп правил набора номера

Группы правил набора номера создаются для абонентской группы единой системы обмена сообщениями. Группы правил набора номера для местных, междугородных или международных звонков можно создать в консоли управления Центра администрирования Exchange или с помощью командлета **Set-UMDialPlan** в командной консоли. После создания групп правил набора номера для абонентской группы единой системы обмена сообщениями и определения правил набора номера можно применить созданные группы к абонентской группе или автосекретарю единой системы обмена сообщениями или к пользователям, на которых распространяется политика почтовых ящиков единой системы обмена сообщениями, в зависимости от того, как пользователь получает доступ к единой системе обмена сообщениями.

Группы правил набора номера, созданные для абонентской группы единой системы обмена сообщениями, можно применять к указанным ниже элементам.

  - **Та же абонентская группа**.   Эти параметры будут применяться ко всем пользователям, набирающим номер голосового доступа к Outlook, но не вошедшим в свои почтовые ящики. Чтобы применить группу правил набора номера с именем `MyAllowedDialRuleGroup` для звонков внутри страны к той же абонентской группе, воспользуйтесь командлетом **Set-UMDialPlan** в командной консоли следующим образом.
    
        Set-UMDialPlan -Identity MyUMDialPlan -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

  - **Одна или несколько политик почтовых ящиков единой системы обмена сообщениями.   **Параметры, настроенные в политике почтовых ящиков единой системы обмена сообщениями, будут применяться ко всем пользователям, на которых распространяется действие этой политики. Эти параметры будут применяться к пользователям, набирающим номер голосового доступа к Outlook и уже вошедшим в свои почтовые ящики. Чтобы применить группу правил набора номера для звонков внутри страны с именем `MyAllowedDialRuleGroup` к отдельной политике почтовых ящиков единой системы обмена сообщениями, воспользуйтесь страницей **Авторизация набора номера** в политике почтовых ящиков Центра администрирования Exchange или командлетом **Set-UMMailboxPolicy** в командной консоли следующим образом.
    
        Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

  - **Один или несколько автосекретарей, связанных с абонентской группой единой системы обмена сообщениями**.   Эти параметры будут применяться ко всем пользователям, звонящим автосекретарю единой системы обмена сообщениями. Чтобы применить группу правил набора номера для звонков внутри страны с именем `MyAllowedDialRuleGroup` к отдельному автосекретарю единой системы обмена сообщениями, воспользуйтесь страницей **Авторизация набора номера** для автосекретаря в Центре администрирования Exchange или командлетом **Set-UMAutoAttendant** в командной консоли следующим образом.
    
        Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups MyAllowedDialRuleGroup

Способы применения групп правил набора номера в единой системе обмена сообщениями приведены в следующей таблице.

### Применение правил исходящих звонков

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Тип абонента</th>
<th>Область применения</th>
<th>Применяемые параметры исходящих звонков</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Номер голосового доступа к Outlook</p></td>
<td><p>Пользователь набирает номер голосового доступа к Outlook абонентской группы и входит в свой почтовый ящик</p></td>
<td><p>Политика почтовых ящиков единой системы обмена сообщениями</p></td>
</tr>
<tr class="even">
<td><p>Анонимный абонент</p></td>
<td><p>Пользователь набирает номер голосового доступа к Outlook абонентской группы</p></td>
<td><p>Абонентская группа единой системы обмена сообщениями</p></td>
</tr>
<tr class="odd">
<td><p>Анонимный абонент</p></td>
<td><p>Пользователь набирает добавочный номер телефона или телефонный номер доступа к автосекретарю</p></td>
<td><p>Автосекретарь единой системы обмена сообщениями</p></td>
</tr>
<tr class="even">
<td><p>Абонент, находящийся внутри организации</p></td>
<td><p>Пользователь набирает номер воспроизведения на телефоне.</p></td>
<td><p>Политика почтовых ящиков единой системы обмена сообщениями</p></td>
</tr>
</tbody>
</table>


В начало

## Применение правил набора номера

Исходящий звонок выполняется в следующих случаях:

  - единая система обмена сообщениями выполняет для абонента вызов внешнего телефонного номера;

  - единая система обмена сообщениями переводит звонок автосекретарю;

  - единая система обмена сообщениями переключает звонок на пользователя в вашей организации;

  - пользователь единой системы обмена сообщениями использует функцию воспроизведения по телефону.

В каждом из этих сценариев единая система обмена сообщениями применяет правила набора номера и осуществляет звонок для пользователя. Однако в зависимости от сценария и от того, как пользователь инициирует вызов, единая система обмена сообщениями может применять к набираемому телефонному номеру только некоторые из правил набора номера. В других случаях единая система обмена сообщениями может применить все правила исходящих звонков, настроенные для набираемого телефонного номера.

В начало
