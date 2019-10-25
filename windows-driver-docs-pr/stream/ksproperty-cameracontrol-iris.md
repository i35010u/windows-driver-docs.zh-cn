---
title: KSPROPERTY\_CAMERACONTROL\_IRIS
description: 用户模式客户端使用 KSPROPERTY\_CAMERACONTROL\_IRIS 属性来获取或设置照相机的口径设置。 此属性为可选项。
ms.assetid: 000fc146-f6bb-490b-93b6-ebf5ad83b92f
keywords:
- KSPROPERTY_CAMERACONTROL_IRIS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_IRIS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f253bbf55246c813ee9fe0fd48b8fd57df9565c8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843348"
---
# <a name="ksproperty_cameracontrol_iris"></a>KSPROPERTY\_CAMERACONTROL\_IRIS


用户模式客户端使用 KSPROPERTY\_CAMERACONTROL\_IRIS 属性来获取或设置照相机的口径设置。 此属性为可选项。

## <span id="ddk_ksproperty_cameracontrol_iris_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_IRIS_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

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
<td><p>“是”</p></td>
<td><p>筛选器或节点</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>漫长</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是指定相机口径设置的 LONG。 此值以 fstop \* 10 的单位表示。

<a name="remarks"></a>备注
-------

KSPROPERTY\_CAMERACONTROL\_S 结构的**值**成员指定了相机的口径设置。

支持此属性的每个视频捕获微型驱动程序都必须为此属性定义其自己的范围和默认值。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_CAMERACONTROL\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)

 

 






