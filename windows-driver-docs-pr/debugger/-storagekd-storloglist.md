---
title: storagekd.storloglist
description: Storagekd.storloglist 扩展显示 Storport 适配器的内部日志条目。
ms.assetid: 6308DDEF-8AB0-4D16-9245-3046114D5173
keywords:
- storagekd.storloglist Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- storagekd.storloglist
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bad0a2d5c26f63bca91ef6cc546843c7a7eaa81d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565779"
---
# <a name="storagekdstorloglist"></a>!storagekd.storloglist


**！ Storagekd.storloglist**扩展显示 Storport 适配器的内部日志项。

```dbgcmd
!storagekd.storloglist <Address> [<starting_entry> [<ending_entry>]] [L <count>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定 Storport 适配器设备扩展或设备对象的地址。

<span id="_______starting_entry______"></span><span id="_______STARTING_ENTRY______"></span> *启动\_条目*   
要显示的区域中的开始条目中。 如果未指定，上次*计数*不会显示条目。

<span id="_______ending_entry______"></span><span id="_______ENDING_ENTRY______"></span> *ending\_entry*   
中要显示的范围的结束条目。 如果未指定，*计数*将显示条目，从指定的项目开始*启动\_条目*。

<span id="_______count______"></span><span id="_______COUNT______"></span> *count*   
若要显示的项计数。 如果未指定，使用值为 50。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 8 及更高版本</strong></p></td>
<td align="left"><p>Storagekd.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

下面是举例 **！ storagekd.storloglist**显示：

**0: kd&gt; !storagekd.storloglist ffffe0010f5e01a0**

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

 

 





