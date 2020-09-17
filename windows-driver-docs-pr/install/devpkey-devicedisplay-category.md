---
title: DEVPKEY_DeviceDisplay_Category
description: DEVPKEY_DeviceDisplay_Category
ms.assetid: 4f1999cd-e3b7-4755-ab48-1feabbc9d245
keywords:
- DEVPKEY_DeviceDisplay_Category 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceDisplay_Category
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7c9d8ca5e11085911e6a3e5f07df5fc3314fa203
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716388"
---
# <a name="devpkey_devicedisplay_category"></a>DEVPKEY_DeviceDisplay_Category


DEVPKEY_DeviceDisplay_Category 设备属性表示应用于设备实例的一个或多个功能类别。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceDisplay_Category</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

物理设备的设备类别通过[设备元数据包](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)中的[**device.devicecategory**](/previous-versions/windows/hardware/metadata/ff541101(v=vs.85)) XML 元素进行指定。 系统中该设备的每个实例都继承该物理设备的设备类别。

每台物理设备可以在 [设备元数据包](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)中指定一个或多个功能类别。 Windows 设备和打印机使用每个类别将设备实例组合到识别的设备类别之一中。

对于设备支持的每个硬件功能，多功能设备通常会标识多个功能类别。 例如，多功能设备可以标识打印机、传真、扫描仪和可移动存储设备功能的功能类别。

[**DEVPROP_TYPE_STRING_LIST**](devprop-type-string-list.md)中的第一个功能类别字符串指定物理设备的主要功能类别。 主要功能类别由独立硬件供应商 (IHV) 来指定如何播发、打包、销售和最终由用户标识设备。

如果 DEVPKEY_DeviceDisplay_Category 设备属性指定了多个功能类别字符串，则在第一个字符串之后的剩余字符串将指定物理设备的辅助功能类别。

控制面板中的 " **设备和打印机** " 用户界面显示设备实例的主要和次要功能类别。 这些类别按照 DEVPKEY_DeviceDisplay_Category 设备属性中指定的顺序显示。

可以通过调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)访问 DEVPKEY_DeviceDisplay_Category 属性。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey (包含 Devpkey) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**Device.devicecategory**](/previous-versions/windows/hardware/metadata/ff541101(v=vs.85))

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

