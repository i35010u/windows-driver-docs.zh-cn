---
title: KSPROPERTY\_CAMERACONTROL\_泄露
description: 用户模式客户端使用 KSPROPERTY\_CAMERACONTROL\_曝露属性来获取或设置数码相机的曝光时间。 此属性为可选项。
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
ms.openlocfilehash: 2c3d723b1ea0c50afdaba409a58d75ae38065967
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843248"
---
# <a name="ksproperty_cameracontrol_exposure"></a>KSPROPERTY\_CAMERACONTROL\_泄露


用户模式客户端使用 KSPROPERTY\_CAMERACONTROL\_曝露属性来获取或设置数码相机的曝光时间。 此属性为可选项。

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

 

属性值（操作数据）是指定曝光长度的 LONG。

此值用对数基数2秒表示，因此，对于小于零的值，公开时间为 1/2n 秒。 对于正值和零，曝光时间为2n 秒。 例如：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
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
<td><p>wget-1.12-5.el6</p></td>
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

KSPROPERTY\_CAMERACONTROL\_S 结构的**值**成员指定了公开的长度。

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

 

 






