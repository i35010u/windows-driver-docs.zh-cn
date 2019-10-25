---
title: CODECAPI\_视频\_编码器
description: CODECAPI\_视频\_编码器
ms.assetid: e08f26ff-1e11-42a4-a9f8-3af9b885a901
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b75814fd9dbdeccb9a9702a2873129c96b020e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844720"
---
# <a name="codecapi_video_encoder"></a>CODECAPI\_视频\_编码器


## <span id="ddk_codecapi_video_encoder_ks"></span><span id="DDK_CODECAPI_VIDEO_ENCODER_KS"></span>


视频编码器使用此 GUID 的支持（由用户模式 KsProperty BASICSUPPORT 查询）来指示它们是视频编码器。

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
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>无</p></td>
<td><p>Filter</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>型</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 BOOL，并指定微型驱动程序是否支持视频编码。 如果值为**TRUE** ，则表示微型驱动程序支持视频编码。 如果筛选器不是视频编码器，则筛选器不应支持此 GUID。

### <a name="span-idheadersspanspan-idheadersspanheaders"></a><span id="headers"></span><span id="HEADERS"></span>只要

在*ksmedia*中声明。 包括*ksmedia*。

### <a name="requirements"></a>要求

**标头：** 在*ksmedia*中声明。 包括*ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

 





