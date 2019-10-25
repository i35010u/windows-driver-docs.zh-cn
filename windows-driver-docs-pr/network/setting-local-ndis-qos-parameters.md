---
title: 设置本地 NDIS QoS 参数
description: 设置本地 NDIS QoS 参数
ms.assetid: 7AB30829-16A0-46BF-8066-506E01E718A4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b296c8de9238fc3cfe44256176306beefff090d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841941"
---
# <a name="setting-local-ndis-qos-parameters"></a>设置本地 NDIS QoS 参数


本地 NDIS 服务质量（QoS）参数指定用于微型端口驱动程序及其网络适配器的本地预配 QoS 设置。 微型端口驱动程序通过以下方式获取本地 NDIS QoS 参数：

-   通过\_QOS 的对象标识符（OID）方法请求，由数据中心桥接（DCB）组件（Msdcb）发出的[QOS\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)。 此 OID 请求包含一个[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构，用于指定本地 NDIS QOS 参数。

    有关 DCB 组件的详细信息，请参阅[用于数据中心桥接的 NDIS QoS 体系结构](ndis-qos-architecture-for-data-center-bridging.md)。

    **注意**  从 Windows Server 2012 开始，DCB 组件是通过 Microsoft 数据中心桥接（DCB）服务器功能安装和启用的。 默认情况下不安装此功能。

     

-   通过网络适配器的独立硬件供应商（IHV）存储在系统注册表中并由其定义的专有设置。 当[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数由 NDIS 调用时，微型端口驱动程序将读取这些设置。

-   通过由 IHV 开发的管理应用程序，将专用设置颁发给微型端口驱动程序。

当 DCB 组件[\_参数\_qos](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)方法发出 oid 方法请求时， **ndis\_qos\_参数\_愿意**标记**ndis\_QOS\_参数。Flags**成员指定微型端口驱动程序如何从本地 NDIS QoS 参数解析其操作 QoS 参数。 根据此标志，驱动程序将通过以下方式解析本地 QoS 参数：

-   如果设置了**NDIS\_QOS\_参数\_愿意**标志，则微型端口驱动程序必须启用本地 DCB 交换（DCBX）的状态。 这允许对驱动程序进行远程配置，使其具有 QoS 参数。 在这种情况下，驱动程序将根据远程 QoS 参数解析其操作 QoS 参数。

    微型端口驱动程序还可以根据 IHV 定义的任何专有 QoS 设置来解析其操作 QoS 参数。 对于不是由对等方进行远程配置或由操作系统本地配置的 QoS 参数，驱动程序只能执行此操作。

    有关此过程的详细信息，请参阅[接收远程 NDIS QoS 参数](receiving-remote-ndis-qos-parameters.md)。

-   \_如果未设置 DCBX **\_参数\_愿意**标志，则微型端口驱动程序必须禁用本地。 这允许驱动程序从其本地 QoS 参数而不是远程 QoS 参数解析其操作 QoS 参数。

    **请注意**  如果已禁用本地 DCBX，则微型端口驱动程序仍然可以接受远程 qos 参数，但不能使用它们来解析其操作 QoS 参数。

     

如果已禁用本地 DCBX，则微型端口驱动程序在管理其本地 QoS 参数时必须遵循以下指导原则：

-   微型端口驱动程序必须禁用或重写其相关**NDIS\_qos\_参数\_*XXX*\_配置**\_标志的任何本地 QoS 参数 **。Flags**成员。

    例如，微型端口驱动程序可以用其专用设置替代由 IHV 定义的 QoS 参数。 如果没有使用**NDIS\_qos\_参数\_*XXX*\_配置**的标志指定的本地 QoS 参数没有专用设置，则驱动程序必须在网络上禁用这些 qos 参数的使用适配器.

    **请注意**  ndis 保证 **\_参数\_ETS\_配置了 ndis\_qos 参数**，而**ndis\_qos\_参数\_** 已设置或清除\_配置的标志到.

     

-   小型端口驱动程序应在解决其操作 NDIS QoS 参数时，*应用* [**NDIS\_qos\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构中包含的本地 QoS 参数。 如果驱动程序应用这些本地 QoS 参数，则它不能使用从远程对等端收到的任何远程 QoS 参数。

    有关此过程的详细信息，请参阅[解决操作 NDIS QoS 参数](resolving-operational-ndis-qos-parameters.md)。

有关本地 DCBX 适用状态的详细信息，请参阅[管理本地 DCBX 适用的状态](managing-the-local-dcbx-willing-state.md)。

 

 





