---
title: 多纹理验证
description: 多纹理验证
ms.assetid: 3f56f7c1-89d6-40d0-9540-b6280379ddc5
keywords:
- 多个纹理 WDK Direct3D，验证
- 纹理管理 WDK Direct3D，验证
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b3aad9defcd7bdde4ee29df6c799f8db3bfb4bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372828"
---
# <a name="multiple-texture-validation"></a>多纹理验证


## <span id="ddk_multiple_texture_validation_gg"></span><span id="DDK_MULTIPLE_TEXTURE_VALIDATION_GG"></span>


当前硬件不一定实现 Direct3D 可以表示的所有内容。 应用程序确定是否可以由第一个设置所需的混合模式，并调用执行特定的混合操作**IDirect3DDevice7::ValidateDevice**方法。 该驱动程序必须在初始化时和支持准确地报告其功能[ **D3dValidateTextureStageState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)以允许要验证其功能。 验证还介绍了在 TBLEND 级别指定的操作。 璝惠**IDirect3DDevice7::ValidateDevice**，请参阅 Direct3D SDK 文档。

下表列出的返回代码**IDirect3DDevice7::ValidateDevice**。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回代码</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CONFLICTINGTEXTUREFILTER</p></td>
<td align="left"><p>硬件不能执行三线性筛选和在同一时间的多个纹理。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TOOMANYOPERATIONS</p></td>
<td align="left"><p>硬件不能处理指定的数目的选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UNSUPPORTEDALPHAARG</p></td>
<td align="left"><p>不支持指定的 alpha 参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>UNSUPPORTEDALPHAOPERATION</p></td>
<td align="left"><p>不支持指定的 alpha 操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UNSUPPORTEDCOLORARG</p></td>
<td align="left"><p>指定的颜色参数不受支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>UNSUPPORTEDCOLOROPERATION</p></td>
<td align="left"><p>指定的颜色操作是不受支持。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UNSUPPORTEDFACTORVALUE</p></td>
<td align="left"><p>硬件不能支持 D3DTA_TFACTOR 大于 1.0。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WRONGTEXTUREFORMAT</p></td>
<td align="left"><p>硬件不能在所选的纹理格式中支持的当前状态。</p></td>
</tr>
</tbody>
</table>

 

 

 





