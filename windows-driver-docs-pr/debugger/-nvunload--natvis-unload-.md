---
title: .nvunload (NatVis Unload)
description: .Nvunload 命令将卸载调试器环境中的 NatVis 文件。
ms.assetid: E63BE2B5-291B-4F78-98FF-C1D7663A184E
keywords:
- .nvunload (NatVis Unload) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .nvunload (NatVis Unload)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 00b7e084694d3430bf84e3c8859a0674d4f0ba55
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523604"
---
# <a name="nvunload-natvis-unload"></a>.nvunload (NatVis Unload)


.Nvunload 命令将卸载调试器环境中的 NatVis 文件。

```dbgcmd
.nvunload FileName|ModuleName  
```

<span id="_______FileName___ModuleName______"></span><span id="_______filename___modulename______"></span><span id="_______FILENAME___MODULENAME______"></span> *FileName | ModuleName*   
指定的 NatVis 文件名称或要卸载的模块名称。

**文件名**是要卸载的.natvis 文件的显式名称。 可以使用完全限定的路径。

**ModuleName**是正在调试的目标进程中某个模块的名称。 命名的模块名称的符号文件 (PDB) 中嵌入的所有 NatVis 文件都都会被卸载。

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

 

 






