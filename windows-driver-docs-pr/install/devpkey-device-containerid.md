---
title: DEVPKEY_Device_ContainerId
description: DEVPKEY_Device_ContainerId
ms.assetid: 9d5be913-b699-4d8f-aa3f-53ad5dbe6482
keywords:
- DEVPKEY_Device_ContainerId 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_ContainerId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c1c8347e5395fa5caa7385dd01364c1ef3c3101a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387084"
---
# <a name="devpkeydevicecontainerid"></a>DEVPKEY_Device_ContainerId


插即用 (PnP) 管理器使用 DEVPKEY_Device_ContainerId 设备属性以一个或多个设备节点进行分组 (*devnodes*) 到*设备容器*表示的物理实例设备。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_ContainerId</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><a href="devprop-type-guid.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_GUID&lt;/strong&gt;](devprop-type-guid.md)"><strong>DEVPROP_TYPE_GUID</strong></a></td>
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

从 Windows 7 开始，即插即用的管理器使用的设备容器和其标识符 (*ContainerID*) 到一个或多个组*devnodes* ，源自和属于特定的每个实例物理设备。 对于设备实例 ContainerID 引用通过 DEVPKEY_Device_ContainerId 设备属性。

当发起到容器的单个设备实例中的所有 devnodes 都分组时，您将完成以下结果：

-   操作系统可以确定功能之间的关联方式*devnodes*来源于物理设备。

-   用户或应用程序会显示而不是传统函数为中心的视图的设备的设备为中心的视图。

DEVPKEY_Device_ContainerId 可以用于确定的设备容器分组*devnodes*在系统中。 对于给定 devnode，可以确定所有 devnodes 属于同一个容器通过完成以下步骤：

-   调用**SetupDiGetDeviceProperty**该 devnode 所属的设备容器的值。

-   枚举在计算机上的所有 devnodes 并查询每个 devnode 获取其 DEVPKEY_Device_ContainerId。 每个 ContainerId 值相匹配的原始 devnode ContainerId 值是容器的相同的一部分。

**请注意**  所有*devnodes*属于容器上给定的总线类型必须共享相同的 ContainerID 值。

 

有关 ContainerIDs 详细信息，请参阅[容器 Id](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)。

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


[容器 Id](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






