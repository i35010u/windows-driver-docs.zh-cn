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
ms.openlocfilehash: d77e358b158540f392fdf811dc9ac7471ccf8954
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378041"
---
# <a name="devpkeydevicedisplaycategory"></a>DEVPKEY_DeviceDisplay_Category


DEVPKEY_DeviceDisplay_Category 设备属性表示应用于设备实例的一个或多个功能类别。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
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
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

通过指定物理设备的设备类别[ **DeviceCategory** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541101(v=vs.85))中的 XML 元素[设备元数据包](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)。 该设备在系统中的每个实例将继承该物理设备的设备类别。

每个物理设备可以具有一个或多功能类别中指定[设备元数据包](https://docs.microsoft.com/windows-hardware/drivers/install/device-metadata-packages)。 每个类别的 Windows 设备和打印机用于分组到一个已识别的设备类别的设备实例。

多功能设备通常会识别为每个设备支持的硬件功能的多个功能类别。 例如，多功能设备无法识别打印机、 传真、 扫描程序和可移动存储设备功能的功能的类别。

第一个功能类别中的字符串[ **DEVPROP_TYPE_STRING_LIST** ](devprop-type-string-list.md)指定物理设备的主要功能类别。 主要功能类别是由独立硬件供应商 (IHV) 来指定播发设备是如何定义、 打包、 销售的和最终用户标识。

如果 DEVPKEY_DeviceDisplay_Category 设备属性指定多个功能类别字符串，请按照第一个字符串的剩余字符串指定物理设备的辅助功能类别。

**设备和打印机**控制面板中的用户界面中显示主要和辅助功能类别的设备实例。 这些类别 DEVPKEY_DeviceDisplay_Category 设备属性中指定的顺序显示。

可以通过调用访问 DEVPKEY_DeviceDisplay_Category 属性[ **SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DeviceCategory**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541101(v=vs.85))

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






