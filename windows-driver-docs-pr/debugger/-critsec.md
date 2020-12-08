---
title: critsec
description: Critsec 扩展显示关键部分。
keywords:
- critsec Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- critsec
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 736b4e6e0a4c2ce9366323c7181b3d7151322bd7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803327"
---
# <a name="critsec"></a>!critsec


**！ Critsec** 扩展显示关键部分。

```dbgsyntax
!critsec Address 
```

## <a name="span-idddk__critsec_dbgspanspan-idddk__critsec_dbgspanparameters"></a><span id="ddk__critsec_dbg"></span><span id="DDK__CRITSEC_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定临界区的十六进制地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关可显示关键部分信息的其他命令和扩展，请参阅 [显示关键部分](displaying-a-critical-section.md)。 有关关键部分的信息，请参阅 Microsoft Windows SDK 文档、Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，并将标记 Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

如果你不知道关键部分的地址，则应使用 [**！ ntsdexts**](-locks---ntsdexts-locks-.md) 扩展名。 这将显示已通过调用 **RtlInitializeCriticalSection** 初始化的所有关键部分。

以下是示例：

```dbgcmd
0:000> !critsec 3a8c0e9c

CritSec +3a8c0e9c at 3A8C0E9C
LockCount          1
RecursionCount     1
OwningThread       99
EntryCount         472
ContentionCount    1
*** Locked
```

 

 





