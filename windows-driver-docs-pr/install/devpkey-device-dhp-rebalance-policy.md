---
title: DEVPKEY_Device_DHP_Rebalance_Policy
description: DEVPKEY_Device_DHP_Rebalance_Policy
ms.assetid: a882a114-9d1b-41ca-ab24-c2cdda952177
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
ms.openlocfilehash: d71e712213acfed590eb998bfe758dddabe5323c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387080"
---
# <a name="devpkeydevicedhprebalancepolicy"></a>DEVPKEY_Device_DHP_Rebalance_Policy


DEVPKEY_Device_DHP_Rebalance_Policy 设备属性表示一个值，指示设备是否将参与资源重新平衡以下[动态硬件分区 (DHP)](https://docs.microsoft.com/windows-hardware/drivers/kernel/dynamic-hardware-partitioning-techniques)处理器热添加操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
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
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>读取和写入应用程序和服务的访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

正在运行 Windows Server 2008 或更高版本的 Windows Server，则操作系统将启动系统范围资源的动态可分区服务器上重新平衡新处理器动态添加到系统时。 DEVPKEY_Device_DHP_Rebalance_Policy 设备属性确定设备是否参与此类资源重新平衡。 该设备出现在中，在下列情况下重新平衡资源：

-   DEVPKEY_Device_DHP_Rebalance_Policy 设备属性不存在。

-   设备属性存在并且未设置设备属性的值。

-   设备属性存在且设备属性的值设置为 2。

如果存在 DEVPKEY_Device_DHP_Rebalance_Policy 设备属性和属性的值设置为 1，设备将不参与重新平衡新处理器动态添加到系统时的资源。

设备的[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)中指定[ **INF 版本部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)的设备的 INF 文件。

网络适配器中的设备的默认行为 (类 = Net) 设备安装程序类是类的成员不会参与资源重新平衡新处理器动态添加到系统时。 所有其他设备安装程序类中的设备的默认行为是成员参与资源重新平衡新处理器动态添加到系统时。

此设备属性不会影响是否由于其他原因而启动资源重新平衡将加入设备。

可以通过调用访问 DEVPKEY_Device_DHP_Rebalance_Policy 属性[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)并[ **SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw).

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
<td align="left"><p>在 Windows Server 2008 和更高版本的 Windows Server 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

 






