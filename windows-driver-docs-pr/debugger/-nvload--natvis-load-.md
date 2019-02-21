---
title: .nvload （NatVis 加载）
description: .Nvload 命令将 NatVis 文件加载到调试器环境。 加载可视化效果后，它将用于呈现可视化效果中定义的数据。
ms.assetid: 9B14B3B4-EA90-426E-8555-0E5B8F63E0A9
keywords:
- .nvload （NatVis 加载） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .nvload (NatVis Load)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1f4a08aeb8e7676a6759a89726701a6a2f24ae44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544276"
---
# <a name="nvload-natvis-load"></a>.nvload （NatVis 加载）


.Nvload 命令将 NatVis 文件加载到调试器环境。 加载可视化效果后，它将用于呈现可视化效果中定义的数据。

```dbgcmd
.nvload FileName|ModuleName   
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______FileName___ModuleName______"></span><span id="_______filename___modulename______"></span><span id="_______FILENAME___MODULENAME______"></span> *FileName | ModuleName*   
指定的 NatVis 文件名称或要加载的模块名称。

**文件名**是要加载的.natvis 文件的显式名称。 可以使用完全限定的路径。

**ModuleName**是正在调试的目标进程中某个模块的名称。 加载所有符号文件 (PDB) 中嵌入命名的模块名称的 NatVis 文件，如果有任何可用。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息，请参阅[c + + 使用.natvis 文件的写入调试器类型可视化工具](https://code.msdn.microsoft.com/windowsdesktop/Writing-type-visualizers-2eae77a2)。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**dx （显示 NatVis 表达式）**](dx--display-visualizer-variables-.md)

 

 






