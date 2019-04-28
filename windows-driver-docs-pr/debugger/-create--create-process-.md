---
title: .create（创建进程）
description: .Create 命令创建新的目标应用程序。
ms.assetid: 9e34eadf-1f68-4eec-ad6b-d70163d5d876
keywords:
- .create （创建过程） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .create (Create Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a0b03dd9795701910d8d001d6da7f0d9e458a8a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334598"
---
# <a name="create-create-process"></a>.create（创建进程）


**.Create**命令将创建一个新的目标应用程序。

```dbgsyntax
.create [-premote RemoteOptions] [-f] CommandLine 
```

## <a name="span-idddkmetacreateprocessdbgspanspan-idddkmetacreateprocessdbgspanparameters"></a><span id="ddk_meta_create_process_dbg"></span><span id="DDK_META_CREATE_PROCESS_DBG"></span>参数


<span id="_______RemoteOptions______"></span><span id="_______remoteoptions______"></span><span id="_______REMOTEOPTIONS______"></span> *RemoteOptions*   
指定要附加的进程服务器。 选项是相同的命令行 **-premote**选项。 请参阅[**激活智能客户端**](activating-a-smart-client.md)有关语法详细信息。

<span id="_______-f______"></span><span id="_______-F______"></span> **-f**   
在正在创建新的目标中除冻结所有目标应用程序中的所有线程。 这些线程仍被冻结之前在新创建的过程中发生异常。 请注意，初始断点被称为异常。 各个线程可以通过使用解冻[ **~ （取消冻结线程） 的 u** ](-u--unfreeze-thread-.md)命令。

<span id="_______CommandLine______"></span><span id="_______commandline______"></span><span id="_______COMMANDLINE______"></span> *CommandLine*   
指定新的进程的完整命令行。 *命令行*可能包含空格，而且不必须用引号括起来。 之后的所有文本 **.create**命令执行的一部分*CommandLine*; 此命令后面不能用分号和其他调试程序命令。

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

如果此命令成功，调试器将在下次调试器将会发出执行命令创建指定的进程。 如果行中多次使用此命令，将必须执行许多次，使用此命令请求。

多个目标进程将始终在一起，除非它们的线程的一些被冻结或挂起。

如果你想要创建一个新进程并冻结所有现有目标，使用-f 选项。

如果 **-premote**选项，则新进程将成为新的系统的一部分。 有关详细信息，请参阅[调试多个目标](debugging-multiple-targets.md)。

 

 





