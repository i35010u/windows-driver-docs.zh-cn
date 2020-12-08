---
title: 设置本地 NDIS QoS 参数
description: 设置本地 NDIS QoS 参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91b4fe3760d9b07c5edbff72ae002107a8188b6a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838725"
---
# <a name="setting-local-ndis-qos-parameters"></a>设置本地 NDIS QoS 参数


本地 NDIS 服务质量 (QoS) 参数指定用于微型端口驱动程序及其网络适配器的本地预配 QoS 设置。 微型端口驱动程序通过以下方式获取本地 NDIS QoS 参数：

-   通过对象标识符 (OID) 方法请求由数据中心桥接 (DCB) 组件颁发的 [oid \_ QOS \_ 参数](./oid-qos-parameters.md) ( # A0) 。 此 OID 请求包含用于指定本地 NDIS QoS 参数的 [**NDIS \_ qos \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构。

    有关 DCB 组件的详细信息，请参阅 [用于数据中心桥接的 NDIS QoS 体系结构](ndis-qos-architecture-for-data-center-bridging.md)。

    **注意**  从 Windows Server 2012 开始，DCB 组件通过 Microsoft 数据中心桥接 (DCB) 服务器功能进行安装和启用。 默认未安装此功能。

     

-   通过存储在系统注册表中并由独立硬件供应商定义的专有设置， (IHV) 用于网络适配器。 当 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数由 NDIS 调用时，微型端口驱动程序将读取这些设置。

-   通过由 IHV 开发的管理应用程序，将专用设置颁发给微型端口驱动程序。

当 DCB 组件发出 [oid \_ qos \_ 参数](./oid-qos-parameters.md)的 oid 方法请求时， **Ndis \_ qos \_ 参数 \_ 愿意** 使用 ndis qos 参数标志 **\_ \_ 。Flags** 成员指定微型端口驱动程序如何从本地 NDIS QoS 参数解析其操作 QoS 参数。 根据此标志，驱动程序将通过以下方式解析本地 QoS 参数：

-   如果设置了 " **NDIS \_ QOS \_ 参数 \_** " （带标志），微型端口驱动程序必须启用本地 DCB Exchange (DCBX) "愿意" 状态。 这允许对驱动程序进行远程配置，使其具有 QoS 参数。 在这种情况下，驱动程序将根据远程 QoS 参数解析其操作 QoS 参数。

    微型端口驱动程序还可以根据 IHV 定义的任何专有 QoS 设置来解析其操作 QoS 参数。 对于不是由对等方进行远程配置或由操作系统本地配置的 QoS 参数，驱动程序只能执行此操作。

    有关此过程的详细信息，请参阅 [接收远程 NDIS QoS 参数](receiving-remote-ndis-qos-parameters.md)。

-   如果未设置 "未设置 **NDIS \_ QOS \_ 参数 \_** " 标志，则微型端口驱动程序必须禁用本地 DCBX。 这允许驱动程序从其本地 QoS 参数而不是远程 QoS 参数解析其操作 QoS 参数。

    **注意**  如果已禁用本地 DCBX，则微型端口驱动程序仍然可以接受远程 QoS 参数，但不能使用它们来解析其操作 QoS 参数。

     

如果已禁用本地 DCBX，则微型端口驱动程序在管理其本地 QoS 参数时必须遵循以下指导原则：

-   微型端口驱动程序必须禁用或替代在 Ndis qos 参数中未设置相关 **NDIS \_ qos \_ 参数 \_ *Xxx* \_ 配置** 标志的任何本地 QoS **参数 \_ \_ 。Flags** 成员。

    例如，微型端口驱动程序可以用其专用设置替代由 IHV 定义的 QoS 参数。 如果没有使用 **NDIS \_ qos \_ 参数 \_ *Xxx* \_ 配置** 标志指定的本地 QoS 参数的专用设置，则驱动程序必须在网络适配器上禁用这些 qos 参数。

    **注意**  NDIS 保证同时设置或清除 **ndis \_ qos \_ 参数 \_ ETS \_ 配置** 的和 **ndis \_ qos \_ 参数 \_ PFC \_ 配置** 的标志。

     

-   小型端口驱动程序 *apply* 应在解析其操作 ndis qos 参数时应用 [**NDIS \_ qos \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构中包含的本地 QoS 参数。 如果驱动程序应用这些本地 QoS 参数，则它不能使用从远程对等端收到的任何远程 QoS 参数。

    有关此过程的详细信息，请参阅 [解决操作 NDIS QoS 参数](resolving-operational-ndis-qos-parameters.md)。

有关本地 DCBX 适用状态的详细信息，请参阅 [管理本地 DCBX 适用的状态](managing-the-local-dcbx-willing-state.md)。

 

