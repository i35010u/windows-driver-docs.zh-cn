---
title: storagekd.storloglist
description: Storagekd. storloglist 扩展显示 Storport 适配器的内部日志条目。
keywords:
- storagekd storloglist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storloglist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 031b3d91300412026dcd67006239b893e5f1cb72
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817011"
---
# <a name="storagekdstorloglist"></a>!storagekd.storloglist


**！ Storagekd storloglist** 扩展显示 Storport 适配器的内部日志条目。

```dbgcmd
!storagekd.storloglist <Address> [<starting_entry> [<ending_entry>]] [L <count>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 Storport 适配器设备扩展或设备对象的地址。

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

 

<a name="remarks"></a>备注
-------

下面是 **！ storloglist** 显示的示例 storagekd：

**0： kd &gt; ！ storagekd. storloglist ffffe0010f5e01a0**

```dbgcmd
Storport RaidLogList
    Circular buffer location:  0xffffe0010f5e1720
    Total logs written: 8
    Displaying entries 0 through 7
    ---------------------------------------------------------------------
    [0]_[23:04:20.521] ResumeDevice.......... Caller: storport!RaidUnitPauseTimerDpcRoutine+0x28 (fffff800`fb4d0b28), P/P/T/L: 0/0/0/0, Pause count: 0, Resumed: True
    [1]_[23:04:20.646] ResumeDevice.......... Caller: storport!RaidUnitPauseTimerDpcRoutine+0x28 (fffff800`fb4d0b28), P/P/T/L: 0/0/0/0, Pause count: 0, Resumed: True
    [2]_[23:04:20.646] SpPauseDevice......... Caller: iaStorAV!RpiPauseDevice+0x67 (fffff800`fb70554f), P/T/L: 3/0/0, Timeout: 180, Adapter: 0xffffe0010f5e01a0
    [3]_[23:04:20.646] PauseDevice........... Caller: storport!StorPortPauseDevice+0x2f6 (fffff800`fb4b52d6), P/P/T/L: 0/3/0/0, Pause count: 1
    [4]_[23:04:20.646] SpResumeDevice........ Caller: iaStorAV!RpiResumeDevice+0x5f (fffff800`fb7055fb), P/T/L: 3/0/0, Adapter: 0xffffe0010f5e01a0
    [5]_[23:04:20.646] ResumeDevice.......... Caller: storport!StorPortResumeDevice+0x19 (fffff800`fb4aa23f), P/P/T/L: 0/3/0/0, Pause count: 0, Resumed: True
    [6]_[23:04:20.646] SpPauseDevice......... Caller: iaStorAV!RpiPauseDevice+0x67 (fffff800`fb70554f), P/T/L: 3/0/0, Timeout: 180, Adapter: 0xffffe0010f5e01a0
    [7]_[23:04:20.646] PauseDevice........... Caller: storport!StorPortPauseDevice+0x2f6 (fffff800`fb4b52d6), P/P/T/L: 0/3/0/0, Pause count: 1
```

 

 





