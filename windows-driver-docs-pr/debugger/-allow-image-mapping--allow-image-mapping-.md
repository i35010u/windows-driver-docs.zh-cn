---
title: .allow_image_mapping（允许映像映射）
description: .Allow_image_mapping 命令控制是否将映射图像文件。
keywords:
- .allow_image_mapping (允许) Windows 调试的图像映射
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- .allow_image_mapping (Allow Image Mapping)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 66299a1f4dde2385842857ba6e521c4240b9e258
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800135"
---
# <a name="allow_image_mapping-allow-image-mapping"></a>。允许 \_ 图像 \_ 映射 (允许图像映射) 


" **允许 \_ 图像 \_ 映射** " 命令控制是否将映射图像文件。

```dbgcmd
    .allow_image_mapping [/r] 0 
    .allow_image_mapping [/r] 1 
    .allow_image_mapping 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="________r______"></span><span id="________R______"></span>**/r**   
重载调试器的模块列表中的所有模块。 这等效于 [**. reload.sql/d**](-reload--reload-module-.md)。

<span id="_______0______"></span>**0**   
阻止图像文件被映射。

<span id="_______1______"></span>**1**   
允许映射映像文件。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式和内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果没有参数，则 " **允许 \_ 映像 \_ 映射** " 将显示当前是否允许图像文件映射。 默认情况下，允许该映射。

调试小型转储时，图像映射最常见。 如果 Dbghelp.dll 无法访问调试记录，也可能会发生映像映射 (例如，在内存已) 的情况下进行内核调试。

 

 





