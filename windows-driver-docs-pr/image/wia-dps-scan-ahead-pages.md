---
title: WIA\_DPS\_扫描\_预先\_页
description: WIA\_DPS\_扫描\_预先\_页属性包含一个值，指示扫描仪是否将发送到应用程序之前缓存的扫描程序缓冲区中的页。
ms.assetid: 8c00b029-dc9f-43e1-af4a-088e143351ca
keywords:
- WIA_DPS_SCAN_AHEAD_PAGES 成像设备
topic_type:
- apiref
api_name:
- WIA_DPS_SCAN_AHEAD_PAGES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0f790ff1ac1c5ea87bf6a073c411b70ad7adbae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577142"
---
# <a name="wiadpsscanaheadpages"></a>WIA\_DPS\_扫描\_预先\_页


WIA\_DPS\_扫描\_预先\_页属性包含一个值，指示扫描仪是否将发送到应用程序之前缓存的扫描程序缓冲区中的页。

## <span id="ddk_wia_dps_scan_ahead_pages_si"></span><span id="DDK_WIA_DPS_SCAN_AHEAD_PAGES_SI"></span>


**请注意**  此属性现已过时。 使用[ **WIA\_IPS\_扫描\_预先**](wia-ips-scan-ahead.md)相反。

 

属性类型：VT\_I4

有效值：WIA\_PROP\_范围 （从 0 到文档送纸器可容纳最大页数)

访问权限：读取/写入

<a name="remarks"></a>备注
-------

如果 WIA\_DPS\_扫描\_预先\_页属性为零，继续扫描已禁用，并且扫描程序将不继续扫描的任何页面。

如果扫描程序扫描预缓冲项上执行数据传输，扫描程序将检索缓冲的页面。 扫描预操作期间，不能更改 WIA 属性。 WIA\_DPS\_扫描\_预先\_页是可选的。

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

## <a name="see-also"></a>请参阅


[**WIA\_IPS\_SCAN\_AHEAD**](wia-ips-scan-ahead.md)

 

 






