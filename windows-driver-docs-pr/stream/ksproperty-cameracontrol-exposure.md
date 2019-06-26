---
title: KSPROPERTY\_CAMERACONTROL\_风险
description: 用户模式下客户端使用 KSPROPERTY\_CAMERACONTROL\_公开属性来获取或设置数字照相机的暴露时间。 此属性为可选项。
ms.assetid: e9ad7a82-0c2d-46e5-a5d5-9f33848f129c
keywords:
- KSPROPERTY_CAMERACONTROL_EXPOSURE 流式处理媒体设备
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
ms.openlocfilehash: e51e3473799bcbece8b53f5146a0e5fba2efd516
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355388"
---
# <a name="kspropertycameracontrolexposure"></a>KSPROPERTY\_CAMERACONTROL\_风险


用户模式下客户端使用 KSPROPERTY\_CAMERACONTROL\_公开属性来获取或设置数字照相机的暴露时间。 此属性为可选项。

## <span id="ddk_ksproperty_cameracontrol_exposure_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_EXPOSURE_KS"></span>


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
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>筛选器或节点</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定的风险的长度长时间。

此值表示为在日志中基本 2 秒，因此，对于值小于零的暴露时间是 1/2n 秒。 对于正值和零的暴露时间是 2n 秒。 例如：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
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

**值**KSPROPERTY 成员\_CAMERACONTROL\_S 结构指定的长度的风险。

每个视频捕获微型驱动程序支持此属性必须定义此属性为其自身范围和默认值。

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

[**KSPROPERTY\_CAMERACONTROL\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)

 

 






