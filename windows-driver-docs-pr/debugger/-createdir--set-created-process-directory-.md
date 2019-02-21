---
title: .createdir （集创建的进程目录）
description: .Createdir 命令控制调试器创建的任何进程的开始目录和句柄继承。
ms.assetid: 797f5398-f0b4-48e9-bc5f-eac5a53cad67
keywords:
- .createdir （集创建的进程目录） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .createdir (Set Created Process Directory)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3a5245f42b272564849464fd2c57a794c9f73e43
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522118"
---
# <a name="createdir-set-created-process-directory"></a>.createdir （集创建的进程目录）


**.Createdir**命令控制调试器创建的任何进程的开始目录和句柄继承。

```dbgsyntax
.createdir [-i | -I] [Path] 
```

## <a name="span-idddkmetasetcreatedprocessdirectorydbgspanspan-idddkmetasetcreatedprocessdirectorydbgspanparameters"></a><span id="ddk_meta_set_created_process_directory_dbg"></span><span id="DDK_META_SET_CREATED_PROCESS_DIRECTORY_DBG"></span>参数


<span id="_______-i______"></span><span id="_______-I______"></span> **-i**   
使调试器可以从调试器继承句柄创建的进程。 这是默认设置。

<span id="_______-I______"></span><span id="_______-i______"></span> **-I**   
可以防止创建句柄继承从调试器调试程序的进程。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span> *路径*   
指定创建的任何目标进程的所有子进程的开始目录。 如果*路径*包含空格，则必须用引号引起来。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>仅限用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>仅实时调试</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果 **.createdir**使用不带任何参数，显示的当前起始目录和句柄继承状态。

如果 **.createdir**从未像现在使用，任何创建的进程将使用其常见的默认目录作为其起始目录。 如果您已经设置了与路径 **.createdir** ，并且想要返回到默认状态，使用 **.createdir""** 不含任何内容的引号内。

**.Createdir**设置会影响创建的所有进程[ **.create （创建进程）**](-create--create-process-.md)。 它还会影响创建的 WinDbg 的进程[文件 |打开可执行文件](file---open-executable.md)菜单命令时，除非**启动目录**文本框用于重写此设置。

 

 





