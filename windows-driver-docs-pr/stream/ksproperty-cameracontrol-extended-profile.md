---
title: KSPROPERTY\_CAMERACONTROL\_扩展\_配置文件
description: KSPROPERTY\_CAMERACONTROL\_扩展\_使用配置文件以允许捕获框架以通知照相机驱动程序选择了哪个配置文件。 .
ms.assetid: 15467152-E514-4DAA-9905-2804802291A5
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PROFILE 流式处理媒体设备
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
ms.openlocfilehash: fb3a15ff015592a8e4e11a6fdb2b76c43bf67ee0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351854"
---
# <a name="kspropertycameracontrolextendedprofile"></a>KSPROPERTY\_CAMERACONTROL\_扩展\_配置文件

KSPROPERTY\_CAMERACONTROL\_扩展\_使用配置文件以允许捕获框架以通知照相机驱动程序选择了哪个配置文件。

## <a name="usage-summary-table"></a>使用率摘要表

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
<td><p>异步、 未取消</p></td>
</tr>
</tbody>
</table>

下表包含的说明和要求[ **KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)结构字段时使用的控件。

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
<td><p>Version</p></td>
<td><p>这必须是 1。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>必须是 KSCAMERA_EXTENDEDPROP_FILTERSCOPE (0xFFFFFFFF)。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof(KSCAMERA_EXTENDEDPROP_HEADER) + sizeof(KSCAMERA_EXTENDEDPROP_PROFILE)。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示最后一个设置操作的错误结果。 如果未设置操作发生，这必须为 0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须是 KSCAMERA_EXTENDEDPROP_CAPS_ASYNCCONTROL。 不支持任何其他模式。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这必须是 0。</p></td>
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
<td><p>Header</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
