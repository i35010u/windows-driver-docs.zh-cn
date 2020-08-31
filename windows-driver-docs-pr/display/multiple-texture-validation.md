---
title: 多纹理验证
description: 多纹理验证
ms.assetid: 3f56f7c1-89d6-40d0-9540-b6280379ddc5
keywords:
- 多纹理 WDK Direct3D，验证
- 纹理管理 WDK Direct3D，验证
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf4b7b3161ee5ac5cee9855adb979f610336f22e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063868"
---
# <a name="multiple-texture-validation"></a>多纹理验证


## <span id="ddk_multiple_texture_validation_gg"></span><span id="DDK_MULTIPLE_TEXTURE_VALIDATION_GG"></span>


当前硬件不一定实现 Direct3D 可以表达的所有内容。 应用程序通过先设置所需的混合模式，然后调用 **IDirect3DDevice7：： ValidateDevice** 方法来确定是否可以执行特定的混合操作。 驱动程序必须在初始化时准确报告其功能，并支持 [**D3dValidateTextureStageState**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb) 以允许验证其功能。 验证还涵盖在 TBLEND 级别指定的操作。 有关 **IDirect3DDevice7：： ValidateDevice**的详细信息，请参阅 Direct3D SDK 文档。

下表列出了 **IDirect3DDevice7：： ValidateDevice**的返回代码。

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
<td align="left"><p>硬件无法同时执行 trilinear 筛选和多纹理操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TOOMANYOPERATIONS</p></td>
<td align="left"><p>硬件无法处理指定数量的选项。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UNSUPPORTEDALPHAARG</p></td>
<td align="left"><p>不支持指定的 alpha 参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>UNSUPPORTEDALPHAOPERATION</p></td>
<td align="left"><p>指定的 alpha 操作不受支持。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UNSUPPORTEDCOLORARG</p></td>
<td align="left"><p>不支持指定的颜色参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>UNSUPPORTEDCOLOROPERATION</p></td>
<td align="left"><p>不支持指定的颜色操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UNSUPPORTEDFACTORVALUE</p></td>
<td align="left"><p>硬件不支持 D3DTA_TFACTOR 大于1.0。</p></td>
</tr>
<tr class="even">
<td align="left"><p>WRONGTEXTUREFORMAT</p></td>
<td align="left"><p>硬件不支持所选纹理格式的当前状态。</p></td>
</tr>
</tbody>
</table>

 

 

