---
title: .send_file（发送文件）
description: .Send_file 命令将复制文件。 如果通过进程服务器执行远程调试，则会将文件从智能客户端的计算机发送到进程服务器的计算机。
keywords:
- 在 Windows 调试) .send_file (发送文件
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .send_file (Send File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd1ed0c3eccd738957f6a04fc51f1d77d45ffbd1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837359"
---
# <a name="send_file-send-file"></a>。发送 \_ 文件 (发送文件) 


**. Send \_ file** 命令复制文件。 如果通过进程服务器执行远程调试，则会将文件从智能客户端的计算机发送到进程服务器的计算机。

```dbgcmd
.send_file [-f] Source Destination 
.send_file [-f] -s Destination 
```

## <a name="span-idddk_meta_send_file_dbgspanspan-idddk_meta_send_file_dbgspanparameters"></a><span id="ddk_meta_send_file_dbg"></span><span id="DDK_META_SEND_FILE_DBG"></span>参数


<span id="_______-f______"></span><span id="_______-F______"></span>**-f**   
强制创建文件。 默认情况下， **发送 \_ 文件** 将不会覆盖任何现有文件。 如果使用-f 开关，将始终创建目标文件，并且将覆盖任何同名的现有文件。

<span id="_______Source______"></span><span id="_______source______"></span><span id="_______SOURCE______"></span>*源*   
指定要发送的文件的完整路径和文件名。 如果要通过进程服务器进行调试，则此文件必须位于运行智能客户端的计算机上。

<span id="_______Destination______"></span><span id="_______destination______"></span><span id="_______DESTINATION______"></span>*目标*   
指定要写入文件的目录。 如果要通过进程服务器进行调试，则会在运行进程服务器的计算机上计算此目录名称。

<span id="_______-s______"></span><span id="_______-S______"></span>**-s**   
使调试器复制所有加载的符号文件。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

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

 

<a name="remarks"></a>备注
-------

如果已通过进程服务器执行远程调试，但要改为开始调试，则此命令特别有用。 在这种情况下，可以使用. send \_ file-s 命令将调试器已使用的所有符号文件复制到进程服务器。 然后，在本地计算机上运行的调试器可以使用这些符号文件。

 

 





