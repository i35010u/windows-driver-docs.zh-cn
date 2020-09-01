---
title: CODECAPI \_ 视频 \_ 编码器
description: CODECAPI \_ 视频 \_ 编码器
ms.assetid: e08f26ff-1e11-42a4-a9f8-3af9b885a901
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2da4844e6829e02cef91ad1b5564db9845a4b44
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186353"
---
# <a name="codecapi_video_encoder"></a>CODECAPI \_ 视频 \_ 编码器


## <span id="ddk_codecapi_video_encoder_ks"></span><span id="DDK_CODECAPI_VIDEO_ENCODER_KS"></span>


视频编码器使用用户模式 KsProperty BASICSUPPORT) 查询的此 GUID (，以指示它们是视频编码器。

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
<th>获取</th>
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
<td><p>筛选器</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

操作数据) 的属性值 (为 BOOL 类型，并指定微型驱动程序是否支持视频编码。 如果值为 **TRUE** ，则表示微型驱动程序支持视频编码。 如果筛选器不是视频编码器，则筛选器不应支持此 GUID。

### <a name="span-idheadersspanspan-idheadersspanheaders"></a><span id="headers"></span><span id="HEADERS"></span>只要

在 *ksmedia*中声明。 包括 *ksmedia*。

### <a name="requirements"></a>要求

**标头：** 在 *ksmedia*中声明。 包括 *ksmedia*。

### <a name="see-also"></a>另请参阅

[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

 

