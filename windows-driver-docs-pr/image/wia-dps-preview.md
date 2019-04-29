---
title: WIA\_DPS\_预览
description: WIA\_DPS\_预览属性指示设备的预览模式。 应用程序设置此属性以将设备置于预览模式。
ms.assetid: 410f58c0-479c-44ab-8126-a5dec79b713b
keywords:
- WIA_DPS_PREVIEW 成像设备
topic_type:
- apiref
api_name:
- WIA_DPS_PREVIEW
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 038d564ad4f6055164d63f4af1cf0921493c8553
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366989"
---
# <a name="wiadpspreview"></a>WIA\_DPS\_预览


WIA\_DPS\_预览属性指示设备的预览模式。 应用程序设置此属性以将设备置于预览模式。

## <span id="ddk_wia_dps_preview_si"></span><span id="DDK_WIA_DPS_PREVIEW_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

下表描述了有效使用 WIA 的常量\_DPS\_预览属性。

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
<td><p>WIA_FINAL_SCAN</p></td>
<td><p>应用程序将执行最后一个扫描。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PREVIEW_SCAN</p></td>
<td><p>应用程序将执行预览扫描。</p></td>
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
<td><p>适用于 Microsoft Windows XP。 适用于 Windows Vista 及更高版本，使用相同的 WIA_IPS_PREVIEW 属性。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IP\_预览**](wia-ips-preview.md)

 

 






