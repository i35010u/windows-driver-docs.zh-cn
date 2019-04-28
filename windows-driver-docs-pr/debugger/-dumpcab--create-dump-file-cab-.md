---
title: .dumpcab（创建转储文件 CAB）
description: .Dumpcab 命令创建包含当前的转储文件的 CAB 文件。
ms.assetid: 65ed766f-b049-47b0-90d7-e21d510a35ba
keywords:
- .dumpcab （创建转储文件 CAB） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .dumpcab (Create Dump File CAB)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 06c2fcc275f203af634eec64ec989f61d3fb82e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336792"
---
# <a name="dumpcab-create-dump-file-cab"></a>.dumpcab（创建转储文件 CAB）


**.Dumpcab**命令创建包含当前的转储文件的 CAB 文件。

```dbgcmd
.dumpcab [-a] CabName 
```

## <a name="span-idddkmetacreatedumpfilecabdbgspanspan-idddkmetacreatedumpfilecabdbgspanparameters"></a><span id="ddk_meta_create_dump_file_cab_dbg"></span><span id="DDK_META_CREATE_DUMP_FILE_CAB_DBG"></span>参数


<span id="_______-a______"></span><span id="_______-A______"></span> **-a**   
导致要包括在 CAB 文件中的所有当前已加载的符号。 对于小型转储，所有已加载的映像将包含也。 使用[**喜欢我的生活**](lm--list-loaded-modules-.md)若要确定加载的符号和映像。

<span id="_______CabName______"></span><span id="_______cabname______"></span><span id="_______CABNAME______"></span> *CabName*   
CAB 文件名称，包括扩展。 *CabName*可以包括绝对或相对路径; 相对路径是相对于在其中启动调试器的目录。 建议选择扩展.cab 文件。

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
<td align="left"><p>故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

故障转储的更多详细信息，请参阅[崩溃转储文件](crash-dump-files.md)。

<a name="remarks"></a>备注
-------

如果已在调试转储文件，则仅可以使用此命令。

如果你正在调试实时目标并想要创建转储文件，并将其放在出租车里，您应使用[ **.dump （创建转储文件）** ](-dump--create-dump-file-.md)命令。 接下来，该转储文件作为其目标，启动新的调试会话并使用 **.dumpcab**。

**.Dumpcab**命令不能用于将多个转储文件放到一个 CAB 文件中。

 

 





