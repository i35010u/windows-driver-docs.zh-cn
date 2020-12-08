---
title: DEVPKEY_Device_DriverDate
description: DEVPKEY_Device_DriverDate
keywords:
- DEVPKEY_Device_DriverDate 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverDate
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: eafe7259b2828b648ff3fe47249fff66d013291d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838029"
---
# <a name="devpkey_device_driverdate"></a>DEVPKEY_Device_DriverDate


PKEY_Device_DriverDate 设备属性表示当前为设备实例安装的驱动程序的日期。

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
<td align="left"><p>DEVPKEY_Device_DriverDate</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-filetime.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_FILETIME&lt;/strong&gt;](devprop-type-filetime.md)"><strong>DEVPROP_TYPE_FILETIME</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应的注册表值标识符和注册表值名称</strong></p></td>
<td align="left"><p>REGSTR_VAL_DRIVERDATEDATA</p>
<p><strong>DriverDateData</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_DriverDate 的值是由 inf [**DriverVer 指令**](./inf-driverver-directive.md)提供的，inf 版本部分包括在安装设备的 inf **版本部分** 中，也包括在安装设备的 [**inf *DDINSTALL* 部分**](./inf-ddinstall-section.md)中的设备特定 inf **DriverVer** 指令中。

可以调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_Device_DriverDate 属性的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_DriverDate 属性键。 在这些早期版本的 Windows 上，可以通过访问设备实例的软件密钥下的相应 **DriverDateData** 注册表值来访问此属性的值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅 [访问设备驱动程序属性](./accessing-device-driver-properties.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**INF *DDInstall* 部分**](./inf-ddinstall-section.md)

[**INF DriverVer 指令**](./inf-driverver-directive.md)

**INF 版本部分** 
[ **SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

