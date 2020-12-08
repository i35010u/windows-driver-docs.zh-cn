---
title: WIA \_ DIP \_ 开发 \_ 类型
description: WIA \_ DIP \_ 开发 \_ 类型属性包含设备类型和设备子类型。
keywords:
- WIA_DIP_DEV_TYPE 图像设备
topic_type:
- apiref
api_name:
- WIA_DIP_DEV_TYPE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b807ebc22960d8ac0e5d09759cc77bc7a0b337e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824523"
---
# <a name="wia_dip_dev_type"></a>WIA \_ DIP \_ 开发 \_ 类型


WIA \_ DIP \_ 开发 \_ 类型属性包含设备类型和设备子类型。 WIA 服务创建并维护此属性

## <span id="ddk_wia_dip_dev_type_si"></span><span id="DDK_WIA_DIP_DEV_TYPE_SI"></span>


属性类型： VT \_ I4

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

设备类型和子类型是从设备文件的驱动程序 INF 文件中获取的。 应用程序读取 WIA \_ DIP \_ 开发 \_ 类型属性，以确定它使用的是扫描仪、照相机还是视频设备。

下表描述了设备类型的可能值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>设备类型</th>
<th>值</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>StiDeviceTypeDefault</strong></p></td>
<td><p>0x0000</p></td>
<td><p>默认设备</p></td>
</tr>
<tr class="even">
<td><p><strong>StiDeviceTypeScanner</strong></p></td>
<td><p>0x0001</p></td>
<td><p>扫描仪设备</p></td>
</tr>
<tr class="odd">
<td><p><strong>StiDeviceTypeDigitalCamera</strong></p></td>
<td><p>0x0002</p></td>
<td><p>照相机设备</p></td>
</tr>
<tr class="even">
<td><p><strong>StiDeviceTypeStreamingVideo</strong></p></td>
<td><p>0x0003</p></td>
<td><p>视频设备</p></td>
</tr>
</tbody>
</table>

 

有关 INF 文件的详细信息，请参阅 [WIA 设备的 INF 文件](./inf-files-for-wia-devices.md)。 **StiDeviceType**_Xxx_ 常量在 *Sti* 中定义。

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

 

