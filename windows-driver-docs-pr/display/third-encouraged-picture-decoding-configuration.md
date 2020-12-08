---
title: 第三个建议的图片解码配置
description: 第三个建议的图片解码配置
keywords:
- 压缩的图片解码设置 WDK DirectX VA
- 图片解码设置 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63fce5a74aac9469bcc1a36ff6483ef2dd624fb8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801801"
---
# <a name="third-encouraged-picture-decoding-configuration"></a>第三个建议的图片解码配置


## <span id="ddk_third_encouraged_picture_decoding_configuration_gg"></span><span id="DDK_THIRD_ENCOURAGED_PICTURE_DECODING_CONFIGURATION_GG"></span>


第三种建议配置提供对在某些实现中预期的非托管 IDCT 的支持。 建议将此配置用于解码器。 但是，第二个配置是加速器的首选。

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

 

 

 





