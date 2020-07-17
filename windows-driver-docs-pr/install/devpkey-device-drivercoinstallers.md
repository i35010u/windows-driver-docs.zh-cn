---
title: DEVPKEY_Device_DriverCoInstallers
description: DEVPKEY_Device_DriverCoInstallers
ms.assetid: ba85a906-adfa-42f9-b52a-e8a48c8d5076
keywords:
- DEVPKEY_Device_DriverCoInstallers 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverCoInstallers
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8a30c338fde2e29bd69dc30d3069d8a1221b53c2
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418493"
---
# <a name="devpkey_device_drivercoinstallers"></a>DEVPKEY_Device_DriverCoInstallers


DEVPKEY_Device_DriverCoInstallers 设备属性表示作为设备实例的*共同安装*程序注册的 dll 名称和 dll 中入口点的列表。

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
<td align="left"><p>DEVPKEY_Device_DriverCoInstallers</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string-list.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING_LIST&lt;/strong&gt;](devprop-type-string-list.md)"><strong>DEVPROP_TYPE_STRING_LIST</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据格式</strong></p></td>
<td align="left"><p>"AbcCoInstall.dll、AbcCoInstallEntryPoint\0...AbcCoInstall.dll、AbcCoInstallEntryPoin\0\0"</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>对应的注册表值标识符和注册表值名称</strong></p></td>
<td align="left"><p>REGSTR_VAL_COINSTALLERS_32</p>
<p><strong>CoInstallers32</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_DriverCoInstallers 的值由[**INF *DDInstall*提供。**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-coinstallers-section)安装设备的 INF 文件中的 Coinstallers 部分。

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_DriverCoInstallers 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_DriverCoInstallers 属性键。 在这些早期版本的 Windows 上，可以通过访问设备实例的软件密钥下的相应**CoInstallers32**注册表值来访问此属性的值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅[访问设备驱动程序属性](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-driver-properties)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**INF *DDInstall*。Coinstallers 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-coinstallers-section)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






