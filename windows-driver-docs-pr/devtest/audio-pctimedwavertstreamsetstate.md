---
title: 'PcTimedWaveRtStreamSetState 规则 (音频) '
description: PcTimedWaveRtStreamSetState 规则指定 ProtCls 微型端口驱动程序在所需时间内通过 IMiniportWaveRTStream SetState 进行状态转换。
ms.date: 05/21/2018
keywords:
- 'PcTimedWaveRtStreamSetState 规则 (音频) '
topic_type:
- apiref
api_name:
- PcTimedWaveRtStreamSetState
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 614ef576b938bd6dcd9cf75aab6e0aac27e727b4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820887"
---
# <a name="pctimedwavertstreamsetstate-rule-audio"></a>PcTimedWaveRtStreamSetState 规则 (音频) 


PcTimedWaveRtStreamSetState 规则指定 ProtCls 微型端口驱动程序通过 [**IMiniportWaveRTStream：： SetState**](/previous-versions/windows/hardware/drivers/ff536756(v=vs.85)) 在所需时间内进行状态转换。

**驱动程序模型：音频**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00072001) 


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
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定 <strong>/domain 音频</strong>。</p>
<p>例如：</p>
<p><strong>verifier/domain 音频</strong>[<em>options</em>] <strong>/driver</strong> <em> &lt; yourdriver &gt; </em></p>
<p>有关详细信息，请参阅<a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a>。</p></td>
</tr>
</tbody>
</table>

 

