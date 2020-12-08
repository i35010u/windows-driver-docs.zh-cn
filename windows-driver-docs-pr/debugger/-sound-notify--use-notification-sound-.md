---
title: .sound_notify（使用通知音）
description: 当 WinDbg 进入等待命令状态时，.sound_notify 命令将导致播放声音。
keywords:
- .sound_notify (使用通知声音) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .sound_notify (Use Notification Sound)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e02f10eb8a12358b87db55559e812ff211686f70
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819897"
---
# <a name="sound_notify-use-notification-sound"></a>。声音 \_ 通知 (使用通知声音) 


当 WinDbg 进入等待命令状态时， **声音 \_ 通知** 命令会导致播放声音。

```dbgcmd
.sound_notify /ed 
.sound_notify /ef File 
.sound_notify /d 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="________ed______"></span><span id="________ED______"></span>**/ed**   
导致在 WinDbg 进入等待命令状态时播放默认的 Windows 警报声音。

<span id="________ef_______File______"></span><span id="________ef_______file______"></span><span id="________EF_______FILE______"></span>**/ef**  **** *文件*   
使指定文件中包含的声音在 WinDbg 进入等待命令状态时播放。

<span id="________d"></span><span id="________D"></span>**/d**  
禁止播放声音。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

此命令仅在 WinDbg 中可用，不能在脚本文件中使用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

 

 





