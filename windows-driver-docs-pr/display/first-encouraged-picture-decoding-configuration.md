---
title: 第一个建议的图片解码配置
description: 第一个建议的图片解码配置
keywords:
- 压缩的图片解码设置 WDK DirectX VA
- 图片解码设置 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f35fd29af6347097169dd1d067de41caf81a5da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808457"
---
# <a name="first-encouraged-picture-decoding-configuration"></a>第一个建议的图片解码配置


## <span id="ddk_first_encouraged_picture_decoding_configuration_gg"></span><span id="DDK_FIRST_ENCOURAGED_PICTURE_DECODING_CONFIGURATION_GG"></span>


第一种建议的配置是为了改进对脱离主机位流处理加速度的支持。

此配置的定义方式与 [第一个图片解码配置](first-picture-decoding-configuration.md) 相同，但有以下例外情况。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>bConfigBitstreamRaw</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigMBcontrolRasterOrder</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bConfigResidDiffHost</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
</tbody>
</table>

 

 

 





