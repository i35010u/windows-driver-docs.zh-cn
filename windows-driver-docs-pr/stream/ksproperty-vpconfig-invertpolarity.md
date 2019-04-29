---
title: KSPROPERTY\_VPCONFIG\_INVERTPOLARITY
description: KSPROPERTY\_VPCONFIG\_INVERTPOLARITY 属性切换强制反转的视频端口的极性全局标志。
ms.assetid: c0b69aa4-0f81-42b4-9a69-5afcf702f5f1
keywords:
- KSPROPERTY_VPCONFIG_INVERTPOLARITY 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_INVERTPOLARITY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: abbe2f20956b3d68b70570f37b97bd7c0bd234e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355509"
---
# <a name="kspropertyvpconfiginvertpolarity"></a>KSPROPERTY\_VPCONFIG\_INVERTPOLARITY


KSPROPERTY\_VPCONFIG\_INVERTPOLARITY 属性切换强制反转的视频端口的极性全局标志。

## <span id="ddk_ksproperty_vpconfig_invertpolarity_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_INVERTPOLARITY_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>布尔</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一个布尔值。 指定 **，则返回 TRUE**反转极性，或指定**FALSE**以免反转极性。

<a name="remarks"></a>备注
-------

KSPROPERTY\_VPCONFIG\_INVERTPOLARITY 属性请求返回状态\_成功以指示成功完成。 否则，请求将返回相应的错误状态代码。

此功能涉及到硬件，因为不使用此功能的模型必须返回状态\_不\_实现。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






