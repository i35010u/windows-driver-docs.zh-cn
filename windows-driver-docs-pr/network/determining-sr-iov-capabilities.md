---
title: 确定 SR-IOV 功能
description: 确定 SR-IOV 功能
ms.assetid: 61895987-2469-471E-BB29-FF1CDD2869DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47091c95b4f58e53dee12a94087fc9c02edca948
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212939"
---
# <a name="determining-sr-iov-capabilities"></a>确定 SR-IOV 功能


本主题介绍 NDIS 和过量驱动程序如何确定单个根 i/o 虚拟化 (网络适配器的 SR-IOV) 功能。 本主题包含以下信息：

[在*MiniportInitializeEx*期间报告 sr-iov 功能](#reporting-sr-iov-capabilities-during-miniportinitializeex)

[通过过量驱动程序查询 SR-IOV 功能](#querying-sr-iov-capabilities-by-overlying-drivers)

## <a name="reporting-sr-iov-capabilities-during-miniportinitializeex"></a>在*MiniportInitializeEx*期间报告 sr-iov 功能


当 NDIS 调用微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，驱动程序提供以下 sr-iov 功能：

-   网络适配器可支持的一组完整的 SR-IOV 硬件功能。

-   当前在网络适配器上启用的 SR-IOV 功能。

-   小型端口驱动程序是否在网络适配器上管理 PCI Express (PCIe) 物理功能 (PF) 或虚拟函数 (VF) 。

微型端口驱动程序通过以下方式初始化的 [**NDIS \_ SRIOV \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities) 结构报告基础网络适配器的 sr-iov 硬件功能：

1. 微型端口驱动程序初始化 **标头** 成员。 驱动程序将**标头**的**类型**成员设置为 NDIS \_ 对象 \_ 类型 \_ 默认值。

   从 NDIS 6.30 开始，微型端口驱动程序会将**标头**的**修订**成员设置为 ndis \_ SRIOV \_ 功能 \_ 修订版本 \_ 1，并将**Size**成员设置为 ndis \_ SIZEOF \_ SRIOV \_ 功能 \_ 修订版本 \_ 1。

2. 微型端口驱动程序在 **SriovCapabilities** 成员中设置相应的标志，以报告 sr-iov 功能。

   如果网络适配器支持 SR-IOV，则 PCI Express (PCIe) 物理功能的微型端口驱动程序必须设置以下标志：

   -   \_支持 NDIS SRIOV \_ CAP \_ SRIOV \_

   -   NDIS \_ SRIOV \_ CAP \_ PF \_ 小型端口

   > [!NOTE]
   > 网络适配器 (VF) 的 PCIe 虚拟功能的微型端口驱动程序必须同时设置 NDIS \_ SRIOV \_ cap \_ VF \_ 微型端口标志和 ndis \_ SRIOV \_ cap \_ SRIOV 支持的 \_ 标志。    

当 NDIS 调用微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，驱动程序会按照以下步骤注册网络适配器的 sr-iov 功能：

1.  微型端口驱动程序初始化 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes) 结构。

    微型端口驱动程序将 **HardwareSriovCapabilities** 成员设置为指向先前初始化的 [**NDIS \_ SRIOV \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities) 结构的指针。

    如果** \* SRIOV** INF 关键字的注册表设置值为1，则当前在网络适配器上启用 sr-iov 功能。 微型端口驱动程序将 **CurrentSriovCapabilities** 成员设置为指向同一 [**NDIS \_ SRIOV \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities) 结构的指针。

    如果** \* SRIOV** INF 关键字的注册表设置值为零，则该网络适配器上当前禁用了 sr-iov 功能。 微型端口驱动程序必须将 **CurrentSriovCapabilities** 成员设置为 NULL。

    有关** \* SRIOV** INF 关键字的详细信息，请参阅[Sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

2.  驱动程序调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) ，并将 *MiniportAttributes* 参数设置为指向 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes) 结构的指针。

有关适配器初始化过程的详细信息，请参阅 [初始化微型端口适配器](initializing-a-miniport-adapter.md)。

## <a name="querying-sr-iov-capabilities-by-overlying-drivers"></a>通过过量驱动程序查询 SR-IOV 功能


NDIS 通过以下方式将网络适配器当前启用的 SR-IOV 功能传递到绑定到网络适配器的过量驱动程序：

-   当 NDIS 调用过量筛选器驱动程序的 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach) 函数时，Ndis 通过 *AttachParameters* 参数传递网络适配器的 sr-iov 功能。 此参数包含指向 [**NDIS \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters) 结构的指针。 此结构的 **SriovCapabilities** 成员包含指向 [**NDIS \_ SRIOV \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities) 结构的指针。

-   当 NDIS 调用过量协议驱动程序的 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex) 函数时，Ndis 通过 *BindParameters* 参数传递网络适配器的 sr-iov 功能。 此参数包含指向 [**NDIS \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters) 结构的指针。 此结构的 **SriovCapabilities** 成员包含指向 [**NDIS \_ SRIOV \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities) 结构的指针。

NDIS 还会返回 [**ndis \_ SRIOV \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities) 结构， () oid 处理 [oid \_ SRIOV \_ 硬件 \_ 功能](./oid-sriov-hardware-capabilities.md) 的请求对象标识符，以及由过量协议或筛选器驱动程序颁发的 [oid \_ SRIOV \_ 当前 \_ 功能](./oid-sriov-current-capabilities.md) 。

 

