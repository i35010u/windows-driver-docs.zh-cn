---
title: DEVPKEY_Device_SafeRemovalRequired
description: DEVPKEY_Device_SafeRemovalRequired
ms.assetid: a162e259-21aa-40d9-a65a-af175a59df6a
keywords:
- DEVPKEY_Device_SafeRemovalRequired 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_SafeRemovalRequired
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ef7906313cc671605a1e20ad970f8c2917643765
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418415"
---
# <a name="devpkey_device_saferemovalrequired"></a>DEVPKEY_Device_SafeRemovalRequired


DEVPKEY_Device_SafeRemovalRequired 设备属性表示一个布尔值，该值指示热插拔设备实例是否需要从计算机中安全地删除。

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
<td align="left"><p>DEVPKEY_Device_SafeRemovalRequired</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
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

如果热插拔设备实例的此属性的值为 DEVPROP_TRUE，则设备实例需要从计算机中安全地删除。 在这种情况下，Windows 会在任务栏右侧的通知区域中显示 "**安全删除硬件**" 图标。 当用户单击此图标时，系统将启动**安全删除硬件**程序。 使用此程序，用户可以指示系统准备要删除的设备实例，然后将其从计算机中删除。

**注意**   如果设备实例是可移动媒体设备（如光驱），则设备实例必须已插入介质，并且 DEVPKEY_Device_SafeRemovalRequired 属性值必须为 DEVPROP_TRUE。 如果两者都为 true，则会在 "**安全删除硬件**" 程序中显示设备实例。

 

如果满足以下条件，Windows 即插即用（PnP）确定热插拔设备实例需要系统中的安全删除：

-   设备实例当前已连接到系统。

-   设备实例已启动或可以被系统自动弹出。

-   未设置设备实例的 CM_DEVCAP_SURPRISEREMOVALOK 设备功能位。 有关设备功能的详细信息，请参阅[**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)。

-   设备实例未将[**DEVPKEY_Device_SafeRemovalRequiredOverride**](devpkey-device-saferemovalrequiredoverride.md)设备属性设置为 DEVPROP_FALSE。

    **注意**   PnP 无条件确定，如果 DEVPKEY_Device_SafeRemovalRequiredOverride 设备属性设置为 DEVPROP_TRUE，热插拔设备需要安全删除。

     

-   设备实例可以直接从其父设备实例中删除，也可以在其设备树中有可移动的祖先。

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_SafeRemovalRequired 的值。

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
<td align="left">Devpkey （包括 Devpkey）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEVPKEY_Device_SafeRemovalRequiredOverride**](devpkey-device-saferemovalrequiredoverride.md)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)

 

 






