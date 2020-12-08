---
title: .restart（重启内核连接）
description: Restart 命令重新启动内核连接。请勿将此命令与. restart (Restart 目标应用程序) 命令，该命令仅在用户模式下运行。
keywords:
- 。重新启动 (重新启动内核连接) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .restart (Restart Kernel Connection)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cc268a5adcdb93689540aea1bbb9a7959bdd2588
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795189"
---
# <a name="restart-restart-kernel-connection"></a>.restart（重启内核连接）


**Restart** 命令重新启动内核连接。

请勿将此命令与 [**. restart (Restart 目标应用程序)**](-restart--restart-target-application-.md) 命令，该命令仅在用户模式下运行。

```dbgcmd
.restart 
```

## <span id="ddk_meta_restart_kernel_connection_dbg"></span><span id="DDK_META_RESTART_KERNEL_CONNECTION_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

只能在 KD 中使用 **. restart** 命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>仅限内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关重新建立与目标的联系的详细信息，请参阅 [与目标计算机同步](synchronizing-with-the-target-computer.md)。

<a name="remarks"></a>备注
-------

**重启** 命令类似于 [**CTRL + R (重新同步)**](ctrl-r--re-synchronize-.md)命令，不同之处在于，**重启** 更广泛地影响。 此命令等效于结束调试器，然后将新的调试器附加到目标计算机。

当 [通过 remote.exe执行远程调试](remote-debugging-through-remote-exe.md)时，**重启** 命令最有用，并且结束并重新启动调试器可能会很困难。 但是，如果要通过调试器执行远程调试，则不能使用。从调试客户端 **重新启动** 。

 

 





