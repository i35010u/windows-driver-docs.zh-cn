---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 配置文件
description: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 配置文件用于允许捕获框架通知照相机驱动程序已选择哪个配置文件。 .
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PROFILE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PROFILE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: adf0570647460dceb5c9ad6c5976097024f0a0b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837853"
---
# <a name="ksproperty_cameracontrol_extended_profile"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 配置文件

KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ 配置文件用于允许捕获框架通知照相机驱动程序已选择哪个配置文件。

## <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>范围</th>
<th>控制</th>
<th>类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本 1</p></td>
<td><p>筛选器</p></td>
<td><p>异步，不可取消</p></td>
</tr>
</tbody>
</table>

下表包含使用控件时 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构字段的说明和要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>这必须为1。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>必须 (0xFFFFFFFF) KSCAMERA_EXTENDEDPROP_FILTERSCOPE。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_PROFILE) 。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须 KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL。 不支持任何其他模式。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>此属性必须为 0。</p></td>
</tr>
</tbody>
</table>

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
