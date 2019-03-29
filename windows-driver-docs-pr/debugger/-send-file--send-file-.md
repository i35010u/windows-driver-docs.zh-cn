---
title: .send_file（发送文件）
description: .Send_file 命令将复制文件。 如果您正在执行的进程服务器通过远程调试，它将文件发送从智能客户端计算机到进程服务器的计算机。
ms.assetid: ad12ec46-79a3-458a-acdc-c2ccb06f8c96
keywords:
- .send_file （发送文件） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .send_file (Send File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a0905f792e32ed595c7053573525b5836b1ba277
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567479"
---
# <a name="sendfile-send-file"></a>.send\_文件 （发送文件）


**.Send\_文件**命令将复制文件。 如果您正在执行的进程服务器通过远程调试，它将文件发送从智能客户端计算机到进程服务器的计算机。

```dbgcmd
.send_file [-f] Source Destination 
.send_file [-f] -s Destination 
```

## <a name="span-idddkmetasendfiledbgspanspan-idddkmetasendfiledbgspanparameters"></a><span id="ddk_meta_send_file_dbg"></span><span id="DDK_META_SEND_FILE_DBG"></span>参数


<span id="_______-f______"></span><span id="_______-F______"></span> **-f**   
强制文件创建。 默认情况下 **.send\_文件**将不会覆盖任何现有文件。 如果使用-f 开关，始终会创建目标文件，并具有相同名称的任何现有文件将被覆盖。

<span id="_______Source______"></span><span id="_______source______"></span><span id="_______SOURCE______"></span> *Source*   
指定的完整路径和要发送的文件的文件名。 如果你正在调试的进程服务器通过，此文件必须位于运行智能客户端的计算机上。

<span id="_______Destination______"></span><span id="_______destination______"></span><span id="_______DESTINATION______"></span> *目标*   
指定要写入该文件所在的目录。 如果你正在调试的进程服务器通过，此目录名称计算上运行的进程服务器的计算机。

<span id="_______-s______"></span><span id="_______-S______"></span> **-s**   
使调试器来复制所有已加载的符号文件。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

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

 

<a name="remarks"></a>备注
-------

当正在执行的进程服务器，通过远程调试，但想要开始改为在本地调试时，此命令是特别有用。 在这种情况下可以使用.send\_文件-s 命令将调试程序已使用的所有符号文件复制到进程服务器。 在本地计算机上运行的调试程序然后可以使用这些符号文件。

 

 





