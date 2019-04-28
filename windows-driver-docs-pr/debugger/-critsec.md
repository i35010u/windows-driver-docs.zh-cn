---
title: critsec
description: Critsec 扩展显示关键部分。
ms.assetid: 7e30efd5-2bdc-420c-b3ed-504280ddd8f7
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
ms.openlocfilehash: 37171ddd8dc73228f783bb2966c85a0858718336
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336872"
---
# <a name="critsec"></a>!critsec


**！ Critsec**扩展显示关键部分。

```dbgsyntax
!critsec Address 
```

## <a name="span-idddkcritsecdbgspanspan-idddkcritsecdbgspanparameters"></a><span id="ddk__critsec_dbg"></span><span id="DDK__CRITSEC_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定关键部分的十六进制的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关其他命令和扩展，可以显示关键部分的信息，请参阅[显示关键节](displaying-a-critical-section.md)。 有关关键部分的信息，请参阅 Microsoft Windows SDK 文档，Windows Driver Kit (WDK) 文档，并*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。

<a name="remarks"></a>备注
-------

如果不知道的关键部分地址，则应使用[ **！ ntsdexts.locks** ](-locks---ntsdexts-locks-.md)扩展。 这将显示所有已通过调用来初始化的关键部分**RtlInitializeCriticalSection**。

下面是一个示例：

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

 

 





