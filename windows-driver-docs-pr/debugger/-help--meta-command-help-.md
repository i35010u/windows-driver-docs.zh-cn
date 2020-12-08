---
title: .help（元命令帮助）
description: "\"Help\" 命令显示所有元命令的列表。"
keywords:
- 。帮助 (的元命令帮助) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .help (Meta-Command Help)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0d03127c47ab914822d80300e3c4e01420548341
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825855"
---
# <a name="help-meta-command-help"></a>.help（元命令帮助）


" **Help** " 命令显示所有元命令的列表。

```dbgcmd
.help
.help /D 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="________D"></span><span id="________d"></span>**/D**  
使用 [调试器标记语言](debugger-markup-language-commands.md)显示输出。 输出包含链接的列表，您可以单击这些链接以查看使用特定字母仅的元命令。

## <span id="ddk_meta_meta_command_help_dbg"></span><span id="DDK_META_META_COMMAND_HELP_DBG"></span>


### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>模式</p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>目标</p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p>平台</p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

有关元命令的详细信息，请使用 **. help** 命令。 有关标准命令的详细信息，请使用 [ **？**](---command-help-.md) 。 有关扩展命令的详细信息，请使用 [**！帮助**](-help.md) 扩展。

 

 





