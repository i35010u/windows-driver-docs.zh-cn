---
title: NDIS 支持的 WMI 操作
description: NDIS 支持的 WMI 操作
ms.assetid: 78dfe8a6-25aa-40d4-bc32-19bd1d4a41b1
keywords:
- Windows Management Instrumentation WDK 网络、 NDIS 操作
- WMI WDK 网络、 NDIS 操作
- 虚拟连接 WDK NDIS WMI
- VCs WDK NDIS WMI
- 微型端口适配器 WDK 连接网络、 枚举
- 适配器 WDK 连接网络、 枚举
- QU
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eedbbd90727ca5cba19f1675fe5fa2c5bf32fc1e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384384"
---
# <a name="ndis-supported-wmi-operations"></a>NDIS 支持的 WMI 操作





NDIS 支持 WMI 执行以下操作：

-   枚举适配器以及枚举 (VC) 的虚拟连接。

    NDIS 注册全局 Guid ( [GUID\_NDIS\_ENUMERATE\_适配器\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/guid-ndis-enumerate-adapters-ex)和 GUID\_NDIS\_ENUMERATE\_VC) 与 WMI 的启用 WMI 客户端来枚举所有微型端口适配器 （即，微型端口驱动程序实例） 和所有名为 VCs。 因为 NDIS 跟踪所有已加载的微型端口驱动程序和所有命名 VCs，NDIS 不会查询此类信息的微型端口驱动程序。

-   查询单个实例和设置的单个实例

    通过 NDIS，WMI 客户端可以查询或设置一个数据块，这对应于单个 OID 的单个实例。 对于查询，NDIS 返回所有与适配器或 VC 相关联的信息。 WMI 客户端不能查询或设置位于 OID 的数据项。 例如，GUID 的查询\_NDIS\_代\_共同\_链接\_速度 GUID 返回出站和入站速度。 WMI 客户端无法查询仅出站速度或仅入站的速度。

-   查询所有数据

    NDIS 通过获取适当的数据并与 WMI 返回的所有实例的 guid 的组合的数据满足特定 GUID 在查询所有数据请求。 例如，在响应上的查询的所有数据请求[GUID\_NDIS\_ENUMERATE\_适配器\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/guid-ndis-enumerate-adapters-ex)，NDIS 到 WMI 返回所有已加载的微型端口驱动程序的列表。 查询所有上的数据映射到 OID 的 GUID\_GEN\_共同\_XMIT\_PDU\_NDIS 好了，在每个面向连接的微型端口驱动程序的每个 VC 查询该 OID 并组合的数据返回到 WMI。 由于查询所有数据请求的开销可能非常高，WMI 客户端应使用查询所有数据请求仅枚举适配器和 VCs。 确定适配器或 VC 感兴趣之后, 在客户端然后可以查询各个实例的 GUID。

-   事件通知

    WMI 客户端可以使用 NDIS 以获取特定状态指示通知注册。 此类的状态指示时，NDIS 将具有相应的 GUID 的状态信息到 WMI 传递的 WMI 事件的形式传送到客户端。

-   执行方法

    通过 NDIS，WMI 客户端可以运行与数据块，它对应于单个 OID 相关联的方法。 WMI 客户端提供 NDIS 运行该方法所需的信息。 方法请求可以与微型端口适配器、 NDIS 端口或 VCs 相关联。 NDIS 后成功运行该方法返回生成的信息。

 

 





