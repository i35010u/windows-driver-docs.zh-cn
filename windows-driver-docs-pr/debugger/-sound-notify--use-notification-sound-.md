---
title: .sound_notify （使用通知声音）
description: .Sound_notify 命令使 WinDbg 进入等待的命令状态时要播放的声音。
ms.assetid: 72ef33ea-1c75-4add-80eb-a0d824571948
keywords:
- .sound_notify （使用通知声音） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .sound_notify (Use Notification Sound)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fb846550287246a942cbd36da74bfadf122013a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544845"
---
# <a name="soundnotify-use-notification-sound"></a>.sound\_通知 （使用通知声音）


**.Sound\_通知**命令使 WinDbg 进入等待的命令状态时要播放的声音。

```dbgcmd
.sound_notify /ed 
.sound_notify /ef File 
.sound_notify /d 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="________ed______"></span><span id="________ED______"></span> **/ed**   
将导致默认 Windows 警报声 WinDbg 进入等待的命令状态时要播放。

<span id="________ef_______File______"></span><span id="________ef_______file______"></span><span id="________EF_______FILE______"></span> **/ef** **** *文件*   
会导致包含在指定的文件，WinDbg 将进入等待的命令状态时要播放的声音。

<span id="________d"></span><span id="________D"></span> **/d**  
禁用的声音播放。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

此命令仅在 WinDbg 中可用，并能在脚本文件。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

 

 





