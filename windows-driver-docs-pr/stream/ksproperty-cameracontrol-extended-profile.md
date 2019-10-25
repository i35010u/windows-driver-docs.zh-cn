---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_配置文件
description: KSPROPERTY\_CAMERACONTROL\_扩展\_配置文件用于允许捕获框架通知照相机驱动程序已选择哪个配置文件。 。
ms.assetid: 15467152-E514-4DAA-9905-2804802291A5
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
ms.openlocfilehash: 4ff90b69dcaba0a6baccfd7698441d868b74820e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824007"
---
# <a name="ksproperty_cameracontrol_extended_profile"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_配置文件

KSPROPERTY\_CAMERACONTROL\_扩展\_配置文件用于允许捕获框架通知照相机驱动程序已选择哪个配置文件。

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
<th>控件</th>
<th>在任务栏的搜索框中键入</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本 1</p></td>
<td><p>Filter</p></td>
<td><p>异步，不可取消</p></td>
</tr>
</tbody>
</table>

下表包含使用控件时[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段的说明和要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>这必须为1。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>必须是 KSCAMERA_EXTENDEDPROP_FILTERSCOPE （0xFFFFFFFF）。</p></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>这必须是 sizeof （KSCAMERA_EXTENDEDPROP_HEADER） + sizeof （KSCAMERA_EXTENDEDPROP_PROFILE）。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须为 KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL。 不支持任何其他模式。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这必须是0。</p></td>
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
