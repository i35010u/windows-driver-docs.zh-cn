---
title: .detach（从进程分离）
description: .Detach 命令将结束调试会话，但保留运行任何用户模式目标应用程序。
ms.assetid: 4f0fbd8b-3037-4549-99da-be40a091a363
keywords:
- .detach （从进程分离） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .detach (Detach from Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9b16176b96fe6cc3acda159c547c2120555b42fe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336850"
---
# <a name="detach-detach-from-process"></a>.detach（从进程分离）


**.Detach**命令将结束调试会话，但会使任何用户模式下的目标应用程序运行。

```dbgcmd
.detach [ /h | /n ]
```

## <a name="span-idddkmetadetachfromprocessdbgspanspan-idddkmetadetachfromprocessdbgspanparameters"></a><span id="ddk_meta_detach_from_process_dbg"></span><span id="DDK_META_DETACH_FROM_PROCESS_DBG"></span>参数


<span id="________h______"></span><span id="________H______"></span> **/h**   
将继续并标记为已处理的任何未完成的调试事件。 这是默认设置。

<span id="________n______"></span><span id="________N______"></span> **/n**   
任何未完成的调试事件将可继续运行而无需被标记为已处理。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

用于实时用户模式下调试，此命令仅支持在 Windows XP 和更高版本的 Windows 中。

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
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此命令将结束调试会话中任何以下方案：

-   在调试的用户模式或内核模式转储文件。

-   在调试实时用户模式下的目标。

-   在 noninvasively 调试用户模式下的目标。

如果仅要调试单个目标，调试器将返回到休眠模式后它分离。

你是否[调试多个目标](debugging-multiple-targets.md)，则在调试会话将继续执行的剩余目标。

 

 





