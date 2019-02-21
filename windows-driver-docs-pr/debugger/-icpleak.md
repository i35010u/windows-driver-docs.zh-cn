---
title: icpleak
description: Icpleak 扩展将检查所有 I/O 完成对象具有的最大排队的条目数的对象的系统中。
ms.assetid: 8644a41a-44da-47bc-94ef-5024bb457c7d
keywords:
- I/O 完成
- icpleak Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- icpleak
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b9216d5506ceaf34967a6e800c43ad59ac78288
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522045"
---
# <a name="icpleak"></a>！ icpleak


**！ Icpleak**扩展插件将检查所有 I/O 完成对象具有的最大排队的条目数的对象的系统中。

```dbgcmd
!icpleak [HandleFlag]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______HandleFlag______"></span><span id="_______handleflag______"></span><span id="_______HANDLEFLAG______"></span> *HandleFlag*   
如果设置此标志，显示内容还包括具有最大数量的已排队的项的对象的句柄的所有进程。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关 I/O 完成端口的信息，请参阅*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这本书不可能在某些语言和国家/地区中可用。）

<a name="remarks"></a>备注
-------

此扩展时，I/O 完成池中没有泄漏。 一个过程通过调用分配 I/O 完成数据包时，可能发生 I/O 完成池泄漏[ **PostQueuedCompletionStatus**](https://msdn.microsoft.com/library/windows/desktop/aa365458)，但不是调用[ **GetQueuedCompletionStatus** ](https://msdn.microsoft.com/library/windows/desktop/aa364986)来释放它们，或者当进程正在排队完成条目的端口，但没有线程检索条目。 若要检测运行泄漏[ **！ poolused** ](-poolused.md)扩展以及检查 ICP 值池标记。 如果池使用的 ICP 标记非常重要，可能发生泄漏。

此扩展仅适用于系统维护类型列表。 如果*HandleFlag*设置和系统有多的进程，此扩展将会很长时间才能运行。

可以随时停止通过按 CTRL + BREAK （在 WinDbg) 或 CTRL + C （中 KD)。

 

 





