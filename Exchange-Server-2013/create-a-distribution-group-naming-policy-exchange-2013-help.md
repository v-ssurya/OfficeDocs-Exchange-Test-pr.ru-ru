﻿---
title: 'Создание политики именования групп рассылки: Exchange 2013 Help'
TOCTitle: Создание политики именования групп рассылки
ms:assetid: b2ffb654-345d-4be1-be8e-83d28901373e
ms:mtpsurl: https://technet.microsoft.com/ru-ru/library/JJ218693(v=EXCHG.150)
ms:contentKeyID: 50487268
ms.date: 04/30/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Создание политики именования групп рассылки

 

_**Применимо к:** Exchange Online, Exchange Server 2013_

_**Последнее изменение раздела:** 2012-11-01_

*Политика именования групп* позволяет упорядочить именование групп рассылок, которые создаются пользователями в организации. Можно задать обязательные суффикс и префикс для имени создаваемых групп рассылки и заблокировать определенные слова. Это позволяет предотвратить использование неуместных слов в именах групп.

Политика именования групп используется для:

  - применения согласованной стратегии именования групп, создаваемых пользователями;

  - идентификации групп рассылки в общей адресной книге;

  - указания на назначение или состав группы;

  - указания на пользователей — потенциальных членов группы;

  - указания региона использования группы;

  - предотвращения использования неуместных слов в именах групп.

Как работает политика именования групп? Когда пользователь создает группу, в поле «Отображаемое имя» вводится имя группы. После создания группы Microsoft Exchange применяет политику именования групп, добавляя префиксы и суффиксы, определенные в политике. Полное имя отображается в списке групп рассылки в Центре администрирования Exchange (EAC), в общей адресной книге и в полях сообщений электронной почты «Кому», «Копия» и «От». Если пользователь указывает заблокированное слово, при попытке сохранения новой группы появляется сообщение об ошибке с просьбой убрать слово и повторить сохранение.

Ниже приведены несколько примеров политики именования групп. В каждом из них **\<Имя группы\>** означает описательное имя, которое группе присвоил тот, кто ее создает. Система Exchange добавляет префиксы и суффиксы, определенные в политике, и отображает имя, когда группа создана.

  - Текстовые строки с подчеркиваниями, используемые в качестве префикса (**DG**) и суффикса (**Users**):
    
    **DG\_\<имя группы\>\_Users**

  - Несколько префиксов (**DG** и **Contoso**) и один суффикс (**Users**) с использованием текстовых строк:
    
    **DG\_Contoso\_\<имя группы\>\_Users**

  - АТрибут (**Department**), используемый как префикс:
    
    **Department\_\<имя группы\>**
    
    Предположим, у преподавателей в учебном заведении заполнен атрибут Department. Вот пример имени группы, созданной сотрудником отдела психологии:
    
    **Psychology\_Cognitive201**
    
    В этом примере знак подчеркивания указан в качестве второго префикса, чтобы отделить имя отдела от имени группы.

## Что нужно знать перед началом работы?

  - Осталось времени до завершения: 5 минут.

  - Для выполнения этих процедур необходимы соответствующие разрешения. Сведения о необходимых разрешениях см. в статье Запись «Группы рассылки» в разделе [Разрешения получателей](recipients-permissions-exchange-2013-help.md).

  - Максимальная длина имени группы — 64 символа. Сюда включается общее число символов префикса, имени, указанного пользователем, и суффикса.

  - Политика именования групп применяется только к группам, созданным пользователями. Когда вы или другие администраторы используете Центр администрирования Exchange для создания групп рассылки, политика именования групп игнорируется и не применяется к имени группы.

  - Имена групп создаются без пробелов. Рекомендуется использовать знак подчеркивания (\_) или другой заполнитель между строками текста, атрибутами и именем группы.

  - При создании и редактировании группы рассылки можно использовать Windows PowerShell для переопределения политики именования групп. Дополнительные сведения см. в разделе [Переопределение политики именования групп рассылки](override-the-distribution-group-naming-policy-exchange-2013-help.md).

  - Сочетания клавиш для процедур, описанных в этой статье, приведены в статье [Сочетания клавиш в Центре администрирования Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

> [!TIP]  
> Возникли проблемы? Обратитесь за помощью к участникам форумов, посвященных Exchange. Посетите форумы по таким продуктам: <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> или <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>..


## Использование Центра администрирования Exchange для создания политики именования групп

1.  В центре администрирования Exchange выберите пункты **Группы** \> **Дополнительно** \> **Настроить политику имен групп**.

2.  В разделе **Политика именования групп** в раскрывающемся меню выберите **Атрибут** или **Текст**, чтобы настроить префикс.
    
      - **Атрибут**   Выберите атрибут и нажмите кнопку **ОК**.
    
      - **Текст**   Введите текстовую строку и нажмите кнопку **ОК**.
    
    Обратите внимание, что введенная текстовая строка (или выбранный атрибут) отображается в виде гиперссылки. Щелкните гиперссылку, чтобы изменить строку или атрибут.

3.  Чтобы добавить другие префиксы, нажмите кнопку **Добавить**.

4.  В качестве суффикса выберите в раскрывающемся меню **Атрибут** или **Текст**, после чего настройте суффикс.

5.  Чтобы добавить другие суффиксы, нажмите кнопку **Добавить**.
    
    После добавления префикса или суффикса отображается предварительный вид результата применения политики именования групп.

6.  Чтобы удалить префикс или суффикс из политики, нажмите кнопку **Удалить**![Удаление](images/JJ218693.37ba42c3-6f0d-42f3-b69b-ff912a99b5b7(EXCHG.150).gif "Удаление").

7.  Для добавления или удаления заблокированных слов выберите пункт **Заблокированные слова**.
    
      - Чтобы добавить слово в список, введите его и нажмите кнопку **Добавить**![Добавление символа для папок, исключенных при миграции электронной почты](images/JJ218693.444d5c83-821f-472c-b733-e84308e2531e(EXCHG.150).gif "Добавление символа для папок, исключенных при миграции электронной почты").
    
      - Чтобы удалить слово из списка, выберите его и нажмите кнопку **Удалить**.
    
      - Чтобы изменить существующее заблокированное слово, выберите его и нажмите кнопку **Редактировать**.

8.  Завершив настройку, нажмите кнопку **Сохранить**.

## Как проверить, что все получилось?

Чтобы проверить, успешно ли создана политика именования групп, выполните указанные ниже действия.

  - В центре администрирования Exchange выберите пункты **Группы** \> **Дополнительно** \> **Настроить политику имен групп**.
    
    На странице **Политика именования групп** политика, которую вы определили, указана в разделе **Предварительный просмотр политики**.

  - В Windows PowerShell выполните следующую команду для отображения политики именования групп:
    
        Get-OrganizationConfig | FL DistributionGroupNamingPolicy

