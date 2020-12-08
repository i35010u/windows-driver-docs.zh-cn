---
title: .createdir（设置已创建的进程目录）
description: Createdir 命令控制启动目录并处理调试器创建的任何进程的继承。
keywords:
- createdir (集创建的进程目录) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .createdir (Set Created Process Directory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1102cd40df2417da66064a1c1b347f408f3ce135
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786499"
---
# <a name="createdir-set-created-process-directory"></a>.createdir（设置已创建的进程目录）


**Createdir** 命令控制启动目录并处理调试器创建的任何进程的继承。

```dbgsyntax
.createdir [-i | -I] [Path] 
```

## <a name="span-idddk_meta_set_created_process_directory_dbgspanspan-idddk_meta_set_created_process_directory_dbgspanparameters"></a><span id="ddk_meta_set_created_process_directory_dbg"></span><span id="DDK_META_SET_CREATED_PROCESS_DIRECTORY_DBG"></span>参数


<span id="_______-i______"></span><span id="_______-I______"></span>**-i**   
使调试器创建的进程从调试器继承句柄。 这是默认值。

<span id="_______-I______"></span><span id="_______-i______"></span>**-I**   
阻止调试器创建的进程从调试器继承句柄。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span>*路径*   
指定由任何目标进程创建的所有子进程的起始目录。 如果 *路径* 包含空格，则必须用引号将其引起来。

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

如果使用不带参数的 **createdir** ，则将显示当前起始目录和句柄继承状态。

如果从未使用过 **createdir** ，则任何创建的进程都将使用其常规默认目录作为其起始目录。 如果已设置 **createdir** 的路径，并且想要返回到默认状态，请在引号内使用不包含任何内容的 **createdir ""** 。

**Createdir** 设置影响由创建的所有进程 [**。) 创建 (创建进程**](-create--create-process-.md)。 它还会影响 WinDbg 的文件创建的进程 [|打开可执行](file---open-executable.md) 菜单命令，除非使用 " **开始目录** " 文本框来替代此设置。

 

 





