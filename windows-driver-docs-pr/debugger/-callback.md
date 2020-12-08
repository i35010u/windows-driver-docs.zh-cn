---
title: 回调 (callback)
description: 回调扩展显示与指定线程的陷阱相关的回调数据。
keywords:
- 系统陷阱的回叫数据
- 回调 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- callback
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ff9ba94d85dffeb59975fb4a514f48571b246203
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814103"
---
# <a name="callback"></a>!callback


**！回调** 扩展显示与指定线程的陷阱相关的回调数据。

```dbgsyntax
!callback Address [Number]
```

## <a name="span-idddk__callback_dbgspanspan-idddk__callback_dbgspanparameters"></a><span id="ddk__callback_dbg"></span><span id="DDK__CALLBACK_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定线程的十六进制地址。 如果此项为-1 或省略，则使用当前线程。

<span id="_______Number______"></span><span id="_______number______"></span><span id="_______NUMBER______"></span>*编号*   
指定所需的回叫帧的数目。 此帧显示在显示中。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

此扩展命令只能与基于 x86 的目标计算机一起使用。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关系统陷阱的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，Mark Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

如果系统没有遇到系统陷阱，此扩展将不会产生有用的数据。

 

 





