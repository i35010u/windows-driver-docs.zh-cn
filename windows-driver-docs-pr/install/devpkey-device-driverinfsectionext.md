---
title: DEVPKEY_Device_DriverInfSectionExt
description: DEVPKEY_Device_DriverInfSectionExt
ms.assetid: bf6260b4-5df3-4f85-8319-0f864c017e3d
keywords:
- DEVPKEY_Device_DriverInfSectionExt 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverInfSectionExt
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6fa3a15d00a64f98bcbbc13d18dfc836545ebd77
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418271"
---
# <a name="devpkey_device_driverinfsectionext"></a>DEVPKEY_Device_DriverInfSectionExt


DEVPKEY_Device_DriverInfSectionExt 设备驱动程序属性表示安装设备实例的驱动程序的[**INF DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)的平台扩展。

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
<td align="left"><p>DEVPKEY_Device_DriverInfSectionExt</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应的注册表值标识符和注册表值名称</strong></p></td>
<td align="left"><p>REGSTR_VAL_INFSECTIONEXT</p>
<p><strong>InfSectionExt</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 设置 DEVPKEY_Device_DriverInfSectionExt 的值。

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_DriverInfSectionExt 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_DriverInfSectionExt 属性键。 在这些早期版本的 Windows 上，可以通过访问设备实例的软件密钥下的相应**InfSectionExt**注册表值来访问此属性的值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅[访问设备驱动程序属性](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-driver-properties)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**INF DDInstall 节**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






