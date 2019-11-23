---
title: 确定 SR-IOV 功能
description: 确定 SR-IOV 功能
ms.assetid: 61895987-2469-471E-BB29-FF1CDD2869DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95b2302470e0795960a1525450dffe4df205c07e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834908"
---
# <a name="determining-sr-iov-capabilities"></a>确定 SR-IOV 功能


本主题介绍 NDIS 和过量驱动程序如何确定网络适配器的单个根 i/o 虚拟化（SR-IOV）功能。 本主题包含下列信息：

[在*MiniportInitializeEx*期间报告 sr-iov 功能](#reporting-sr-iov-capabilities-during-miniportinitializeex)

[通过过量驱动程序查询 SR-IOV 功能](#querying-sr-iov-capabilities-by-overlying-drivers)

## <a name="reporting-sr-iov-capabilities-during-miniportinitializeex"></a>在*MiniportInitializeEx*期间报告 sr-iov 功能


当 NDIS 调用微型端口驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，驱动程序提供以下 sr-iov 功能：

-   网络适配器可支持的一组完整的 SR-IOV 硬件功能。

-   当前在网络适配器上启用的 SR-IOV 功能。

-   微型端口驱动程序是否在网络适配器上管理 PCI Express （PCIe）物理功能（PF）或虚拟功能（VF）。

微型端口驱动程序通过使用以下方法初始化的[**NDIS\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构来报告基础网络适配器的 sr-iov 硬件功能：

1. 微型端口驱动程序初始化**标头**成员。 驱动程序将**标头**的**类型**成员设置为\_对象\_类型\_默认值。

   从 NDIS 6.30 开始，微型端口驱动程序会将**标头**的**修订**成员设置为 NDIS\_SRIOV\_功能 \_修订版本\_1，将**Size**成员设置为 ndis\_SIZEOF\_\_\_\_

2. 微型端口驱动程序在**SriovCapabilities**成员中设置相应的标志，以报告 sr-iov 功能。

   如果网络适配器支持 SR-IOV，则该适配器的 PCI Express （PCIe）物理功能的微型端口驱动程序必须设置以下标志：

   -   支持 NDIS\_SRIOV\_CAP\_SRIOV\_

   -   NDIS\_SRIOV\_CAP\_PF\_微型端口

   > [!NOTE]
   > 网络适配器的 PCIe 虚拟功能（VF）的微型端口驱动程序必须同时将 NDIS\_SRIOV\_\_CAP 设置为 "VF\_微型端口" 标志，并将 NDIS\_SRIOV\_CAP\_SRIOV\_支持的标志。    

当 NDIS 调用微型端口驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，驱动程序会按照以下步骤注册网络适配器的 sr-iov 功能：

1.  微型端口驱动程序初始化[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

    微型端口驱动程序将**HardwareSriovCapabilities**成员设置为指向先前初始化的[**NDIS\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构的指针。

    如果 **\*SRIOV** INF 关键字的注册表设置值为1，则当前在网络适配器上启用了 sr-iov 功能。 微型端口驱动程序将**CurrentSriovCapabilities**成员设置为指向同一[**NDIS\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构的指针。

    如果 **\*SRIOV** INF 关键字的注册表设置值为零，则该网络适配器上当前禁用了 sr-iov 功能。 微型端口驱动程序必须将**CurrentSriovCapabilities**成员设置为 NULL。

    有关 **\*SRIOV** INF 关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

2.  驱动程序调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) ，并将*MiniportAttributes*参数设置为指向[**NDIS\_微型端口的指针\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

有关适配器初始化过程的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。

## <a name="querying-sr-iov-capabilities-by-overlying-drivers"></a>通过过量驱动程序查询 SR-IOV 功能


NDIS 通过以下方式将网络适配器当前启用的 SR-IOV 功能传递到绑定到网络适配器的过量驱动程序：

-   当 NDIS 调用过量筛选器驱动程序的[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)函数时，Ndis 通过*AttachParameters*参数传递网络适配器的 sr-iov 功能。 此参数包含指向[**NDIS\_筛选器的指针\_ATTACH\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。 此结构的**SriovCapabilities**成员包含指向[**NDIS\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构的指针。

-   当 NDIS 调用过量协议驱动程序的[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数时，Ndis 通过*BindParameters*参数传递网络适配器的 sr-iov 功能。 此参数包含指向[**NDIS\_筛选器的指针\_ATTACH\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。 此结构的**SriovCapabilities**成员包含指向[**NDIS\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构的指针。

在处理\_OID 的对象标识符（OID）查询请求时，NDIS 还会返回[**ndis\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构[\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-hardware-capabilities)，以及由过量协议或筛选器驱动程序发出的[SRIOV\_当前\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-sriov-current-capabilities)。\_

 

 





