---
title: DEVPKEY_Device_BaseContainerId
description: DEVPKEY_Device_BaseContainerId
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
ms.openlocfilehash: df9907b66e187b2c694e68707bec26fa49cdacf3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782825"
---
# <a name="devpkey_device_basecontainerid"></a>DEVPKEY_Device_BaseContainerId


DEVPKEY_Device_BaseContainerId 设备属性表示) 的基本容器标识符 (*ID* 的 *GUID* 值。Windows 即插即用 (PnP) manager 将此值分配给设备节点 (*devnode*) 。

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
<td align="left"><p>DEVPKEY_Device_BaseContainerId</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><a href="devprop-type-guid.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_GUID&lt;/strong&gt;](devprop-type-guid.md)"><strong>DEVPROP_TYPE_GUID</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_BASE_CONTAINERID</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

PnP 管理器使用以下方法之一确定 devnode 的容器 ID：

-   总线驱动程序提供容器 ID。

    当 PnP 管理器将容器 ID 分配给 devnode 时，它会首先检查 devnode 的总线驱动程序是否可以提供容器 ID。 总线驱动程序通过 [**IRP_MN_QUERY_ID**](../kernel/irp-mn-query-id.md) 查询请求提供容器 ID，并将 **IdType** 字段设置为 **BusQueryContainerID**。

-   PnP 管理器使用可移动设备功能生成容器 ID。

    如果总线驱动程序无法为其枚举的 devnode 提供容器 ID，则 PnP 管理器使用可移动设备功能为该设备枚举的所有 devnodes 生成容器 ID。 总线驱动程序报告此设备的功能，以响应 [**IRP_MN_QUERY_CAPABILITIES**](../kernel/irp-mn-query-capabilities.md) 的请求。

-   PnP 管理器使用可移动设备功能的替代生成容器 ID。

    尽管替代机制不会更改可移动设备功能的值，但它会强制 PnP 管理器使用替代设置，而不是在为设备生成容器 Id 时使用可移动设备功能的值。

有关这些方法的详细信息，请参阅 [如何生成容器 id](./how-container-ids-are-generated.md)。

不管如何获取容器 ID 值，PnP 管理器都将值分配给 devnode 的 DEVPKEY_Device_BaseContainerId 属性。

DEVPKEY_Device_BaseContainerId 属性可用于强制将新的 devnode 与系统中存在的其他 devnodes 进行分组。 这使你可以将新的 devnode 用作其他相关 devnodes 的父 (或 *基*) 容器 ID。 为此，必须首先获取现有 devnode 的 DEVPKEY_Device_BaseContainerID GUID。 然后，必须返回新 devnode 的容器 ID GUID，以响应 [**IRP_MN_QUERY_ID**](../kernel/irp-mn-query-id.md) 查询请求，该请求将 **QueryId** 字段设置为 **BusQueryContainerID**。

**注意**   DEVPKEY_Device_BaseContainerId 或 [**DEVPKEY_Device_ContainerId**](devpkey-device-containerid.md) 属性的查询所返回的值可能不同于同一 devnode 的值。

 

**注意**  不要使用 DEVPKEY_Device_BaseContainerId 属性在系统中重新构建设备容器分组。 请改用 [**DEVPKEY_Device_ContainerId**](devpkey-device-containerid.md) 属性。

 

有关容器 Id 的详细信息，请参阅 [容器 id](./container-ids.md)。

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
<td align="left">Devpkey (包含 Devpkey) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[容器 ID](./container-ids.md)

[**DEVPKEY_Device_ContainerId**](devpkey-device-containerid.md)

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

