---
title: .exepath（设置可执行文件路径）
description: .Exepath 命令设置或显示的可执行文件搜索路径。
ms.assetid: 09f8c2f6-4df7-4039-bb92-66d42015c3dc
keywords:
- .exepath （设置可执行文件路径） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .exepath (Set Executable Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1c705f2f67abb356c53a3f846ae6dcdb2a75e05f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334495"
---
# <a name="exepath-set-executable-path"></a>.exepath（设置可执行文件路径）


**.Exepath**命令设置或显示的可执行文件搜索路径。

```dbgcmd
.exepath[+] [Directory [; ...]] 
```

## <a name="span-idddkmetasetexecutablepathdbgspanspan-idddkmetasetexecutablepathdbgspanparameters"></a><span id="ddk_meta_set_executable_path_dbg"></span><span id="DDK_META_SET_EXECUTABLE_PATH_DBG"></span>参数


<span id="______________"></span> **+**   
指定调试器应附加到以前的可执行文件搜索路径 （而不是替换路径） 的新目录。

<span id="_______Directory______"></span><span id="_______directory______"></span><span id="_______DIRECTORY______"></span> *Directory*   
指定要放入搜索路径中的一个或多个目录。 如果未指定*Directory*，显示当前路径。 可以使用分号分隔多个目录。

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

 

 

 





