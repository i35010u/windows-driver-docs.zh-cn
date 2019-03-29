---
title: lsf、lsf-（加载或卸载源文件）
description: Lsf 和 lsf 命令加载或卸载源文件。
ms.assetid: e788a778-e331-4b7b-8aad-072b3d08442b
keywords:
- lsf，lsf-（加载或卸载源文件） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lsf, lsf- (Load or Unload Source File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7715ea4d9f0f9a2db7d8c1031b5974a735203b4d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563865"
---
# <a name="lsf-lsf--load-or-unload-source-file"></a>lsf、lsf-（加载或卸载源文件）


**Lsf**并**lsf-** 命令加载或卸载源文件。

```dbgcmd
lsf Filename 
lsf- Filename
```

## <a name="span-idddkcmdloadorunloadsourcefiledbgspanspan-idddkcmdloadorunloadsourcefiledbgspanparameters"></a><span id="ddk_cmd_load_or_unload_source_file_dbg"></span><span id="DDK_CMD_LOAD_OR_UNLOAD_SOURCE_FILE_DBG"></span>参数


<span id="_______Filename______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span> *文件名*   
指定要加载或卸载的文件。 如果此文件不位于其中从中打开调试器的目录，则必须包括绝对或相对路径。 文件名称必须遵守 Microsoft Windows 文件命名约定。

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

**Lsf**命令加载源文件。

**Lsf-** 命令将卸载源文件。 可以使用此命令卸载以前加载的文件**lsf**或自动加载源文件。 不能使用**lsf-** 卸载通过 WinDbg 的加载文件[文件 |打开源文件](file---open-source-file.md)命令或加载 WinDbg 工作区的文件。

在 CDB 或 KD 中，可以查看中的源文件[调试器命令窗口](debugger-command-window.md)。 在 WinDbg 中，源加载了文件，为新[源 windows](source-window.md)。

有关源文件、 源路径和加载源文件的其他方法的详细信息，请参阅[源路径](source-path.md)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**ls，lsa （列表源行）**](ls--lsa--list-source-lines-.md)

[**lsc （列表当前源）**](lsc--list-current-source-.md)

 

 






