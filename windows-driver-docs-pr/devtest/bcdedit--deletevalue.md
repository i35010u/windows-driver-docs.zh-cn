---
title: BCDEdit /deletevalue
description: BCDEdit/deletevalue 命令从 Windows 启动配置数据存储 (BCD) 中删除或删除启动项选项 (及其值) 。
ms.date: 05/21/2018
keywords:
- BCDEdit/deletevalue 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /deletevalue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6f660e814c909446ea1be3154aa5e64b7c4214f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817494"
---
# <a name="bcdedit-deletevalue"></a>BCDEdit /deletevalue

**BCDEdit/deletevalue** 命令从 Windows 启动配置数据存储 (BCD) 中删除或删除启动项选项 (及其值) 。 使用 **bcdedit/deletevalue** 命令删除使用 [**bcdedit/set**](bcdedit--set.md) 命令添加的选项。

``` syntax
bcdedit  /deletevalue [{ID}] datatype  
```

> [!NOTE]
> 删除 BCDEdit 选项之前，你可能需要在计算机上禁用或暂停 BitLocker 和安全启动。

若要删除已设置的启动选项值，请使用 **BCDEdit/deletevalue** 命令。 使用 **BCDEdit/deletevalue** 命令的常见方案是在测试和调试驱动程序时删除启动项选项。 

例如，如果使用 [**bcdedit/set**](bcdedit--set.md) 将 **groupsize** processor group 选项更改为新值以用于测试目的，则可以使用 **bcdedit/deletevalue** 删除新值，并通过键入以下命令恢复为默认值。 请注意，必须重新启动计算机才能使更改生效。

``` syntax
bcdedit /deletevalue groupsize
```

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows Vista</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>Windows Server 2008</p></td>
</tr>
</tbody>
</table>

<a name="see-also"></a>请参阅
--------

[**BCDEdit /set**](bcdedit--set.md)
