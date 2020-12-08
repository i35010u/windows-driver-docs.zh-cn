---
title: .exepath（设置可执行文件路径）
description: Exepath 命令将设置或显示可执行文件搜索路径。
keywords:
- exepath (设置可执行文件路径) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .exepath (Set Executable Path)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 13254877cd623cf1843108b5de2684b3e85d0636
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820415"
---
# <a name="exepath-set-executable-path"></a>.exepath（设置可执行文件路径）


**Exepath** 命令将设置或显示可执行文件搜索路径。

```dbgcmd
.exepath[+] [Directory [; ...]] 
```

## <a name="span-idddk_meta_set_executable_path_dbgspanspan-idddk_meta_set_executable_path_dbgspanparameters"></a><span id="ddk_meta_set_executable_path_dbg"></span><span id="DDK_META_SET_EXECUTABLE_PATH_DBG"></span>参数


<span id="______________"></span> **+**   
指定调试器应将新目录追加到上一个可执行文件搜索路径 (，而不是替换路径) 。

<span id="_______Directory______"></span><span id="_______directory______"></span><span id="_______DIRECTORY______"></span>*目录*   
指定要放入搜索路径中的一个或多个目录。 如果未指定 *目录*，则显示当前路径。 可以用分号分隔多个目录。

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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

 

 





