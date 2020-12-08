---
title: .attach（附加到进程）
description: . Attach 命令附加到新的目标应用程序。
keywords:
- 附加到进程 (。附加) 命令
- 处理、附加到进程 (。附加) 命令
- 。将 (附加到进程) Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .attach (Attach to Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 22ef0e233e2a34e388ab2286670ced5be193f5c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799991"
---
# <a name="attach-attach-to-process"></a>.attach（附加到进程）


**. Attach** 命令附加到新的目标应用程序。

```dbgcmd    
.attach [-premote RemoteOptions] AttachOptions PID
```

## <a name="span-idddk_meta_attach_to_process_dbgspanspan-idddk_meta_attach_to_process_dbgspanparameters"></a><span id="ddk_meta_attach_to_process_dbg"></span><span id="DDK_META_ATTACH_TO_PROCESS_DBG"></span>参数


<span id="_______RemoteOptions______"></span><span id="_______remoteoptions______"></span><span id="_______REMOTEOPTIONS______"></span>*RemoteOptions*   
指定要附加到的进程服务器。 选项与命令行 **-premote** 选项的选项相同。 有关语法的详细信息，请参阅 [**激活智能客户端**](activating-a-smart-client.md) 。

<span id="_______AttachOptions______"></span><span id="_______attachoptions______"></span><span id="_______ATTACHOPTIONS______"></span>*AttachOptions*   
指定如何完成附加操作。 这可以包括以下任何选项：

<span id="-b"></span><span id="-B"></span>**-b**  
阻止调试器在附加到目标进程时请求初始中断。 如果应用程序已挂起，或者您想要避免在目标中创建一个中断线程，则这会很有用。

<span id="-e"></span><span id="-E"></span>**-e**  
允许调试器附加到已在调试的进程。 有关详细信息，请参阅 [重新附加到目标应用程序](reattaching-to-the-target-application.md) 。

<span id="-k"></span><span id="-K"></span>**-k**  
开始本地内核调试会话。 有关详细信息，请参阅 [执行本地内核调试](performing-local-kernel-debugging.md) 。

<span id="-f"></span><span id="-F"></span>**-f**  
冻结所有目标应用程序中的所有线程，但要附加到的新目标除外。 这些线程将保持冻结状态，直到新附加的进程中出现异常。 请注意，初始断点限定为异常。 可以使用 [**~ u (解冻线程)**](-u--unfreeze-thread-.md) 命令，来解冻单个线程。

<span id="-r"></span><span id="-R"></span>**-r**  

导致调试器在附加到目标进程时启动该进程。 如果应用程序已挂起，并且你希望它继续执行，则这会很有用。

<span id="-v"></span><span id="-V"></span>**-v**  
导致 noninvasively 调试指定进程。

<span id="_______PID______"></span><span id="_______pid______"></span>*PID*   
指定新目标应用程序的进程 ID。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

当 CDB 处于休眠状态或它已在调试一个或多个进程时，可以使用此命令。 当 WinDbg 处于休眠状态时，不能使用它。

如果此命令成功，则调试器将在下一次发出执行命令时附加到指定的进程。 如果在一行中多次使用此命令，则必须使用此命令多次请求执行。

由于在 noninvasive 调试过程中不允许执行，因此调试器不能一次调试多个进程。 这也意味着，使用 **-v** 命令可能会使现有的侵害性调试会话不太有用。

多个目标进程将始终一起执行，除非它们的某些线程被冻结或挂起。

如果要附加到新进程并冻结所有现有目标，请使用 **-f** 选项。 例如，你可能会在客户端应用程序中调试崩溃，并想要附加到服务器进程，而不允许客户端应用程序继续运行。

如果使用了 **-premote** 选项，则新的进程将是新系统的一部分。 有关详细信息，请参阅 [调试多个目标](debugging-multiple-targets.md)。

 

 





