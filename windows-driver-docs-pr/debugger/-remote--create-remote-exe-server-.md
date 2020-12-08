---
title: .remote（创建 Remote.exe 服务器）
description: Remote 命令启动 Remote.exe 服务器，启用到当前调试会话的远程连接。
keywords:
- Create Remote.exe Server ( remote) 命令
- 通过 remote.exe 远程调试，创建 Remote.exe Server ( 远程) 命令
- 。远程 () Windows 调试创建 Remote.exe 服务器
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .remote (Create Remote.exe Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 980450e43dca361067c8db14f6f21d708d1ddac2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795199"
---
# <a name="remote-create-remoteexe-server"></a>.remote（创建 Remote.exe 服务器）


**Remote** 命令启动 [Remote.exe 服务器](starting-a-remote-exe-session.md)，启用到当前调试会话的远程连接。

```dbgcmd
.remote session
```

## <a name="span-idddk_meta_create_remote_exe_server_dbgspanspan-idddk_meta_create_remote_exe_server_dbgspanparameters"></a><span id="ddk_meta_create_remote_exe_server_dbg"></span><span id="DDK_META_CREATE_REMOTE_EXE_SERVER_DBG"></span>参数


<span id="_______session______"></span><span id="_______SESSION______"></span>*会话*   
指定为调试会话指定的名称。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

可以在 KD 和 CDB 中使用 **remote** 命令，但不能在 WinDbg 中使用它。

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

有关如何使用 Remote.exe 服务器和 Remote.exe 客户端的详细信息，请参阅 Remote.exe中的 [远程调试 ](remote-debugging-through-remote-exe.md)。

<a name="remarks"></a>备注
-------

**Remote** 命令创建 Remote.exe 进程，并将当前调试器转换为 Remote.exe 服务器。 此服务器使 Remote.exe 的客户端能够连接到当前的调试会话。

 

 





