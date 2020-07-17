---
title: DEVPKEY_DeviceInterface_FriendlyName
description: DEVPKEY_DeviceInterface_FriendlyName
ms.assetid: 398618a2-621b-477f-b90b-127e8df24b3d
keywords:
- DEVPKEY_DeviceInterface_FriendlyName 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceInterface_FriendlyName
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 67bb065765dac77d90e4ac682602f99f42ff4a20
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418220"
---
# <a name="devpkey_deviceinterface_friendlyname"></a>DEVPKEY_DeviceInterface_FriendlyName


DEVPKEY_DeviceInterface_FriendlyName 设备属性表示设备接口的友好名称。

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
<td align="left"><p>DEVPKEY_DeviceInterface_FriendlyName</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的读取和写入访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应的注册表值名称</strong></p></td>
<td align="left"><p><strong>友好</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

设备接口类的**FriendlyName**注册表值由 inf DDInstall 中包含的[**inf AddInterface 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)设置[**。 *DDInstall***](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-interfaces-section)INF 文件中安装设备接口的接口部分。

Windows 将接口的[**DEVPKEY_NAME**](devpkey-name--device-interface-.md)设备属性的值设置为 DEVPKEY_DeviceInterface_FriendlyName 的值。 若要在用户界面项中标识设备接口，请使用设备接口的 DEVPKEY_NAME 的值，而不是 DEVPKEY_DeviceInterface_FriendlyName 的值。

可以通过调用[**SetupDiGetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)来检索 DEVPKEY_DeviceInterface_FriendlyName 的值，并通过调用[**SetupDiSetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)进行设置。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_DeviceInterface_FriendlyName 属性键。 通过访问设备接口的相应**FriendlyName**注册表项值，可以访问此属性的值。 有关如何访问设备接口的注册表项值的信息，请参阅[访问设备接口属性](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-interface-properties)。

有关设备接口的信息，请参阅[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)和[**INF AddInterface 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**DEVPKEY_NAME（设备接口）**](devpkey-name--device-interface-.md)

[**INF AddInterface 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive)

[**INF *DDInstall*。接口部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-interfaces-section)

[**SetupDiGetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

[**SetupDiOpenDeviceInterfaceRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey)

[**SetupDiSetDeviceInterfaceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)

 

 






