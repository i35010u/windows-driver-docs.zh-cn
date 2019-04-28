---
title: bugdump
description: Bugdump 扩展设置格式并显示 bug 检查回调缓冲区中包含的信息。
ms.assetid: cbea92de-e45b-416c-87f1-6faba95788d0
keywords:
- bugdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bugdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: da3053780adbfa1717a3adc30e3dda8fed390168
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334648"
---
# <a name="bugdump"></a>!bugdump


**！ Bugdump**扩展设置格式并显示 bug 检查回调缓冲区中包含的信息。

```dbgsyntax
    !bugdump [Component] 
```

## <a name="span-idddkbugdumpdbgspanspan-idddkbugdumpdbgspanparameters"></a><span id="ddk__bugdump_dbg"></span><span id="DDK__BUGDUMP_DBG"></span>参数


<span id="_______Component______"></span><span id="_______component______"></span><span id="_______COMPONENT______"></span> *组件*   
指定的回调数据将进行检查的组件。 如果省略，将显示所有 bug 检查回调数据。

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

有关详细信息，请参阅[读取 Bug 检查回调数据](reading-bug-check-callback-data.md)。

<a name="remarks"></a>备注
-------

此扩展可以仅在出现的 bug 检查后，或在调试时的内核模式崩溃转储文件。

*组件*参数对应于最后一个参数中使用[ **KeRegisterBugCheckCallback**](https://msdn.microsoft.com/library/windows/hardware/ff553105)。

保存回调数据的缓冲区在小内存转储中不可用。 这类缓冲区很内核内存转储和完全内存转储中存在。 但是，在 Windows XP SP1、 Windows Server 2003 和更高版本的 Windows 中，创建转储文件在驱动程序的前**BugCheckCallback**调用例程，并且因此这些缓冲区将包含这些写入的数据例程。

如果您正在执行的已崩溃系统的实时调试，将会显示所有回调数据。

 

 





