---
title: .srcpath、.lsrcpath（设置源路径）
description: Srcpath 和. lsrcpath 命令设置或显示源文件搜索路径。
keywords:
- srcpath、. lsrcpath (设置源路径) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .srcpath, .lsrcpath (Set Source Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5c1620453ab2e13c18b2b45d68c6dd04538df622
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826189"
---
# <a name="srcpath-lsrcpath-set-source-path"></a>.srcpath、.lsrcpath（设置源路径）


**Srcpath** 和 **. lsrcpath** 命令设置或显示源文件搜索路径。

```dbgcmd
.srcpath[+] [Directory [; ...]] 
.lsrcpath[+] [Directory [; ...]] 
```

## <a name="span-idddk_meta_set_source_path_dbgspanspan-idddk_meta_set_source_path_dbgspanparameters"></a><span id="ddk_meta_set_source_path_dbg"></span><span id="DDK_META_SET_SOURCE_PATH_DBG"></span>参数


<span id="______________"></span> **+**   
指定新目录将追加到 (，而不是替换以前的源文件搜索路径) 。

<span id="_______Directory______"></span><span id="_______directory______"></span><span id="_______DIRECTORY______"></span>*目录*   
指定要放入搜索路径中的一个或多个目录。 如果未指定 *目录* ，则显示当前路径。 用分号分隔多个目录。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

**Srcpath** 命令在所有调试器上都可用。 **Lsrcpath** 命令仅在 WinDbg 中可用，不能在脚本文件中使用。

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

有关更改此路径的详细信息和其他方式，请参阅 [源路径](source-path.md)。 有关通过调试器执行远程调试时可以使用的命令的详细信息，请参阅 [控制远程调试会话](controlling-a-remote-debugging-session.md)。

<a name="remarks"></a>备注
-------

如果你将包含 `srv*` 在源路径中，则调试器将使用 [srcsrv.ini](srcsrv.md) 从目标模块的符号文件中指定的位置检索源文件。 有关在源路径中使用 srv 的详细信息 \* ，请参阅 [使用源服务器](using-a-source-server.md) 和 [**srcfix**](-srcfix---lsrcfix--use-source-server-.md)。

当从调试客户端发出此命令时， **。 srcpath** 将在调试服务器上设置源路径，而 **lsrcpath** 将设置本地计算机上的源路径。

 

 





