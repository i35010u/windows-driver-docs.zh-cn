---
title: openmaps
description: Openmaps 扩展显示引用的缓冲区控制块 (BCBs) 和虚拟地址控制块 (VACBs) 指定的共享的缓存映射。
ms.assetid: 4ecce331-c18e-462a-807a-b8929059b897
keywords:
- BCB （缓冲区控制块）
- VACB （虚拟地址控制块）
- 共享的缓存映射
- 缓存管理器
- openmaps Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- openmaps
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2496778b2ec95bd3941420766cf0087c241d0e78
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334437"
---
# <a name="openmaps"></a>!openmaps


**！ Openmaps**扩展显示引用的缓冲区控制块 (BCBs) 和虚拟地址控制块 (VACBs) 为指定的共享的缓存映射。

```dbgcmd
!openmaps Address [Flag]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定共享的缓存映射的地址。

<span id="_______Flag______"></span><span id="_______flag______"></span><span id="_______FLAG______"></span> *Flag*   
确定显示哪个控制块。 如果*标志*是**1**，调试器将显示所有控制块。 如果*标志*是**0**，调试器将显示仅引用控制块。 默认值是**0**。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

缓存管理有关的信息，请参阅 Microsoft Windows SDK 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

有关其他缓存管理扩展的信息，请参阅[ **！ cchelp** ](-cchelp.md)扩展。

 

 





