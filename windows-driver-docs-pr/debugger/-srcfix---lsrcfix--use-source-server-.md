---
title: .srcfix、.lsrcfix（使用源服务器）
description: .Srcfix 和.lsrcfix 命令自动设置的源路径，以指示将使用源服务器。
ms.assetid: e4cc3031-7990-4339-9dc2-f2c5a219a771
keywords:
- .srcfix，.lsrcfix （使用源服务器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .srcfix, .lsrcfix (Use Source Server)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8b5710055ed6656452b2cb2278c11f8e7baaa12f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338814"
---
# <a name="srcfix-lsrcfix-use-source-server"></a>.srcfix、.lsrcfix（使用源服务器）


**.Srcfix**并 **.lsrcfix**命令自动设置的源路径，以指示将使用源服务器。

```dbgcmd
.srcfix[+] [Paths] 
.lsrcfix[+] [Paths] 
```

## <a name="span-idddkmetausesourceserverdbgspanspan-idddkmetausesourceserverdbgspanparameters"></a><span id="ddk_meta_use_source_server_dbg"></span><span id="DDK_META_USE_SOURCE_SERVER_DBG"></span>参数


<span id="______________"></span> **+**   
使现有的源路径，会予以保留，并 **; srv\\*** 若要追加到末尾。 如果**+** 是未使用，将替换现有的源路径。

<span id="_______Paths______"></span><span id="_______paths______"></span><span id="_______PATHS______"></span> *Paths*   
指定一个或多个附加路径; 要追加到新的源路径的末尾。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

**.Srcfix**命令出现在所有调试器上。 **.Lsrcfix**命令仅在 WinDbg 中可用，并能在脚本文件。

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

本地源路径设置为远程客户端的详细信息，请参阅[ **WinDbg 命令行选项**](windbg-command-line-options.md)。 有关详细信息[SrcSrv](srcsrv.md)，请参阅[使用源服务器](using-a-source-server.md)。 源路径和本地源路径的详细信息，请参阅[源路径](source-path.md)。 有关命令的可执行通过调试器的远程调试时使用的详细信息，请参阅[控制远程调试会话](controlling-a-remote-debugging-session.md)。

<a name="remarks"></a>备注
-------

当您将添加`srv*`到源路径中，调试器使用[SrcSrv](srcsrv.md)来从目标模块的符号文件中指定的位置检索源文件。 使用`srv*`在源中路径是从根本上不同于使用`srv*`符号路径中。 在符号路径中，可以指定符号服务器位置连同`srv*`(例如， `.sympath SRV* https://msdl.microsoft.com/download/symbols`)。 在源路径 srv\*是相互独立，从所有其他元素之间用分号分隔。

从调试客户端，发出此命令时 **.srcfix**设置为在调试服务器上，使用源服务器的源路径时 **.lsrcfix**执行相同的本地计算机上。

这些命令将与相同[ **.srcpath （设置源路径）** ](-srcpath---lsrcpath--set-source-path-.md)并 **.lsrcpath （设置本地源路径）** 命令跟**srv\\** * 源路径元素。 因此，以下两个命令是等效的：

```dbgcmd
.srcfix[+] [Paths] 
.srcpath[+] srv*[;Paths] 
```

同样，以下两个命令是等效的：

```dbgcmd
.lsrcfix[+] [Paths] 
.lsrcpath[+] srv*[;Paths] 
```

 

 





