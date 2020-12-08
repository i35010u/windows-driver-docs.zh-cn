---
title: lsf、lsf-（加载或卸载源文件）
description: Lsf 和 lsf 加载或卸载源文件。
keywords:
- lsf，lsf- (加载或卸载源文件) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lsf, lsf- (Load or Unload Source File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1403e371d3d7f1a2e7f2f73946695f88344bbc3e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783446"
---
# <a name="lsf-lsf--load-or-unload-source-file"></a>lsf、lsf-（加载或卸载源文件）


**Lsf** 和 **lsf** 加载或卸载源文件。

```dbgcmd
lsf Filename 
lsf- Filename
```

## <a name="span-idddk_cmd_load_or_unload_source_file_dbgspanspan-idddk_cmd_load_or_unload_source_file_dbgspanparameters"></a><span id="ddk_cmd_load_or_unload_source_file_dbg"></span><span id="DDK_CMD_LOAD_OR_UNLOAD_SOURCE_FILE_DBG"></span>参数


<span id="_______Filename______"></span><span id="_______filename______"></span><span id="_______FILENAME______"></span>*Filename*   
指定要加载或卸载的文件。 如果此文件不在从中打开调试器的目录中，则必须包含绝对路径或相对路径。 文件名必须遵循 Microsoft Windows 文件名约定。

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

 

<a name="remarks"></a>备注
-------

**Lsf** 命令加载源文件。

**Lsf** 卸载源文件。 可以使用此命令卸载以前使用 **lsf** 或自动加载的源文件加载的文件。 不能使用 **lsf** 来卸载通过 WinDbg 的文件加载的文件 [|"打开文件](file---open-source-file.md) " 命令或已加载 WinDbg 工作区的文件。

在 CDB 或 KD 中，可以在 [调试器命令窗口](debugger-command-window.md)中查看源文件。 在 WinDbg 中，源文件作为新的 [源窗口](source-window.md)加载。

有关源文件、源路径和其他加载源文件的方法的详细信息，请参阅 [源路径](source-path.md)。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**ls、lsa（列出源行）**](ls--lsa--list-source-lines-.md)

[**lsc（列出当前源）**](lsc--list-current-source-.md)

 

 






