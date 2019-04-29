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
ms.openlocfilehash: fd7ffd441ad6460f0ea5992da68c21b6d40696ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380091"
---
# <a name="devpkeydevicesaferemovalrequired"></a>DEVPKEY_Device_SafeRemovalRequired


DEVPKEY_Device_SafeRemovalRequired 设备属性表示一个布尔值，该值指示是否热即插即用设备实例需要从计算机的安全删除。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
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
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果此属性对于热即插即用设备实例的值为 DEVPROP_TRUE，设备实例都必须从计算机的安全删除。 在这种情况下，Windows 将显示**安全删除硬件**任务栏右侧的通知区域中的图标。 当用户单击此图标时，在系统启动**安全删除硬件**程序。 通过使用此程序，用户可以指示系统之前可能会意外删除从计算机删除准备设备实例。

**请注意**  设备实例是否可移动介质设备，如在光盘驱动器上，设备实例必须具有媒体插入，并且必须具有 DEVPROP_TRUE DEVPKEY_Device_SafeRemovalRequired 属性值。 如果两者均为 true，在显示设备实例**安全删除硬件**程序。

 

Windows 插 (PnP) 确定热即插即用设备实例需要从系统的安全删除，是否满足以下条件：

-   设备实例当前连接到系统。

-   设备实例或者启动或可由系统自动弹出。

-   未设置为设备实例 CM_DEVCAP_SURPRISEREMOVALOK 设备功能位。 有关设备功能的详细信息，请参阅[ **SetupDiGetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551967)。

-   设备实例不具有[ **DEVPKEY_Device_SafeRemovalRequiredOverride** ](devpkey-device-saferemovalrequiredoverride.md)设备属性设置为 DEVPROP_FALSE。

    **请注意**  即插即用无条件地确定是否 DEVPKEY_Device_SafeRemovalRequiredOverride 设备属性设置为 DEVPROP_TRUE 热即插即用设备，需要安全删除。

     

-   设备实例是从其父设备实例直接可移动或在其设备树中具有可移动的祖先。

您可以调用[ **SetupDiGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551963)检索 DEVPKEY_Device_SafeRemovalRequired 值。

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


[**DEVPKEY_Device_SafeRemovalRequiredOverride**](devpkey-device-saferemovalrequiredoverride.md)

[**SetupDiGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551963)

[**SetupDiGetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551967)

 

 






