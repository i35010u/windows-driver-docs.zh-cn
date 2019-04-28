---
title: .endpsrv（结束进程服务器）
description: .Endpsrv 命令会使当前进程服务器或 KD 连接服务器关闭。
ms.assetid: 3f8d0a85-f0f4-4c13-ab52-e4d99ba3599c
keywords:
- .endpsrv （结束进程服务器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .endpsrv (End Process Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9339a9aaf2d51e9b7f9a2d13b1ee0685543f660b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337218"
---
# <a name="endpsrv-end-process-server"></a>.endpsrv（结束进程服务器）


**.Endpsrv**命令将导致当前进程服务器或 KD 连接服务器关闭。

```dbgcmd
.endpsrv 
```

## <span id="ddk_meta_end_process_server_dbg"></span><span id="DDK_META_END_PROCESS_SERVER_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

仅当执行远程调试通过进程服务器或 KD 连接服务器时，可以使用此命令。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关这些服务器的详细信息，请参阅[的进程服务器 （用户模式）](process-servers--user-mode-.md)或[KD 连接服务器 （内核模式）](kd-connection-servers--kernel-mode-.md)

<a name="remarks"></a>备注
-------

**.Endpsrv**命令终止的进程服务器或 KD 连接服务器当前连接到智能客户端。

如果你想要终止的进程服务器或从其运行的计算机的 KD 连接服务器，使用任务管理器结束进程 （dbgsrv.exe 或 kdsrv.exe）。

**.Endpsrv**命令可以终止的进程服务器或 KD 连接服务器，但它不能终止调试服务器。 有关如何执行该操作的信息，请参阅[控制远程调试会话](controlling-a-remote-debugging-session.md)。

 

 





