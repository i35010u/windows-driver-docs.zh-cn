---
title: 第七个图片解码配置
description: 第七个图片解码配置
ms.assetid: eb52cdb4-4009-4860-80ac-5c2172f8a9b3
keywords:
- 压缩的图片解码设置 WDK DirectX VA
- 图片解码设置 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75562285ee5566f8c6de178beadfdec7ecaea8c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825731"
---
# <a name="seventh-picture-decoding-configuration"></a>第七个图片解码配置


## <span id="ddk_seventh_picture_decoding_configuration_gg"></span><span id="DDK_SEVENTH_PICTURE_DECODING_CONFIGURATION_GG"></span>


此集中的第七个配置仅为[**DXVA\_ConnectMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_connectmode)结构中指示[\_C](mpeg2-c.md)和[mpeg2\_D](mpeg2-d.md)受限配置文件定义。 在最小互操作集中，任何其他受限制的配置文件都不包括此配置。

此配置（不是首选配置）的定义方式与[第一个图片解码配置](first-picture-decoding-configuration.md)相同，但以下情况例外。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>bConfigResidDiffHost</strong></p></td>
<td align="left"><p>无</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigResidDiffAccelerator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bConfig4GroupedCoefs</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

 

 





