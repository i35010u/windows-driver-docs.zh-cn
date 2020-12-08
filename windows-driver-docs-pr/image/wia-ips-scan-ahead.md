---
title: WIA \_ IP \_ \_ 提前扫描
description: 使用 "WIA \_ ip \_ 扫描提前" 属性，可以在 \_ 硬件设备中提前扫描 (扫描速度最快，缓冲扫描程序内部内存中的扫描图像，以相同或较低的速度将缓冲图像以相同或较低的速度传输到客户端应用程序) 。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPS_SCAN_AHEAD 图像设备
topic_type:
- apiref
api_name:
- WIA_IPS_SCAN_AHEAD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cbbc0a26ef780a23e71e617a4a5d3009595a25e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808727"
---
# <a name="wia_ips_scan_ahead"></a>WIA \_ IP \_ \_ 提前扫描


使用 " **WIA \_ ip \_ 扫描 \_ 提前** " 属性，可以在硬件设备中提前扫描 (扫描速度最快，缓冲扫描程序内部内存中的扫描图像，以相同或较低的速度将缓冲图像以相同或较低的速度传输到客户端应用程序) 。 WIA 微型驱动程序创建并维护此属性。




**注意**  此属性取代了 [**WIA \_ DPS \_ SCAN \_ 提前 \_ 页面**](wia-dps-scan-ahead-pages.md)，这现在已过时。

 

属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

下表描述了 " **WIA \_ ip \_ \_ 提前扫描** " 属性的有效值。

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
<td><p>WIA_SCAN_AHEAD_DISABLED</p></td>
<td><p>已禁用扫描。 如果支持该属性，则这是所需的默认值。</p></td>
</tr>
<tr class="even">
<td><p>WIA_SCAN_AHEAD_ENABLED</p></td>
<td><p>启用预扫描。 WIA 客户端应用程序必须尽可能快地下载映像。 如果扫描作业在完成之前被取消，某些扫描的文档可能会丢失， (尚未传输到应用程序) 。</p></td>
</tr>
</tbody>
</table>

 

此属性仅对 (WIA 类别送纸器) 的进纸器项有效 \_ \_ ，并且是可选的。

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

## <a name="see-also"></a>请参阅


[**WIA \_ DPS \_ \_ 提前扫描 \_ 页面**](wia-dps-scan-ahead-pages.md)

 

 






