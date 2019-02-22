---
title: 注册表项对象例程
description: 注册表项对象例程
ms.assetid: 9db6ff0d-8371-41bc-82c4-1bb56f5430f2
keywords:
- 注册表 WDK 内核，对象例程
- 驱动程序注册表信息 WDK 内核，对象例程
- 对象例程 WDK 内核
- 注册表项对象 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 364fbd4055f5399d80f93ea8bfba5c695fe7edd7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524628"
---
# <a name="registry-key-object-routines"></a>注册表项对象例程





Windows 高级管理人员管理的对象管理器 executive 对象作为表示注册表项。 (有关对象管理器的详细信息，请参阅[对象管理](managing-kernel-objects.md)。)具体而言，所有密钥都有一个对象的名称，并可以打开密钥的句柄。

用户模式应用程序访问密钥相对于全局句柄，例如 HKEY\_本地\_机或 HKEY\_当前\_用户。 但是，这些句柄不可用到内核模式代码。 而是指一个键按对象名称。 所有注册表项的根是**\\注册表**对象。 全局句柄对应的后代**\\注册表**对象，如以下表中所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用户模式下句柄</th>
<th>相应对象名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HKEY_LOCAL_MACHINE</p></td>
<td><p><strong>\Registry\Machine</strong></p></td>
</tr>
<tr class="even">
<td><p>HKEY_USERS</p></td>
<td><p><strong>\Registry\User</strong></p></td>
</tr>
<tr class="odd">
<td><p>HKEY_CLASSES_ROOT</p></td>
<td><p>没有内核模式的等效项</p></td>
</tr>
<tr class="even">
<td><p>HKEY_CURRENT_USER</p></td>
<td><p>没有简单的内核模式等效项，但看到<a href="registry-run-time-library-routines.md" data-raw-source="[Registry Run-Time Library Routines](registry-run-time-library-routines.md)">注册表运行时库例程</a></p></td>
</tr>
</tbody>
</table>

 

驱动程序可以通过执行以下步骤操作注册表项对象：

1.  打开注册表项对象的句柄。 有关详细信息，请参阅[打开注册表项对象的句柄](opening-a-handle-to-a-registry-key-object.md)。

2.  执行预期的操作通过调用适当**Zw*Xxx*密钥**例程。 有关如何执行此操作的信息，请参阅[使用注册表项对象的句柄](using-a-handle-to-a-registry-key-object.md)。

3.  通过调用关闭句柄[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)。

 

 




