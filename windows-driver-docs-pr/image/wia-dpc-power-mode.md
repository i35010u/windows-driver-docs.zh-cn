---
title: WIA\_DPC\_电源\_模式
description: WIA\_DPC\_电源\_模式属性定义摄像机设备的当前电源。
ms.assetid: b99d9ebc-6a1f-4bfc-be3a-07dba5b38186
keywords:
- WIA_DPC_POWER_MODE 成像设备
topic_type:
- apiref
api_name:
- WIA_DPC_POWER_MODE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71a09fae56d34b7259a6fc8a423c7adfe32d7606
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392563"
---
# <a name="wiadpcpowermode"></a>WIA\_DPC\_电源\_模式


WIA\_DPC\_电源\_模式属性定义摄像机设备的当前电源。

## <span id="ddk_wia_dpc_power_mode_si"></span><span id="DDK_WIA_DPC_POWER_MODE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

应用程序读取 WIA\_DPC\_电源\_使用模式属性以确定哪些 power 源照相机。

下表描述了有效使用 WIA 的常量\_DPC\_电源\_模式。

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
<td><p>POWERMODE_BATTERY</p></td>
<td><p>照相机设备电池电源运行。</p></td>
</tr>
<tr class="even">
<td><p>POWERMODE_LINE</p></td>
<td><p>照相机设备正在运行的电源适配器。</p></td>
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
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本操作系统中已过时，并应不再使用。 但是，此属性仍定义 Windows Vista 中与应用程序和用于 Windows Server 2003、 Windows XP 和早期版本的 Windows 设备的兼容性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





