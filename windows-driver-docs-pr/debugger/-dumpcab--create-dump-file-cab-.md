---
title: .dumpcab（创建转储文件 CAB）
description: Dumpcab 命令创建包含当前转储文件的 CAB 文件。
keywords:
- dumpcab (创建转储文件 CAB) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dumpcab (Create Dump File CAB)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 64ed1c6cfef0180d7f72b93b22e5e1ef5552f991
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799899"
---
# <a name="dumpcab-create-dump-file-cab"></a>.dumpcab（创建转储文件 CAB）


**Dumpcab** 命令创建包含当前转储文件的 CAB 文件。

```dbgcmd
.dumpcab [-a] CabName 
```

## <a name="span-idddk_meta_create_dump_file_cab_dbgspanspan-idddk_meta_create_dump_file_cab_dbgspanparameters"></a><span id="ddk_meta_create_dump_file_cab_dbg"></span><span id="DDK_META_CREATE_DUMP_FILE_CAB_DBG"></span>参数


<span id="_______-a______"></span><span id="_______-A______"></span>**-a**   
使所有当前加载的符号都包含在 CAB 文件中。 对于小型转储，将同时包含所有加载的映像。 使用 [**"爱情"**](lm--list-loaded-modules-.md) 来确定要加载的符号和图像。

<span id="_______CabName______"></span><span id="_______cabname______"></span><span id="_______CABNAME______"></span>*CabName*   
CAB 文件的名称，包括扩展名。 *CabName* 可以包含绝对路径或相对路径;相对路径是相对于启动调试器的目录的相对路径。 建议选择扩展名 .cab。

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
<td align="left"><p>故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关故障转储的详细信息，请参阅 [故障转储文件](crash-dump-files.md)。

<a name="remarks"></a>备注
-------

仅当你已在调试转储文件时，才能使用此命令。

如果正在调试某个活动目标，并且想要创建转储文件并将其放入 CAB 中，则应使用 [**. dump (创建转储文件)**](-dump--create-dump-file-.md) 命令。 接下来，启动新的调试会话，将转储文件作为其目标，并使用 **dumpcab**。

**Dumpcab** 命令不能用于将多个转储文件放入一个 CAB 文件。

 

 





