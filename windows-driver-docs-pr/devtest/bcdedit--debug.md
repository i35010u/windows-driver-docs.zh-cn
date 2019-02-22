---
title: BCDEdit /debug
description: /Debug 启动选项启用或禁用内核调试与指定的启动项目或当前引导条目相关联的 Windows 操作系统。
ms.assetid: 013ec247-f2ca-4918-9dfa-8b1348d0b4e5
ms.date: 07/02/2018
keywords:
- BCDEdit /debug 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /debug
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a2893cd491e6d910924f3557d5e52897363cf12d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545954"
---
# <a name="bcdedit-debug"></a>BCDEdit /debug


**/Debug**启动选项启用或禁用内核调试与指定的启动项目或当前引导条目相关联的 Windows 操作系统。

> [!NOTE]
> 设置 BCDEdit 选项之前，您可能需要禁用或暂停 BitLocker 和安全启动的计算机上。

 

``` syntax
    bcdedit /debug [{ID}] { on | off } 

   
```

<a name="parameters"></a>参数
----------

**{**<em>ID</em>**}**   
**{**<em>ID</em>**}** 是与启动条目关联的 GUID。 如果未指定 **{**<em>ID</em>**}**，命令将修改当前处于活动状态的操作系统。 如果指定的启动项，则与启动项关联的 GUID 必须括在大括号 **{}**。

 **on**   
启用内核调试的指定的启动项目。 如果未指定的启动项，则为当前操作系统启用内核调试。

**off**   
禁用内核调试程序的指定的启动项目。 如果未指定的启动项，则为当前操作系统禁用内核调试。

### <a name="comments"></a>备注

**/Debug**启动选项可启用内核调试特定的启动项。 使用 **/dbgsettings**选项配置的调试要使用连接和连接参数的类型。 如果没有 **/dbgsettings**指定为启动项目中，将使用全局调试设置。 下表中列出的全局设置的默认值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">dbgsetting 参数</th>
<th align="left">默认值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>连接类型</p></td>
<td align="left"><p>序列</p></td>
</tr>
<tr class="even">
<td align="left"><p>调试端口</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>波特率</p></td>
<td align="left"><p>115200</p></td>
</tr>
</tbody>
</table>

 

有关 Windows 调试工具的信息，请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)。 有关设置和配置内核模式调试会话，请参阅[设置了内核模式调试手动](https://msdn.microsoft.com/library/windows/hardware/hh439378)。

以下示例启用内核调试的启动项目的 49916baf-0e08-11db-9af4-000bdbd316a0 的 guid。

```
bcdedit /debug {49916baf-0e08-11db-9af4-000bdbd316a0} on 
```

在以下示例中，第一个命令将设置全局调试器设置 USB 2.0 和名称目标 myVistaTarget。 第二个命令为当前会话启用调试器。

```
bcdedit /dbgsettings usb targetname:myVistaTarget 
bcdedit /debug ON 
```

 

 





