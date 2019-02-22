---
title: WIA\_DIP\_开发人员\_类型
description: WIA\_DIP\_开发人员\_类型属性包含设备类型和设备子类型。
ms.assetid: 685c1cfa-cc3b-42e6-aef3-359ae7220715
keywords:
- WIA_DIP_DEV_TYPE 成像设备
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
ms.openlocfilehash: 05657209ef6c2cad47d7da062a303900261cacf7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543168"
---
# <a name="wiadipdevtype"></a>WIA\_DIP\_开发人员\_类型


WIA\_DIP\_开发人员\_类型属性包含设备类型和设备子类型。 WIA 服务创建和维护此属性

## <span id="ddk_wia_dip_dev_type_si"></span><span id="DDK_WIA_DIP_DEV_TYPE_SI"></span>


属性类型：VT\_I4

有效值：WIA\_PROP\_NONE

访问权限：只读

<a name="remarks"></a>备注
-------

从设备文件的驱动程序的 INF 文件获取的设备类型和子类型。 应用程序读取 WIA\_DIP\_开发人员\_类型属性，以确定它是否正在使用扫描程序、 相机或视频设备。

下表介绍了设备类型的可能值。

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
<td><p>扫描程序设备</p></td>
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

 

有关 INF 文件的详细信息，请参阅[WIA 设备 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff542770)。 **StiDeviceType * * * Xxx*中定义常量*Sti.h*。

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
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

 

 





