---
title: icpleak
description: Icpleak 扩展在系统中检查包含最多已排队条目的对象的所有 i/o 完成对象。
keywords:
- I/o 完成
- icpleak Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- icpleak
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: afa10f09f9bfc87394eaa9f52647dfbd9900fc11
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826765"
---
# <a name="icpleak"></a>!icpleak


**！ Icpleak** extension 检查系统中具有最大排队条目数的对象的所有 i/o 完成对象。

```dbgcmd
!icpleak [HandleFlag]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______HandleFlag______"></span><span id="_______handleflag______"></span><span id="_______HANDLEFLAG______"></span>*HandleFlag*   
如果设置了此标志，则显示内容还包括所有进程，其中包含具有最多已排队条目的对象的句柄。

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 i/o 完成端口的信息，请参阅 Russinovich 和 David 的 *Microsoft Windows 内部机制* 。 

<a name="remarks"></a>备注
-------

当 i/o 完成池中存在泄漏时，此扩展很有用。 如果进程通过调用 [**postqueuedcompletionstatus 期间**](/windows/desktop/FileIO/postqueuedcompletionstatus)来分配 i/o 完成数据包，但未调用 [**GetQueuedCompletionStatus**](/windows/win32/api/ioapiset/nf-ioapiset-getqueuedcompletionstatus) 来释放它们，或者进程正在将完成项排队到端口，但没有线程检索这些项，则可能会发生 i/o 完成池溢出。 若要检测泄漏，请运行 [**！ poolused**](-poolused.md) extension 并检查 ICP pool 标记的值。 如果用于 ICP 标记的池使用非常重要，则可能会发生泄露。

此扩展仅适用于系统维护类型列表的情况。 如果设置了 *HandleFlag* 并且系统有多个进程，则此扩展将需要较长时间才能运行。

您可以通过在 WinDbg) 中按 CTRL + BREAK (或在 KD) 中按 CTRL + C (随时停止。

 

