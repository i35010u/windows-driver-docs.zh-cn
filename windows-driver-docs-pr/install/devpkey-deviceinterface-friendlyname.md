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
ms.openlocfilehash: 2fb919987a7cd014229d7438c77e2bc58af63dcc
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096637"
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
<th>Attribute</th>
<th>值</th>
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
<td align="left"><p><strong>FriendlyName</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

设备接口类的**FriendlyName**注册表值由 inf DDInstall 中包含的[**inf AddInterface 指令**](./inf-addinterface-directive.md)设置[**。 *DDInstall***](./inf-ddinstall-interfaces-section.md)INF 文件中安装设备接口的接口部分。

Windows 将接口的 [**DEVPKEY_NAME**](devpkey-name--device-interface-.md) 设备属性的值设置为 DEVPKEY_DeviceInterface_FriendlyName 的值。 若要在用户界面项中标识设备接口，请使用设备接口的 DEVPKEY_NAME 的值，而不是 DEVPKEY_DeviceInterface_FriendlyName 的值。

可以通过调用 [**SetupDiGetDeviceInterfaceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw) 来检索 DEVPKEY_DeviceInterface_FriendlyName 的值，并通过调用 [**SetupDiSetDeviceInterfaceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)进行设置。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_DeviceInterface_FriendlyName 属性键。 通过访问设备接口的相应 **FriendlyName** 注册表项值，可以访问此属性的值。 有关如何访问设备接口的注册表项值的信息，请参阅 [访问设备接口属性](./accessing-device-interface-properties.md)。

有关设备接口的信息，请参阅 [设备接口类](./overview-of-device-interface-classes.md) 和 [**INF AddInterface 指令**](./inf-addinterface-directive.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>另请参阅


[**DEVPKEY_NAME（设备接口）**](devpkey-name--device-interface-.md)

[**INF AddInterface 指令**](./inf-addinterface-directive.md)

[**INF *DDInstall*。接口部分**](./inf-ddinstall-interfaces-section.md)

[**SetupDiGetDeviceInterfaceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

[**SetupDiOpenDeviceInterfaceRegKey**](/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey)

[**SetupDiSetDeviceInterfaceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)

 

