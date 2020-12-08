---
title: WIA \_ DPA \_ 连接 \_ 状态
description: WIA \_ DPA \_ 连接 \_ 状态属性包含设备的当前连接状态。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_DPA_CONNECT_STATUS 图像设备
topic_type:
- apiref
api_name:
- WIA_DPA_CONNECT_STATUS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d281a50e7d9c90b512f9fe76cf5d657f34507e52
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808741"
---
# <a name="wia_dpa_connect_status"></a>WIA \_ DPA \_ 连接 \_ 状态


WIA \_ DPA \_ 连接 \_ 状态属性包含设备的当前连接状态。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_dpa_connect_status_si"></span><span id="DDK_WIA_DPA_CONNECT_STATUS_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

下表列出了 WIA \_ DPA \_ 连接状态属性的可能值 \_ 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_DEVICE_NOT_CONNECTED</p></td>
<td><p>设备未连接。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DEVICE_CONNECTED</p></td>
<td><p>设备已连接并且可操作。</p></td>
</tr>
</tbody>
</table>

 

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
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

 

 





