---
title: .remote（创建 Remote.exe 服务器）
description: .Remote 命令启动 Remote.exe 服务器，启用到当前调试会话的远程连接。
ms.assetid: fa3de33c-ba8c-4e9c-9899-b9a43f3195bf
keywords:
- 创建 Remote.exe 服务器 (.remote) 命令
- remote.exe，创建 Remote.exe 服务器 (.remote) 命令通过远程调试
- .remote （创建 Remote.exe 服务器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .remote (Create Remote.exe Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 86f546e75d8e999298b0b59aaad0573291ef9dce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338916"
---
# <a name="remote-create-remoteexe-server"></a>.remote（创建 Remote.exe 服务器）


**.Remote**命令启动[Remote.exe Server](starting-a-remote-exe-session.md)，启用到当前调试会话的远程连接。

```dbgcmd
.remote session
```

## <a name="span-idddkmetacreateremoteexeserverdbgspanspan-idddkmetacreateremoteexeserverdbgspanparameters"></a><span id="ddk_meta_create_remote_exe_server_dbg"></span><span id="DDK_META_CREATE_REMOTE_EXE_SERVER_DBG"></span>参数


<span id="_______session______"></span><span id="_______SESSION______"></span> *session*   
指定提供给的调试会话的名称。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

可以使用 **.remote**命令中 KD 和 CDB，但您不能在 WinDbg 中使用。

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

有关如何使用 Remote.exe 服务器和 Remote.exe 客户端的详细信息，请参阅[Remote.exe 通过远程调试](remote-debugging-through-remote-exe.md)。

<a name="remarks"></a>备注
-------

**.Remote**命令创建 Remote.exe 过程以及如何启用到 Remote.exe 服务器当前的调试器。 此服务器允许 Remote.exe 客户端连接到当前调试会话。

 

 





