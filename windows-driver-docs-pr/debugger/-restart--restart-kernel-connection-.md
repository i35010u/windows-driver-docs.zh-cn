---
title: .restart（重启内核连接）
description: .Restart 命令重新启动内核连接。不要混淆.restart （重新启动目标应用程序） 命令中，只能在用户模式中运行此命令。
ms.assetid: 2c81625b-d75f-4c5f-9437-9619bf33b500
keywords:
- .restart （重新启动内核连接） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .restart (Restart Kernel Connection)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b9a57ecd03ed93ca6dc2c2a4f4882737e33f1122
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335706"
---
# <a name="restart-restart-kernel-connection"></a>.restart（重启内核连接）


**.Restart**命令重新启动内核连接。

不要将使用此命令相混淆[ **.restart （重新启动目标应用程序）** ](-restart--restart-target-application-.md)命令，仅在用户模式下工作。

```dbgcmd
.restart 
```

## <span id="ddk_meta_restart_kernel_connection_dbg"></span><span id="DDK_META_RESTART_KERNEL_CONNECTION_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

可以使用 **.restart**命令仅在 KD 中。

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

有关重新建立与目标的联系人详细信息，请参阅[与目标计算机同步](synchronizing-with-the-target-computer.md)。

<a name="remarks"></a>备注
-------

**.Restart**命令是类似于[ **CTRL + R （重新同步）** ](ctrl-r--re-synchronize-.md)命令时，不同之处在于 **.restart**中更广泛其效果。 此命令相当于结束调试器，然后将新的调试器附加到目标计算机。

**.Restart**执行时，命令是最有用[remote.exe 通过远程调试](remote-debugging-through-remote-exe.md)和结束和重新启动调试器可能会很困难。 但是，不能使用 **.restart**从调试客户端，如果您正在执行通过调试器的远程调试。

 

 





