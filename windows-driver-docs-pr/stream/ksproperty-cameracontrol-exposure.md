---
title: KSPROPERTY \_ CAMERACONTROL \_ 曝露
description: 用户模式客户端使用 KSPROPERTY \_ CAMERACONTROL \_ 公开的属性获取或设置数码相机的曝光时间。 此属性是可选的。
ms.assetid: e9ad7a82-0c2d-46e5-a5d5-9f33848f129c
keywords:
- KSPROPERTY_CAMERACONTROL_EXPOSURE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXPOSURE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc0a1f366a3f006f44897a4014c04d98b3b4a048
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190542"
---
# <a name="ksproperty_cameracontrol_exposure"></a>KSPROPERTY \_ CAMERACONTROL \_ 曝露


用户模式客户端使用 KSPROPERTY \_ CAMERACONTROL \_ 公开的属性获取或设置数码相机的曝光时间。 此属性是可选的。

## <span id="ddk_ksproperty_cameracontrol_exposure_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_EXPOSURE_KS"></span>


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
<td><p>是</p></td>
<td><p>筛选器或节点</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是指定曝光长度的长时间。

此值用对数基数2秒表示，因此，对于小于零的值，公开时间为 1/2n 秒。 对于正值和零，曝光时间为2n 秒。 例如：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>秒</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>-7</p></td>
<td><p>1/128</p></td>
</tr>
<tr class="even">
<td><p>-6</p></td>
<td><p>1/64</p></td>
</tr>
<tr class="odd">
<td><p>-5</p></td>
<td><p>1/32</p></td>
</tr>
<tr class="even">
<td><p>-4</p></td>
<td><p>1/16</p></td>
</tr>
<tr class="odd">
<td><p>-3</p></td>
<td><p>1/8</p></td>
</tr>
<tr class="even">
<td><p>-2</p></td>
<td><p>1/4</p></td>
</tr>
<tr class="odd">
<td><p>-1</p></td>
<td><p>1/2</p></td>
</tr>
<tr class="even">
<td><p>0</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>1</p></td>
<td><p>2</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KSPROPERTY **Value** \_ CAMERACONTROL S 结构的值成员 \_ 指定了公开的长度。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ CAMERACONTROL \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)

 

