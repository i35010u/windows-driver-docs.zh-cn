---
title: .attach（附加到进程）
description: .Attach 命令将附加到新的目标应用程序。
ms.assetid: e637c7eb-9c3c-4501-b972-a9293a6da52a
keywords:
- 将附加到进程 (.attach) 命令
- 过程中，附加到进程 (.attach) 命令
- .attach （附加到进程） Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .attach (Attach to Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ca03126ac57aa6b9a45056e50f2eb7a1cee3f72a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334726"
---
# <a name="attach-attach-to-process"></a>.attach（附加到进程）


**.Attach**命令将附加到新的目标应用程序。

```dbgcmd    
.attach [-premote RemoteOptions] AttachOptions PID
```

## <a name="span-idddkmetaattachtoprocessdbgspanspan-idddkmetaattachtoprocessdbgspanparameters"></a><span id="ddk_meta_attach_to_process_dbg"></span><span id="DDK_META_ATTACH_TO_PROCESS_DBG"></span>参数


<span id="_______RemoteOptions______"></span><span id="_______remoteoptions______"></span><span id="_______REMOTEOPTIONS______"></span> *RemoteOptions*   
指定要将附加到进程服务器。 选项是相同的命令行 **-premote**选项。 请参阅[**激活智能客户端**](activating-a-smart-client.md)有关语法详细信息。

<span id="_______AttachOptions______"></span><span id="_______attachoptions______"></span><span id="_______ATTACHOPTIONS______"></span> *AttachOptions*   
指定如何进行附加。 这可能包括以下选项之一：

<span id="-b"></span><span id="-B"></span>**-b**  
防止调试器附加到目标进程时请求初始被侵入的情形。 如果应用程序已挂起，或者如果你想要避免在目标中创建被侵入的情形线程，这可以很有用。

<span id="-e"></span><span id="-E"></span>**-e**  
使调试器能够附加到正在调试的进程。 请参阅[重新连接到目标应用程序](reattaching-to-the-target-application.md)有关详细信息。

<span id="-k"></span><span id="-K"></span>**-k**  
开始本地内核调试会话。 请参阅[执行本地内核调试](performing-local-kernel-debugging.md)有关详细信息。

<span id="-f"></span><span id="-F"></span>**-f**  
在附加到新的目标中除冻结所有目标应用程序中的所有线程。 这些线程将保持被冻结，直到新附加的进程中发生异常。 请注意，初始断点被称为异常。 各个线程可以通过使用解冻[ **~ （取消冻结线程） 的 u** ](-u--unfreeze-thread-.md)命令。

<span id="-r"></span><span id="-R"></span>**-r**  

导致调试器开始运行时它将附加到它的目标进程。 如果应用程序已挂起状态，并且您希望其继续执行，这很有用。

<span id="-v"></span><span id="-V"></span>**-v**  
使指定的进程 noninvasively 调试。

<span id="_______PID______"></span><span id="_______pid______"></span> *PID*   
指定新的目标应用程序的进程 ID。

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

 

<a name="remarks"></a>备注
-------

CDB 处于休眠状态，或者如果它已调试一个或多个进程，可以使用此命令。 它不能使用 WinDbg 处于休眠状态时。

如果此命令成功，调试器将附加到指定的进程发出执行命令，在调试器下一次。 如果行中多次使用此命令，将必须执行许多次，使用此命令请求。

在非侵入调试过程中不允许执行，因为调试器不能 noninvasively 一次调试多个进程。 这也意味着，使用 **.attach v**命令可能会导致现有的侵入性调试会话不太有用。

多个目标进程将始终在一起，除非它们的线程的一些被冻结或挂起。

如果你想要附加到新进程并冻结所有现有目标，请使用 **-f**选项。 例如，你可能是调试客户端应用程序故障并想要将附加到的服务器进程，而无需使客户端应用程序继续运行。

如果 **-premote**选项，则新进程将成为新的系统的一部分。 有关详细信息，请参阅[调试多个目标](debugging-multiple-targets.md)。

 

 





