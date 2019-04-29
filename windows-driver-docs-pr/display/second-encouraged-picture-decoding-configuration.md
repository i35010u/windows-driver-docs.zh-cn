---
title: 第二个建议的图片解码配置
description: 第二个建议的图片解码配置
ms.assetid: 9e259768-4588-4a5b-b01b-fca0021cd966
keywords:
- 压缩解码集 WDK DirectX VA 的图片
- 图片解码设置 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c8941d02cbc311a0a801df7f972143d610e954e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390492"
---
# <a name="second-encouraged-picture-decoding-configuration"></a>第二个建议的图片解码配置


## <span id="ddk_second_encouraged_picture_decoding_configuration_gg"></span><span id="DDK_SECOND_ENCOURAGED_PICTURE_DECODING_CONFIGURATION_GG"></span>


第二个建议的配置提供了改进了的支持的非主机 IDCT 加速。 在此集中实现的第一个配置的加速器应支持第二个。 实现支持这两个配置提供了可以使用其加速功能的方式的灵活性。

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
<td align="left"><p><strong>bConfigHostInverseScan</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

 

 





