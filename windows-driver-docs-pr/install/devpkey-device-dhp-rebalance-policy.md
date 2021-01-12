---
title: DEVPKEY_Device_DHP_Rebalance_Policy
description: DEVPKEY_Device_DHP_Rebalance_Policy
keywords:
- DEVPKEY_Device_DHP_Rebalance_Policy 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DHP_Rebalance_Policy
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ba1b622c23d83785600ee71eead69366ed85e92d
ms.sourcegitcommit: 10fecd036370f5eccb538004c5bec1fdd18c3275
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "98124181"
---
# <a name="devpkey_device_dhp_rebalance_policy"></a>DEVPKEY_Device_DHP_Rebalance_Policy


DEVPKEY_Device_DHP_Rebalance_Policy 设备属性表示一个值，该值指示设备是否将按照 [动态硬件分区（ (DHP) ](../kernel/introduction-to-dynamic-hardware-partitioning.md) 处理器热添加操作）参与资源重新平衡。

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
<td align="left"><p>DEVPKEY_Device_DHP_Rebalance_Policy</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
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

 

<a name="remarks"></a>备注
-------

在运行 Windows Server 2008 或更高版本的 Windows Server 的动态分区服务器上，每当将新处理器动态添加到系统时，操作系统就会启动系统范围的资源重新平衡。 DEVPKEY_Device_DHP_Rebalance_Policy 设备属性决定设备是否参与此类资源重新平衡。 在下列情况下，设备会参与资源重新平衡：

-   DEVPKEY_Device_DHP_Rebalance_Policy 设备属性不存在。

-   设备属性存在，但未设置设备属性的值。

-   设备属性存在，设备属性的值已设置为2。

如果 DEVPKEY_Device_DHP_Rebalance_Policy 设备属性存在并且属性的值设置为1，则在将新处理器动态添加到系统时，设备不会参与资源重新平衡。

设备的 [设备安装程序类](./overview-of-device-setup-classes.md) 是在设备 inf 文件的 " [**Inf 版本" 部分**](./inf-version-section.md) 中指定的。

网络适配器中的设备的默认行为 (类 = Net) 设备安装程序类是将新处理器动态添加到系统时，类的成员不参与资源重新平衡。 所有其他设备安装程序类中的设备的默认行为是在将新处理器动态添加到系统时成员参与资源重新平衡。

此设备属性不影响设备是否会参与出于其他原因而启动的资源重新平衡。

可以通过调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 和 [**SetupDiSetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)访问 DEVPKEY_Device_DHP_Rebalance_Policy 属性。

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


[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

