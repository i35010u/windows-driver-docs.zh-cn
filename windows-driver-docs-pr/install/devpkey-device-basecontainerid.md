---
title: DEVPKEY_Device_BaseContainerId
description: DEVPKEY_Device_BaseContainerId
ms.assetid: ccc20b78-60a3-4351-9809-e2a285ad0a19
keywords:
- DEVPKEY_Device_BaseContainerId 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_BaseContainerId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6fd92b523af1bffd23524dbde1840f36d4dbd4c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387110"
---
# <a name="devpkeydevicebasecontainerid"></a>DEVPKEY_Device_BaseContainerId


DEVPKEY_Device_BaseContainerId 设备属性表示*GUID*基容器标识符的值 (*ID*)。Windows 即插即用和 Play (PnP) 管理器将此值分配给设备节点 (*devnode*)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_BaseContainerId</p></td>
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
<td align="left"><p><strong>相应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_BASE_CONTAINERID</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

PnP 管理器通过使用以下方法之一来确定 devnode 的容器 ID:

-   总线驱动程序提供容器 id。

    当 PnP 管理器将容器 ID 分配给 devnode 时，它首先检查是否 devnode 的总线驱动程序可以提供一个容器 id。 总线驱动程序提供容器 ID 通过[ **IRP_MN_QUERY_ID** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)使用的查询请求**Parameters.QueryId.IdType**字段设置为**BusQueryContainerID**。

-   PnP 管理器通过使用可移动设备功能生成的容器 ID。

    如果总线驱动程序不能为它枚举 devnode 提供容器的 ID，即插即用管理器使用可移动设备功能生成枚举设备的所有 devnodes 的容器 ID。 总线驱动程序报告此设备功能，以响应[ **IRP_MN_QUERY_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)请求。

-   PnP 管理器通过使用可移动设备功能的重写生成的容器 ID。

    尽管替代机制不会更改可移动设备功能的值，它会强制 PnP 管理器中，若要生成设备的容器 Id 时使用替代设置而不是可移动设备功能的值。

有关这些方法的详细信息，请参阅[生成如何容器 Id](https://docs.microsoft.com/windows-hardware/drivers/install/how-container-ids-are-generated)。

而不考虑如何获取容器的 ID 值，即插即用管理器将值分配给 devnode DEVPKEY_Device_BaseContainerId 属性。

DEVPKEY_Device_BaseContainerId 属性可用于强制与系统中存在其他 devnodes 新 devnode 的分组。 这使您可以使用新 devnode 作为父 (或*基*) 适用于其他容器 ID 相关 devnodes。 若要执行此操作，你必须首先获取现有 devnode DEVPKEY_Device_BaseContainerID GUID。 然后，必须在响应中返回容器的新 devnode ID GUID 到[ **IRP_MN_QUERY_ID** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)查询请求具有**Parameters.QueryId.IdType**字段设置为**BusQueryContainerID**。

**请注意**   DEVPKEY_Device_BaseContainerId 的查询返回的值或[ **DEVPKEY_Device_ContainerId** ](devpkey-device-containerid.md)属性可以是不同的相同 devnode.

 

**请注意**  不使用 DEVPKEY_Device_BaseContainerId 属性来重新构建系统中的设备容器分组。 使用[ **DEVPKEY_Device_ContainerId** ](devpkey-device-containerid.md)属性改为。

 

有关容器 Id 的详细信息，请参阅[容器 Id](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)。

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

[**DEVPKEY_Device_ContainerId**](devpkey-device-containerid.md)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






