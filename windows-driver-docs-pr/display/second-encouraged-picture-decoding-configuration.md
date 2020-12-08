---
title: 第二个建议的图片解码配置
description: 第二个建议的图片解码配置
keywords:
- 压缩的图片解码设置 WDK DirectX VA
- 图片解码设置 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9ef75cb9943fb4382ae9fe24484ea24c515dd09
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816825"
---
# <a name="second-encouraged-picture-decoding-configuration"></a>第二个建议的图片解码配置


## <span id="ddk_second_encouraged_picture_decoding_configuration_gg"></span><span id="DDK_SECOND_ENCOURAGED_PICTURE_DECODING_CONFIGURATION_GG"></span>


建议的第二个配置提供对脱离主机 IDCT 加速的改进支持。 实现此集内第一个配置的加速器应支持第二个配置。 实现对这两种配置的支持可灵活地使用其加速功能。

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
<td align="left"><p><strong>bConfigHostInverseScan</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

 

 





