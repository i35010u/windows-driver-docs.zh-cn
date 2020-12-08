---
title: devhandles
description: Devhandles 扩展显示指定设备的开放句柄。
keywords:
- devhandles Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- devhandles
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e8da8ec4acd46ee0ef0220a0b6823b13035a5fac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815249"
---
# <a name="devhandles"></a>!devhandles


**！ Devhandles** extension 显示指定设备的开放句柄。

```dbgcmd
!devhandles Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要为其显示打开句柄的设备的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

若要显示完整的句柄信息，此扩展需要私有符号。

可以使用 [**！ drvobj**](-drvobj.md) 或 [**！ devnode**](-devnode.md) 扩展来获取设备对象的地址。

下面是一个被截断的示例：

```dbgcmd
lkd> !devhandles 0x841153d8

Checking handle table for process 0x840d3940
Handle table at 95fea000 with 578 Entries in use

Checking handle table for process 0x86951d90
Handle table at 8a8ef000 with 28 Entries in use

...

Checking handle table for process 0x87e63650
Handle table at 947bc000 with 308 Entries in use

Checking handle table for process 0x87e6f4f0
00000000: Unable to read handle table
```

 

 





