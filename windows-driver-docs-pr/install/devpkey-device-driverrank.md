---
title: DEVPKEY_Device_DriverRank
description: DEVPKEY_Device_DriverRank
keywords:
- DEVPKEY_Device_DriverRank 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverRank
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d4f91f15bd6f73491ccf3cb0c9edbb56ff19d862
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798145"
---
# <a name="devpkey_device_driverrank"></a>DEVPKEY_Device_DriverRank


DEVPKEY_Device_DriverRank 设备属性表示为设备实例安装的驱动程序的级别。

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
<td align="left"><p>DEVPKEY_Device_DriverRank</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-uint32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_UINT32&lt;/strong&gt;](devprop-type-uint32.md)"><strong>DEVPROP_TYPE_UINT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 设置 DEVPKEY_Device_DriverRank 的值。

可以调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_Device_DriverRank 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_DriverRank 属性键。 有关如何在这些早期版本的 Windows 上访问此属性的信息，请参阅 [访问设备驱动程序属性](./accessing-device-driver-properties.md)。

有关驱动程序级别的信息，请参阅 [Windows 如何对驱动程序进行排名](./how-setup-ranks-drivers--windows-vista-and-later-.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiGetDriverInstallParams**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdriverinstallparamsa)

[**SP_DRVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_drvinstall_params)

