---
title: WIA \_ DPS \_ SHEET \_ 送纸器 \_ 注册
description: WIA \_ DPS \_ 工作表 \_ 进纸器 \_ 注册属性包含放置在扫描仪平板上的文档的注册、对齐和边缘检测。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_DPS_SHEET_FEEDER_REGISTRATION 图像设备
topic_type:
- apiref
api_name:
- WIA_DPS_SHEET_FEEDER_REGISTRATION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c617c44ced82bbab3955e94da65fc1af6b447a3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831727"
---
# <a name="wia_dps_sheet_feeder_registration"></a>WIA \_ DPS \_ SHEET \_ 送纸器 \_ 注册


WIA \_ DPS \_ 工作表 \_ 进纸器 \_ 注册属性包含放置在扫描仪平板上的文档的注册、对齐和边缘检测。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_dps_sheet_feeder_registration_si"></span><span id="DDK_WIA_DPS_SHEET_FEEDER_REGISTRATION_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

WIA \_ DPS \_ SHEET \_ 送纸器 \_ 注册属性指明了如何将文档水平定位在掌上电脑或纸器扫描仪的扫描头上。 扫描程序使用属性来预测用户在扫描头上放置文档的位置。

下表介绍了 WIA \_ DPS \_ 工作表格式 \_ 送纸器注册的有效常量 \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回的常量</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LEFT_JUSTIFIED</p></td>
<td><p>该文档位于扫描头的左侧。</p></td>
</tr>
<tr class="even">
<td><p>界线</p></td>
<td><p>文档在扫描头上居中。</p></td>
</tr>
<tr class="odd">
<td><p>RIGHT_JUSTIFIED</p></td>
<td><p>该文档将定位到与扫描头相关的位置。</p></td>
</tr>
</tbody>
</table>

 

对于支持多个扫描头的扫描仪，WIA \_ DPS \_ 工作表 \_ 进纸器 \_ 注册属性相对于最顶层的扫描头。 对于单张纸、滚动送入和手持扫描仪，此属性是必需的。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>对于 Windows Vista 和更高版本的操作系统，请改用 WIA_IPS_SHEET_FEEDER_REGISTRATION 属性。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ IP \_ 工作 \_ 送纸器 \_ 注册**](wia-ips-sheet-feeder-registration.md)

 

 






