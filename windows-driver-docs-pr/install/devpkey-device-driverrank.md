---
title: DEVPKEY_Device_DriverRank
description: DEVPKEY_Device_DriverRank
ms.assetid: 9a6a8e9f-fd3c-4a64-b0d2-565cda0dae52
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
ms.openlocfilehash: 1edf9eb8a4ad38f1b1a981cf5ef0a2b71599397f
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418572"
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
<th>属性</th>
<th>Value</th>
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

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_DriverRank 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_DriverRank 属性键。 有关如何在这些早期版本的 Windows 上访问此属性的信息，请参阅[访问设备驱动程序属性](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-driver-properties)。

有关驱动程序级别的信息，请参阅[Windows 如何对驱动程序进行排名](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-ranks-drivers)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiGetDriverInstallParams**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdriverinstallparamsa)

[**SP_DRVINSTALL_PARAMS**](https://docs.microsoft.com/windows/desktop/api/setupapi/ns-setupapi-_sp_drvinstall_params)

 

 






