---
title: 第三个建议的图片解码配置
description: 第三个建议的图片解码配置
ms.assetid: 9f905030-9fc9-4a5f-8cf5-a36c7861be52
keywords:
- 压缩解码集 WDK DirectX VA 的图片
- 图片解码设置 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5e5c5ed5e55cc7efd9f3e86c4cf1fbce0bce12a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389888"
---
# <a name="third-encouraged-picture-decoding-configuration"></a>第三个建议的图片解码配置


## <span id="ddk_third_encouraged_picture_decoding_configuration_gg"></span><span id="DDK_THIRD_ENCOURAGED_PICTURE_DECODING_CONFIGURATION_GG"></span>


第三个建议的配置提供了对预期在某些实现中的非主机 IDCT 的支持。 对于解码器鼓励，此配置。 但是，第二个配置是首选的加速器。

此配置定义一样[解码配置的第一张图](first-picture-decoding-configuration.md)有以下例外。

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
<td align="left"><p><strong>bConfigMBcontrolRasterOrder</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigResidDiffHost</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bConfigResidDiffAccelerator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfig4GroupedCoefs</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

 

 





