---
title: .endpsrv（结束进程服务器）
description: Endpsrv 命令使当前进程服务器或 KD 连接服务器关闭。
keywords:
- endpsrv (结束进程服务器) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .endpsrv (End Process Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7465fc9e256b9a008e39b5e6c006aaf5eb163657
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804093"
---
# <a name="endpsrv-end-process-server"></a>.endpsrv（结束进程服务器）


**Endpsrv** 命令使当前进程服务器或 KD 连接服务器关闭。

```dbgcmd
.endpsrv 
```

## <span id="ddk_meta_end_process_server_dbg"></span><span id="DDK_META_END_PROCESS_SERVER_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

仅当通过进程服务器或 KD 连接服务器执行远程调试时，才能使用此命令。

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
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关这些服务器的详细信息，请参阅 [Process server (User mode) ](process-servers--user-mode-.md) 或 [KD Connection Server (内核模式) ](kd-connection-servers--kernel-mode-.md)

<a name="remarks"></a>备注
-------

**Endpsrv** 命令终止当前连接到智能客户端的进程服务器或 KD 连接服务器。

如果要从运行进程服务器或 KD 连接服务器的计算机上终止该进程，请使用 "任务管理器" 结束进程 ( # A0 或 kdsrv.exe) 。

**Endpsrv** 命令可以终止进程服务器或 KD 连接服务器，但不能终止调试服务器。 有关如何执行此操作的信息，请参阅 [控制远程调试会话](controlling-a-remote-debugging-session.md)。

 

 





