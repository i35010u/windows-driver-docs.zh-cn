---
title: devhandles
description: Devhandles 扩展显示指定设备打开的句柄。
ms.assetid: a473dd58-1571-4969-b8b7-f7a71128d824
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
ms.openlocfilehash: 3145c0e050e4bf8cfc090a856dd5b39489209d8f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568258"
---
# <a name="devhandles"></a>!devhandles


**！ Devhandles**扩展显示指定设备打开的句柄。

```dbgcmd
!devhandles Address 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定要显示打开的句柄其设备的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

若要显示完整的句柄的信息，此扩展要求私有符号。

可以使用获取的设备对象的地址[ **！ drvobj** ](-drvobj.md)或[ **！ devnode** ](-devnode.md)扩展。

以下是截断的示例：

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

 

 





