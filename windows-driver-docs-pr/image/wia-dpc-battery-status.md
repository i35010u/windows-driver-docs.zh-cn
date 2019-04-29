---
title: WIA\_DPC\_电池\_状态
description: WIA\_DPC\_电池\_STATUS 属性定义剩下要运行照相机设备的电池电量的百分比。
ms.assetid: d6e50c77-9c30-4091-9d6e-7215907ba87b
keywords:
- WIA_DPC_BATTERY_STATUS 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_BATTERY_STATUS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 677b50e28c9b68acf85a35b15a3431399ac1f524
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382304"
---
# <a name="wiadpcbatterystatus"></a>WIA\_DPC\_电池\_状态


WIA\_DPC\_电池\_STATUS 属性定义剩下要运行照相机设备的电池电量的百分比。

## <span id="ddk_wia_dpc_battery_status_si"></span><span id="DDK_WIA_DPC_BATTERY_STATUS_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

值 WIA\_DPC\_电池\_STATUS 属性应为介于 0 到 100 的整数。 应用程序读取此属性以确定电池剩余寿命的摄像机设备。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本操作系统中已过时，并应不再使用。 但是，此属性仍定义 Windows Vista 中与应用程序和用于 Windows Server 2003、 Windows XP 和早期版本的 Windows 设备的兼容性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





