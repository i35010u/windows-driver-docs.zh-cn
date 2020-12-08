---
title: .create（创建进程）
description: . Create 命令创建新的目标应用程序。
keywords:
- 。创建 (创建进程) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .create (Create Process)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 121cfdf04628e7c322e4020cf60cbd58b0528740
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803329"
---
# <a name="create-create-process"></a>.create（创建进程）


**. Create** 命令创建新的目标应用程序。

```dbgsyntax
.create [-premote RemoteOptions] [-f] CommandLine 
```

## <a name="span-idddk_meta_create_process_dbgspanspan-idddk_meta_create_process_dbgspanparameters"></a><span id="ddk_meta_create_process_dbg"></span><span id="DDK_META_CREATE_PROCESS_DBG"></span>参数


<span id="_______RemoteOptions______"></span><span id="_______remoteoptions______"></span><span id="_______REMOTEOPTIONS______"></span>*RemoteOptions*   
指定要附加到的进程服务器。 选项与命令行 **-premote** 选项的选项相同。 有关语法的详细信息，请参阅 [**激活智能客户端**](activating-a-smart-client.md) 。

<span id="_______-f______"></span><span id="_______-F______"></span>**-f**   
冻结所有目标应用程序中的所有线程（在创建的新目标中除外）。 这些线程将保持冻结状态，直到新创建的进程中出现异常。 请注意，初始断点限定为异常。 可以使用 [**~ u (解冻线程)**](-u--unfreeze-thread-.md) 命令，来解冻单个线程。

<span id="_______CommandLine______"></span><span id="_______commandline______"></span><span id="_______COMMANDLINE______"></span>*命令行*   
指定新进程的完整命令行。 *命令行* 可能包含空格，并且不得括在引号中。 **Create** 命令后的所有文本都作为 *命令行* 的一部分执行;此命令后面不能跟分号和其他调试器命令。

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

如果此命令成功，则调试器将在下一次调试器发出执行命令时创建指定的进程。 如果在一行中多次使用此命令，则必须使用此命令多次请求执行。

多个目标进程将始终一起执行，除非它们的某些线程被冻结或挂起。

如果要创建新进程并冻结所有现有目标，请使用-f 选项。

如果使用了 **-premote** 选项，则新的进程将是新系统的一部分。 有关详细信息，请参阅 [调试多个目标](debugging-multiple-targets.md)。

 

 





