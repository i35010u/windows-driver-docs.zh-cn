---
title: WIA\_DPA\_CONNECT\_状态
description: WIA\_DPA\_CONNECT\_状态属性包含设备的当前连接状态。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 524fb89a-47a0-44a7-8f21-36e0abcfdd5c
keywords:
- WIA_DPA_CONNECT_STATUS 成像设备
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
ms.openlocfilehash: b1f078ced043e3662b24ddfc7a896938aecea40e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325283"
---
# <a name="wiadpaconnectstatus"></a>WIA\_DPA\_CONNECT\_状态


WIA\_DPA\_CONNECT\_状态属性包含设备的当前连接状态。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_dpa_connect_status_si"></span><span id="DDK_WIA_DPA_CONNECT_STATUS_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

下表列出可能的值对于 WIA\_DPA\_CONNECT\_STATUS 属性。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_DEVICE_NOT_CONNECTED</p></td>
<td><p>未连接设备。</p></td>
</tr>
<tr class="even">
<td><p>WIA_DEVICE_CONNECTED</p></td>
<td><p>设备已连接并且正常运行。</p></td>
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
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





