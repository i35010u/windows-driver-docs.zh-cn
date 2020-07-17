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
ms.openlocfilehash: c288741b17c1bf085859c6e770d566f9d24e1eb0
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418277"
---
# <a name="devpkey_device_basecontainerid"></a>DEVPKEY_Device_BaseContainerId


DEVPKEY_Device_BaseContainerId 设备属性表示基容器标识符（*ID*）的*GUID*值。Windows 即插即用（PnP）管理器将此值分配给设备节点（*devnode*）。

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

    当 PnP 管理器将容器 ID 分配给 devnode 时，它会首先检查 devnode 的总线驱动程序是否可以提供容器 ID。 总线驱动程序通过[**IRP_MN_QUERY_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)查询请求提供容器 ID，并将**IdType**字段设置为**BusQueryContainerID**。

-   PnP 管理器使用可移动设备功能生成容器 ID。

    如果总线驱动程序无法为其枚举的 devnode 提供容器 ID，则 PnP 管理器使用可移动设备功能为该设备枚举的所有 devnodes 生成容器 ID。 总线驱动程序报告此设备的功能，以响应[**IRP_MN_QUERY_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)的请求。

-   PnP 管理器使用可移动设备功能的替代生成容器 ID。

    尽管替代机制不会更改可移动设备功能的值，但它会强制 PnP 管理器使用替代设置，而不是在为设备生成容器 Id 时使用可移动设备功能的值。

有关这些方法的详细信息，请参阅[如何生成容器 id](https://docs.microsoft.com/windows-hardware/drivers/install/how-container-ids-are-generated)。

不管如何获取容器 ID 值，PnP 管理器都将值分配给 devnode 的 DEVPKEY_Device_BaseContainerId 属性。

DEVPKEY_Device_BaseContainerId 属性可用于强制将新的 devnode 与系统中存在的其他 devnodes 进行分组。 这使你可以将新的 devnode 用作其他相关 devnodes 的父（或*基*）容器 ID。 为此，必须首先获取现有 devnode 的 DEVPKEY_Device_BaseContainerID GUID。 然后，必须返回新 devnode 的容器 ID GUID，以响应[**IRP_MN_QUERY_ID**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-id)查询请求，该请求将**QueryId**字段设置为**BusQueryContainerID**。

**注意**   DEVPKEY_Device_BaseContainerId 或[**DEVPKEY_Device_ContainerId**](devpkey-device-containerid.md)属性的查询所返回的值可能不同于同一 devnode 的值。

 

**注意**   不要使用 DEVPKEY_Device_BaseContainerId 属性在系统中重新构建设备容器分组。 请改用[**DEVPKEY_Device_ContainerId**](devpkey-device-containerid.md)属性。

 

有关容器 Id 的详细信息，请参阅[容器 id](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)。

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


[容器 Id](https://docs.microsoft.com/windows-hardware/drivers/install/container-ids)

[**DEVPKEY_Device_ContainerId**](devpkey-device-containerid.md)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






