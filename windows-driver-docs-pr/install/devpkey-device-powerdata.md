---
title: DEVPKEY_Device_PowerData
description: DEVPKEY_Device_PowerData
ms.assetid: a5ebb465-674c-483a-ae2c-c46c30a67662
keywords:
- DEVPKEY_Device_PowerData 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_PowerData
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b19cc8cc4143dbb1087d326483e271e2b52328b4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840645"
---
# <a name="devpkey_device_powerdata"></a>DEVPKEY_Device_PowerData


DEVPKEY_Device_PowerData 设备属性表示有关设备实例的电源信息。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_PowerData</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-binary.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BINARY&lt;/strong&gt;](devprop-type-binary.md)"><strong>DEVPROP_TYPE_BINARY</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应的 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_DEVICE_POWER_DATA</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 设置 DEVPKEY_Device_PowerData 的值。 DEVPKEY_Device_PowerData 的值包含[**CM_POWER_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-cm_power_data_s)结构。

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_PowerData 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_PowerData 属性键。 相反，你可以使用相应的 SPDRP_DEVICE_POWER_DATA 标识符来访问这些早期版本的 Windows 上的属性值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅[访问 Device Instance SPDRP_Xxx Properties](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)。

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
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey （包括 Devpkey）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**CM_POWER_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-cm_power_data_s)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






