---
title: .suspend_ui（挂起 WinDbg 接口）
description: .Suspend_ui 命令挂起 WinDbg 调试信息窗口的刷新。
ms.assetid: 7fa6ca5c-f960-49eb-b6f0-a6f2d454984f
keywords:
- .suspend_ui （挂起 WinDbg 界面） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .suspend_ui (Suspend WinDbg Interface)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 27f259a66db96243b6bdb95910189d4747cb1ed1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338780"
---
# <a name="suspendui-suspend-windbg-interface"></a>.suspend\_ui （挂起 WinDbg 接口）


**.Suspend\_ui**命令挂起的 WinDbg 调试信息窗口刷新。

```dbgcmd
.suspend_ui 0 
.suspend_ui 1 
.suspend_ui 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______0______"></span> **0**   
挂起 WinDbg 调试信息窗口的刷新。

<span id="_______1______"></span> **1**   
启用 WinDbg 调试信息窗口的刷新。

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
<td align="left"><p>内核模式下</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关调试的信息窗口的信息，请参阅[使用调试信息 Windows](using-debugging-information-windows.md)。

<a name="remarks"></a>备注
-------

不带任何参数， **.suspend\_ui**显示是否将调试信息 windows 目前处于挂起状态。

默认情况下，调试窗口是的信息刷新每次更改显示它们的信息。

挂起的这些窗口刷新可以加快 WinDbg 在一系列的快速操作-例如，跟踪或步进中快速连续多次时。

 

 





