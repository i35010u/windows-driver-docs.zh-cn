---
title: .srcpath、.lsrcpath（设置源路径）
description: .Srcpath 和.lsrcpath 命令设置或显示源文件搜索路径。
ms.assetid: 416c062f-cbf9-4134-aa2c-306147a466b5
keywords:
- .srcpath，.lsrcpath （设置源路径） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .srcpath, .lsrcpath (Set Source Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2e830d183bab930d2448ea57c265d0f65e16d84d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338796"
---
# <a name="srcpath-lsrcpath-set-source-path"></a>.srcpath、.lsrcpath（设置源路径）


**.Srcpath**并 **.lsrcpath**命令设置或显示源文件搜索路径。

```dbgcmd
.srcpath[+] [Directory [; ...]] 
.lsrcpath[+] [Directory [; ...]] 
```

## <a name="span-idddkmetasetsourcepathdbgspanspan-idddkmetasetsourcepathdbgspanparameters"></a><span id="ddk_meta_set_source_path_dbg"></span><span id="DDK_META_SET_SOURCE_PATH_DBG"></span>参数


<span id="______________"></span> **+**   
指定是否将 （而不是替换） 追加到新目录的上一个源文件搜索路径。

<span id="_______Directory______"></span><span id="_______directory______"></span><span id="_______DIRECTORY______"></span> *Directory*   
指定要放入搜索路径中的一个或多个目录。 如果*Directory*未指定，则显示当前路径。 用分号分隔多个目录。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

**.Srcpath**命令出现在所有调试器上。 **.Lsrcpath**命令仅在 WinDbg 中可用，并能在脚本文件。

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

有关详细信息和更改此路径的其他方法，请参阅[源路径](source-path.md)。 有关命令的可执行通过调试器的远程调试时使用的详细信息，请参阅[控制远程调试会话](controlling-a-remote-debugging-session.md)。

<a name="remarks"></a>备注
-------

如果包括`srv*`在您的源路径，使用调试器[SrcSrv](srcsrv.md)来从目标模块的符号文件中指定的位置检索源文件。 详细了解使用 srv\*中的源路径，请参阅[使用源服务器](using-a-source-server.md)并[ **.srcfix**](-srcfix---lsrcfix--use-source-server-.md)。

从调试客户端，发出此命令时 **.srcpath**在调试服务器上设置的源路径时 **.lsrcpath**在本地计算机上设置的源路径。

 

 





