---
title: .restart（重启目标应用程序）
description: .Restart 命令重新启动目标应用程序。不要混淆.restart （重新启动内核连接） 命令中，只能在内核模式中运行此命令。
ms.assetid: abfa1817-41d8-4bb2-a6d2-e9c9027b50df
keywords:
- .restart （重新启动目标应用程序） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .restart (Restart Target Application)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 77576f22e1ac1fbb039369494a8683ccfa1bb582
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338911"
---
# <a name="restart-restart-target-application"></a>.restart（重启目标应用程序）


**.Restart**命令重新启动目标应用程序。

不要将使用此命令相混淆[ **.restart （重新启动内核连接）** ](-restart--restart-kernel-connection-.md)命令，只能在内核模式中运行。

```dbgcmd
.restart 
```

## <span id="ddk_meta_restart_target_application_dbg"></span><span id="DDK_META_RESTART_TARGET_APPLICATION_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关如何发出此命令，并概述的相关命令的详细信息，请参阅[控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

如果调试器最初创建应用程序，CDB 和 WinDbg 可以重新启动目标应用程序。 可以使用 **.restart**命令即使目标应用程序已关闭。

但是，如果应用程序运行和调试程序更高版本附加到进程 **.restart**命令不起作用。

该进程重新启动后，它将立即进入调试器。

在 WinDbg 中，使用[视图 |WinDbg 命令行](view---windbg-command-line.md)命令在 WinDbg 命令提示符下启动你的目标，并且你想要决定是否使用之前，请查看此命令行 **.restart**。

 

 





