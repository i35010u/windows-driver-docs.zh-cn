---
title: PcTimedWaveRtStreamSetState 规则 （音频）
description: PcTimedWaveRtStreamSetState 规则指定 ProtCls 微型端口驱动程序，可在所需的时间内通过 IMiniportWaveRTStream SetState 状态转换。
ms.assetid: D49869E0-9108-460B-8FA3-4FD99C3EA81E
ms.date: 05/21/2018
keywords:
- PcTimedWaveRtStreamSetState 规则 （音频）
topic_type:
- apiref
api_name:
- PcTimedWaveRtStreamSetState
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 90c240c6aa2b6c23846149ec452857557b6d0cbb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343873"
---
# <a name="pctimedwavertstreamsetstate-rule-audio"></a>PcTimedWaveRtStreamSetState 规则 （音频）


PcTimedWaveRtStreamSetState 规则指定 ProtCls 微型端口驱动程序，可通过状态转换[ **IMiniportWaveRTStream::SetState** ](https://msdn.microsoft.com/library/windows/hardware/ff536756)内所需的时间。

|              |       |
|--------------|-------|
| 驱动程序模型 | Audio |

|                                   |                                                                                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00072001) |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>若要验证此规则，请打开命令提示符窗口。 输入驱动程序验证程序命令，并指定<strong>/domain 音频</strong>。</p>
<p>例如：</p>
<p><strong>verifier /domain audio</strong> [<em>options</em>] <strong>/driver</strong> <em>&lt;yourdriver&gt;</em></p>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

 

 





