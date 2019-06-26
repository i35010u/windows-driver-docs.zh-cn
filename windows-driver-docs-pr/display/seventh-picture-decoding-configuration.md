---
title: 第七个图片解码配置
description: 第七个图片解码配置
ms.assetid: eb52cdb4-4009-4860-80ac-5c2172f8a9b3
keywords:
- 压缩解码集 WDK DirectX VA 的图片
- 图片解码设置 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 568196b940beff4cf2cb704c12ae7aa9d0977c19
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365518"
---
# <a name="seventh-picture-decoding-configuration"></a>第七个图片解码配置


## <span id="ddk_seventh_picture_decoding_configuration_gg"></span><span id="DDK_SEVENTH_PICTURE_DECODING_CONFIGURATION_GG"></span>


在此集中的第七个配置定义仅[MPEG2\_C](mpeg2-c.md)并[MPEG2\_D](mpeg2-d.md)受限制的配置文件所示[ **DXVA\_ConnectMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_connectmode)结构。 没有其他受限制的配置文件在其最小互操作性的一组中包括此配置。

此配置 （这不是首选的配置） 的定义一样[解码配置的第一张图](first-picture-decoding-configuration.md)有以下例外。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>bConfigResidDiffHost</strong></p></td>
<td align="left"><p>零</p></td>
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

 

 

 





