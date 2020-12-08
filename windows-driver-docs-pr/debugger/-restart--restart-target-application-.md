---
title: .restart（重启目标应用程序）
description: Restart 命令重新启动目标应用程序。请勿将此命令与. restart (重新启动内核连接) 命令，该命令仅在内核模式下运行。
keywords:
- 。重新启动 (重新启动目标应用程序) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .restart (Restart Target Application)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d29dd6c14fd989aea9acdb96289816408b6eeaa7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790091"
---
# <a name="restart-restart-target-application"></a>.restart（重启目标应用程序）


**Restart** 命令重新启动目标应用程序。

请勿将此命令与 [**. restart (重新启动内核连接)**](-restart--restart-kernel-connection-.md) 命令，该命令仅在内核模式下运行。

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
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅限实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关如何发出此命令并概述相关命令的详细信息，请参阅 [控制目标](controlling-the-target.md)。

<a name="remarks"></a>备注
-------

如果调试器最初创建了应用程序，则 CDB 和 WinDbg 可以重新启动目标应用程序。 即使目标应用程序已关闭，你也可以使用 " **重新启动** " 命令。

但是，如果应用程序正在运行，并且稍后将调试器附加到该进程，则 **restart** 命令不起作用。

进程重新启动后，它会立即中断到调试器。

在 WinDbg 中，使用 " [视图 |WinDbg 命令行](view---windbg-command-line.md) 命令（如果你从 WinDbg 命令提示符启动了目标，并且想要在决定 **是否使用之前** 查看此命令行）。

 

 





