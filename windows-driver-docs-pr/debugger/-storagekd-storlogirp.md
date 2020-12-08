---
title: storagekd.storlogirp
description: Storagekd. storlogirp 扩展显示已为提供的 IRP 筛选的适配器的 Storport 内部日志条目。
keywords:
- storagekd storlogirp Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storlogirp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5dce22b1bfe4898934490b107f4d38160ba1e755
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819397"
---
# <a name="storagekdstorlogirp"></a>!storagekd.storlogirp


**！ Storagekd; storlogirp** 扩展显示已为提供的 IRP 筛选的适配器的 Storport 内部日志条目。

```dbgcmd
!storagekd.storlogirp <Address> <irp> [<starting_entry> [<ending_entry>]] [L <count>]  
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 Storport 适配器设备扩展或设备对象的地址。

<span id="_______irp______"></span><span id="_______IRP______"></span>*irp*   
要查找的 IRP。

<span id="_______starting_entry______"></span><span id="_______STARTING_ENTRY______"></span>*正在启动 \_ 条目*   
范围中要显示的开始项。 如果未指定，则将显示最后一个 *计数* 条目。

<span id="_______ending_entry______"></span><span id="_______ENDING_ENTRY______"></span>*结束 \_ 项*   
要显示的范围中的结束条目。 如果未指定，则将显示 " *计数* " 条目，从 "开始" *\_ 条目* 指定的项目开始。

<span id="_______count______"></span><span id="_______COUNT______"></span>*计数*   
要显示的项的计数。 如果未指定，则使用值50。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 8 及更高版本</strong></p></td>
<td align="left"><p>Storagekd.dll</p></td>
</tr>
</tbody>
</table>

 

 

 





