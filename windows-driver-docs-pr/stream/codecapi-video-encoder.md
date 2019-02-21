---
title: CODECAPI\_视频\_编码器
description: CODECAPI\_视频\_编码器
ms.assetid: e08f26ff-1e11-42a4-a9f8-3af9b885a901
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85c5984822ce79b91000dba0eadff1fdefd9b5cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556169"
---
# <a name="codecapivideoencoder"></a>CODECAPI\_视频\_编码器


## <span id="ddk_codecapi_video_encoder_ks"></span><span id="DDK_CODECAPI_VIDEO_ENCODER_KS"></span>


视频编码器使用的支持 （由用户模式下 KsProperty BASICSUPPORT 查询） 此 GUID 来表示他们对视频编码器。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>Filter</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 的类型 BOOL 和指定微型驱动程序是否支持视频编码。 值为 **，则返回 TRUE**指示微型驱动程序支持视频编码。 如果不是视频编码器，该筛选器应支持此 GUID。

### <a name="span-idheadersspanspan-idheadersspanheaders"></a><span id="headers"></span><span id="HEADERS"></span>标头

在中声明*ksmedia.h*。 包括*ksmedia.h*。

### <a name="requirements"></a>要求

**标头：** 在中声明*ksmedia.h*。 包括*ksmedia.h*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 





