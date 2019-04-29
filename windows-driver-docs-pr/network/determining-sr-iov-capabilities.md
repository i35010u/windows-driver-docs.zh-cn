---
title: 确定 SR-IOV 功能
description: 确定 SR-IOV 功能
ms.assetid: 61895987-2469-471E-BB29-FF1CDD2869DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc33088464d31588e6cde641f6758e7441413610
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364200"
---
# <a name="determining-sr-iov-capabilities"></a>确定 SR-IOV 功能


本主题介绍如何 NDIS 和过量驱动程序确定网络适配器的单根 I/O 虚拟化 (SR-IOV) 功能。 本主题包含下列信息：

[报告期间的 SR-IOV 功能*MiniportInitializeEx*](#report)

[查询的 SR-IOV 功能的基础驱动程序](#query)

## <a name="reporting-sr-iov-capabilities-during-miniportinitializeex"></a>报告期间的 SR-IOV 功能*MiniportInitializeEx*


当 NDIS 调用微型端口驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数，该驱动程序提供的 SR-IOV 功能如下：

-   一组完整的 SR-IOV 网络适配器可以支持的硬件功能。

-   当前在网络适配器启用 SR-IOV 功能。

-   是否微型端口驱动程序就管理 PCI Express (PCIe) 物理函数 (PF) 或虚拟函数 (VF) 上的网络适配器。

微型端口驱动程序报告通过基础的网络适配器的 SR-IOV 硬件功能[ **NDIS\_SRIOV\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451677)初始化的结构按以下方式：

1. 微型端口驱动程序初始化**标头**成员。 驱动程序集**类型**的成员**标头**到 NDIS\_对象\_类型\_默认值。

   从开始 NDIS 6.30，微型端口驱动程序设置**修订**的成员**标头**到 NDIS\_SRIOV\_功能\_修订\_1 和**大小**成员添加到 NDIS\_SIZEOF\_SRIOV\_功能\_修订\_1。

2. 微型端口驱动程序设置相应标志**SriovCapabilities**成员添加到报表的 SR-IOV 功能。

   如果网络适配器支持 SR-IOV，适配器的 PCI Express (PCIe) 物理功能的微型端口驱动程序必须设置以下标志：

   -   NDIS\_SRIOV\_CAPS\_SRIOV\_支持

   -   NDIS\_SRIOV\_CAPS\_PF\_微型端口

   > [!NOTE]
   > 微型端口驱动程序为 PCIe 虚拟函数 (VF) 的网络适配器必须设置这两个 NDIS\_SRIOV\_CAPS\_VF\_微型端口标志和 NDIS\_SRIOV\_CAPS\_SRIOV\_支持标志。    

当 NDIS 调用微型端口驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数，该驱动程序注册的网络适配器的 SR-IOV 功能通过执行以下步骤：

1.  微型端口驱动程序初始化[ **NDIS\_微型端口\_适配器\_硬件\_协助\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构。

    微型端口驱动程序集**HardwareSriovCapabilities**指向以前初始化的指针到成员[ **NDIS\_SRIOV\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451677)结构。

    如果的注册表设置 **\*SRIOV** INF 关键字的一个值，则当前的网络适配器上启用 SR-IOV 功能。 微型端口驱动程序集**CurrentSriovCapabilities**指向相同的指针到成员[ **NDIS\_SRIOV\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451677)结构.

    如果的注册表设置 **\*SRIOV** INF 关键字的值为零、 当前的网络适配器上禁用 SR-IOV 功能。 微型端口驱动程序必须设置**CurrentSriovCapabilities**为 NULL 的成员。

    有关详细信息 **\*SRIOV** INF 关键字，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

2.  驱动程序调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)并设置*MiniportAttributes*参数指向的指针[ **NDIS\_微型端口\_适配器\_硬件\_帮助\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构。

有关适配器初始化过程的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。

## <a name="querying-sr-iov-capabilities-by-overlying-drivers"></a>查询的 SR-IOV 功能的基础驱动程序


NDIS 将传递到过量按以下方式绑定到的网络适配器的驱动程序的网络适配器当前已启用的 SR-IOV 功能：

-   当 NDIS 调用过量的筛选器驱动程序的[ *FilterAttach* ](https://msdn.microsoft.com/library/windows/hardware/ff549905)函数，NDIS 传递网络适配器的 SR-IOV 功能*AttachParameters*参数。 此参数包含一个指向[ **NDIS\_筛选器\_附加\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565481)结构。 **SriovCapabilities**此结构的成员包含一个指向[ **NDIS\_SRIOV\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451677)结构。

-   当 NDIS 调用基础协议驱动[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)函数，NDIS 传递网络适配器的 SR-IOV 功能通过*BindParameters*参数。 此参数包含一个指向[ **NDIS\_筛选器\_附加\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff565481)结构。 **SriovCapabilities**此结构的成员包含一个指向[ **NDIS\_SRIOV\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451677)结构。

NDIS 也会返回[ **NDIS\_SRIOV\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451677)结构，它处理的对象标识符 (OID) 查询请求时[OID\_SRIOV\_硬件\_功能](https://msdn.microsoft.com/library/windows/hardware/hh451862)并[OID\_SRIOV\_当前\_功能](https://msdn.microsoft.com/library/windows/hardware/hh451859)由过量协议颁发或筛选器驱动程序。

 

 





