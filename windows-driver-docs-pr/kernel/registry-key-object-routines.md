---
title: 注册表项对象例程
description: 注册表项对象例程
ms.assetid: 9db6ff0d-8371-41bc-82c4-1bb56f5430f2
keywords:
- 注册表 WDK 内核，对象例程
- 驱动程序注册表信息 WDK 内核，对象例程
- 对象例程 WDK 内核
- 注册表-密钥对象 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebdc2f8e0fe0851e81b121d201af404a168ed7e0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188207"
---
# <a name="registry-key-object-routines"></a>注册表项对象例程





Windows executive 将注册表项表示为由对象管理器管理的管理器对象。  (有关对象管理器的详细信息，请参阅 [对象管理](managing-kernel-objects.md)。 ) 具体而言，每个密钥都有一个对象名称，您可以打开一个项的句柄。

用户模式应用程序相对于全局句柄（如 HKEY \_ 本地 \_ 计算机或 HKEY \_ 当前用户）访问密钥 \_ 。 但这些句柄不适用于内核模式代码。 相反，可以通过其对象名称引用密钥。 所有注册表项的根都是** \\ registry**对象。 全局句柄对应于** \\ 注册表**对象的后代，如下表所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>用户模式句柄</th>
<th>对应的对象名称</th>
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
<td><p>无内核模式等效项</p></td>
</tr>
<tr class="even">
<td><p>HKEY_CURRENT_USER</p></td>
<td><p>无简单的内核模式等效项，但请参阅 <a href="registry-run-time-library-routines.md" data-raw-source="[Registry Run-Time Library Routines](registry-run-time-library-routines.md)">注册表运行时库例程</a></p></td>
</tr>
</tbody>
</table>

 

驱动程序可以通过执行以下步骤来操作注册表项对象：

1.  打开注册表项对象的句柄。 有关详细信息，请参阅 [打开注册表项对象的句柄](opening-a-handle-to-a-registry-key-object.md)。

2.  通过调用适当的 **Zw*Xxx*密钥** 例程来执行预期的操作。 有关如何执行此操作的信息，请参阅 [使用注册表项对象的句柄](using-a-handle-to-a-registry-key-object.md)。

3.  通过调用 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)关闭句柄。

 

