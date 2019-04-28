---
title: 回调
description: 回调扩展插件都会显示与指定的线程陷阱相关的回调数据。
ms.assetid: afbd7884-d63d-4e37-a437-91bc910a3ae2
keywords:
- 系统陷阱的的回调数据
- 回调 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- callback
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6d8eb5975d8075b68bfbd67bd42965fef24ceae9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336896"
---
# <a name="callback"></a>!callback


**！ 回调**扩展插件都会显示与指定的线程陷阱相关的回调数据。

```dbgsyntax
!callback Address [Number]
```

## <a name="span-idddkcallbackdbgspanspan-idddkcallbackdbgspanparameters"></a><span id="ddk__callback_dbg"></span><span id="DDK__CALLBACK_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定线程的十六进制的地址。 如果这是-1 或省略，则使用当前线程。

<span id="_______Number______"></span><span id="_______number______"></span><span id="_______NUMBER______"></span> *数量*   
指定所需的回调帧数。 在显示中记录了此帧。

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

 

此扩展命令仅用于基于 x86 的目标计算机。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关系统陷阱的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

如果系统未遇到系统陷阱，此扩展将不会生成有用的数据。

 

 





