---
title: DEVPKEY_DeviceClass_DHPRebalanceOptOut
description: DEVPKEY_DeviceClass_DHPRebalanceOptOut 设备属性表示一个值，该值指示在发生动态硬件分区 (DHP) 处理器热添加操作后，整个设备类是否参与资源重新平衡。属性 keyDEVPKEY_DeviceClass_DHPRebalanceOptOutProperty 数据类型 identifierDEVPROP_TYPE_BOOLEANProperty accessRead 和应用程序和服务的写访问权限。已本地化的 RemarksOn 动态分区服务器运行 Windows Server 2008 或更高版本的 Windows Server，只要将新处理器动态添加到系统，操作系统就会启动系统范围的资源重新平衡。 在以下情况下，设备类将参与资源重新平衡，DEVPKEY_DeviceClass_DHPRebalanceOptOut 设备属性不存在。设备属性存在，但未设置设备属性的值。设备属性存在并且设备属性的值设置为 FALSE。如果 DEVPKEY_DeviceClass_DHPRebalanceOptOut 设备属性存在并且属性的值设置为 TRUE，则在将新处理器动态添加到系统时，设备类不会参与资源重新平衡。设备的设备安装程序类是在设备 INF 文件的 "INF 版本" 部分中指定的。网络适配器 (类 Net) 的此属性的默认值为 TRUE。 所有其他设备安装程序类的此属性的默认值为 FALSE。此设备属性不影响设备类是否参与出于其他原因而启动的资源重新平衡。可以通过调用 SetupDiGetClassProperty 和 SetupDiSetClassProperty 访问 DEVPKEY_DeviceClass_DHPRebalanceOptOut 属性。
keywords:
- DEVPKEY_DeviceClass_DHPRebalanceOptOut 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_DHPRebalanceOptOut
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 72e6bf5fde019751fcb7928f7a34f95ca4c00fd8
ms.sourcegitcommit: 10fecd036370f5eccb538004c5bec1fdd18c3275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98124299"
---
# <a name="devpkey_deviceclass_dhprebalanceoptout"></a>DEVPKEY_DeviceClass_DHPRebalanceOptOut


DEVPKEY_DeviceClass_DHPRebalanceOptOut 设备属性表示一个值，该值指示在发生 [动态硬件分区 (DHP) ](../kernel/introduction-to-dynamic-hardware-partitioning.md) 处理器热添加操作后，整个设备类是否参与资源重新平衡。

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
<td align="left"><p>DEVPKEY_DeviceClass_DHPRebalanceOptOut</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>按应用程序和服务进行读取和写入访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

**备注**

在运行 Windows Server 2008 或更高版本的 Windows Server 的动态分区服务器上，每当将新处理器动态添加到系统时，操作系统就会启动系统范围的资源重新平衡。 在以下情况下，设备类将参与资源重新平衡：

-   DEVPKEY_DeviceClass_DHPRebalanceOptOut 设备属性不存在。

-   设备属性存在，但未设置设备属性的值。

-   设备属性存在并且设备属性的值设置为 **FALSE**。

如果 DEVPKEY_DeviceClass_DHPRebalanceOptOut 设备属性存在并且属性的值设置为 **TRUE**，则在将新处理器动态添加到系统时，设备类不会参与资源重新平衡。

设备的 [设备安装程序类](./overview-of-device-setup-classes.md) 是在设备 inf 文件的 " [**Inf 版本" 部分**](./inf-version-section.md) 中指定的。

网络适配器的此属性的默认值 (类 = Net) 为 **TRUE**。 所有其他设备安装程序类的此属性的默认值为 **FALSE**。

此设备属性不影响设备类是否参与出于其他原因而启动的资源重新平衡。

可以通过调用 [**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw) 和 [**SetupDiSetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetclasspropertyw)访问 DEVPKEY_DeviceClass_DHPRebalanceOptOut 属性。

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
<td align="left"><p>Windows Server 2008 和更高版本的 Windows Server 中提供。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey (包含 Devpkey) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiSetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetclasspropertyw)

