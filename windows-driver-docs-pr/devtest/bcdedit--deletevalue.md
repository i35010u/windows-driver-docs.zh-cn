---
title: BCDEdit /deletevalue
description: BCDEdit /deletevalue 命令删除，或从 Windows 引导配置数据存储 (BCD) 中删除的启动项选项 （和其值）。
ms.assetid: 70833A12-B1F7-4AF6-952F-02A70718E870
ms.date: 05/21/2018
keywords:
- BCDEdit /deletevalue 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /deletevalue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f229284215ca334b4925d4bc83db5220c43b45d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327349"
---
# <a name="bcdedit-deletevalue"></a>BCDEdit /deletevalue


**BCDEdit /deletevalue**命令删除，或从 Windows 引导配置数据存储 (BCD) 中删除的启动项选项 （和其值）。 使用**BCDEdit /deletevalue**命令删除已添加使用的选项[ **BCDEdit /set** ](bcdedit--set.md)命令。 
``` syntax
     bcdedit  /deletevalue [{ID}] datatype  

   
```

若要删除一个启动选项值，已设置该值，请使用**BCDEdit /deletevalue**命令。 使用的常见方案**BCDEdit /deletevalue**命令是在测试和调试驱动程序时删除启动条目选项。 

例如，如果您使用[ **BCDEdit /set** ](bcdedit--set.md)若要更改**groupsize**处理器组选项的新值用于测试目的，可以使用**BCDEdit /deletevalue**若要删除的新值并键入以下命令来恢复为默认值。 请注意，你必须重启计算机以使更改生效。

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
<td align="left"><p>Windows Vista</p></td>
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
 

 





