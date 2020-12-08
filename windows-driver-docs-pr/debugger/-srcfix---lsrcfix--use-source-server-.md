---
title: .srcfix、.lsrcfix（使用源服务器）
description: Srcfix 和. lsrcfix 命令自动将源路径设置为，以指示将使用源服务器。
keywords:
- srcfix、. lsrcfix (使用源服务器) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .srcfix, .lsrcfix (Use Source Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e28eb08a6e4c0bef6db55ce96ffcd64f0e5aae1e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811245"
---
# <a name="srcfix-lsrcfix-use-source-server"></a>.srcfix、.lsrcfix（使用源服务器）


**Srcfix** 和 **. lsrcfix** 命令自动将源路径设置为，以指示将使用源服务器。

```dbgcmd
.srcfix[+] [Paths] 
.lsrcfix[+] [Paths] 
```

## <a name="span-idddk_meta_use_source_server_dbgspanspan-idddk_meta_use_source_server_dbgspanparameters"></a><span id="ddk_meta_use_source_server_dbg"></span><span id="DDK_META_USE_SOURCE_SERVER_DBG"></span>参数


<span id="______________"></span> **+**   
导致保留现有源路径，并将 **srv \\** _ 追加到末尾。 如果 *+* 未使用 _ *，将替换现有源路径。

<span id="_______Paths______"></span><span id="_______paths______"></span><span id="_______PATHS______"></span>*路径*   
指定要追加到新源路径末尾的一个或多个附加路径。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

**Srcfix** 命令在所有调试器上都可用。 **Lsrcfix** 命令仅在 WinDbg 中可用，不能在脚本文件中使用。

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
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关设置远程客户端本地源路径的详细信息，请参阅 [**WinDbg Command-Line 选项**](windbg-command-line-options.md)。 有关 [srcsrv.ini](srcsrv.md)的详细信息，请参阅 [使用源服务器](using-a-source-server.md)。 有关源路径和本地源路径的详细信息，请参阅 [源路径](source-path.md)。 有关通过调试器执行远程调试时可以使用的命令的详细信息，请参阅 [控制远程调试会话](controlling-a-remote-debugging-session.md)。

<a name="remarks"></a>备注
-------

向 `srv*` 源路径添加时，调试器将使用 [srcsrv.ini](srcsrv.md) 从目标模块的符号文件中指定的位置检索源文件。 `srv*`在源路径中使用在本质上不同于 `srv*` 在符号路径中使用。 在符号路径中，可以指定符号服务器位置和 `srv*` (例如 `.sympath SRV*https://msdl.microsoft.com/download/symbols`) 。 在源路径中，srv \* 独立于所有其他元素用分号分隔。

从调试客户端发出此命令时， **。 srcfix** 将源路径设置为在调试服务器上使用源服务器，而 **lsrcfix** 在本地计算机上执行相同的工作。

这些命令与 [**. srcpath (设置源路径)**](-srcpath---lsrcpath--set-source-path-.md)和 **. Lsrcpath (设置本地源路径)** 命令后跟 **srv \\** _ 源路径元素。 因此，以下两个命令是等效的：

```dbgcmd
.srcfix[+] [Paths] 
.srcpath[+] srv_[;Paths] 
```

同样，以下两个命令是等效的：

```dbgcmd
.lsrcfix[+] [Paths] 
.lsrcpath[+] srv*[;Paths] 
```

 

 





