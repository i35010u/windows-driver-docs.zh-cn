---
title: 初始化 VF 微型端口驱动程序
description: 初始化 VF 微型端口驱动程序
ms.assetid: 23EB2086-E882-4CB6-A910-D8E99E0212E5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2911ef3105d352abd0e0383e4ed6746e38f99fd7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564298"
---
# <a name="initializing-a-vf-miniport-driver"></a>初始化 VF 微型端口驱动程序


本主题介绍进行写入的准则[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)微型端口驱动程序为 PCI Express (PCIe) 虚拟函数 (VF) 的函数。 VF 公开支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器。

> [!NOTE]
> 这些指南仅适用于 VF SR-IOV 网络适配器的微型端口驱动程序。 微型端口驱动程序的 PCIe 物理函数 (PF) 的适配器的初始化准则，请参阅[初始化 PF 微型端口驱动程序](initializing-a-pf-miniport-driver.md)。 

VF 微型端口驱动程序遵循相同的步骤为任何 NDIS 微型端口驱动程序时其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)调用函数。 有关这些步骤的详细信息，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

这些步骤中，除了 VF 微型端口驱动程序时必须遵守下列附加步骤 NDIS 调用驱动程序的[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数：

- VF 微型端口驱动程序调用[ **NdisGetHypervisorInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff562635)函数来验证它是否正在运行的 HYPER-V 子分区中。 此函数将返回[ **NDIS\_虚拟机监控程序\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565708)结构定义分区类型。 如果分区类型将报告为**NdisHypervisorPartitionMsHvChild**，微型端口驱动程序是否正在附加到 PF 的适配器上的 HYPER-V 子分区。

  > [!NOTE] 
  > 如果分区类型将报告为**NdisHypervisorPartitionMsHvParent**，微型端口驱动程序运行附加到在适配器上 PF 在 HYPER-V 父分区中。 在这种情况下，微型端口驱动程序必须初始化为某个 VF 驱动程序。 如果可能，该驱动程序必须将初始化为 PF 驱动程序中所述[PF 微型端口驱动程序的初始化序列](initialization-sequence-for-pf-miniport-drivers.md)。     

- 与 PF 微型端口驱动程序，不同 VF 微型端口驱动程序不得安装使用 SR-IOV 标准化关键字，必须尝试读取这些关键字。 有关这些关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

- VF 微型端口驱动程序报告通过基础的虚拟网络适配器的 SR-IOV 硬件功能[ **NDIS\_SRIOV\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451677)结构，它是按以下方式初始化：

  1. 微型端口驱动程序初始化**标头**成员。 驱动程序集**类型**的成员**标头**到 NDIS\_对象\_类型\_默认值。

     从开始 NDIS 6.30，微型端口驱动程序设置**修订**的成员**标头**到 NDIS\_SRIOV\_功能\_修订\_1 和**大小**成员添加到 NDIS\_SIZEOF\_SRIOV\_功能\_修订\_1。

  2. 微型端口驱动程序设置 NDIS\_SRIOV\_CAPS\_PF\_中的微型端口标志**SriovCapabilities**成员添加到报表的 SR-IOV 功能。

     > [!NOTE]
     > VF 微型端口驱动程序必须设置这两个 NDIS\_SRIOV\_CAPS\_VF\_微型端口标志和 NDIS\_SRIOV\_CAPS\_SRIOV\_支持标志。         

  VF 微型端口驱动程序注册的网络适配器的 SR-IOV 功能通过执行以下步骤：

  1.  微型端口驱动程序初始化[ **NDIS\_微型端口\_适配器\_硬件\_协助\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构。

      微型端口驱动程序集**HardwareSriovCapabilities**并**CurrentSriovCapabilities** previouslyinitialized 指向的指针到成员[ **NDIS\_SRIOV\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451677)结构。

  2.  驱动程序调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)并设置*MiniportAttributes*参数指向的指针[ **NDIS\_微型端口\_适配器\_硬件\_帮助\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)结构。

- VF 微型端口驱动程序必须播发虚拟机队列 (VMQ) 功能。 但是，该驱动程序可以公布其他 NDIS 技术，如电源管理的支持，并且接收方缩放 (RSS)。

  有关 RSS 的详细信息，请参阅[接收方伸缩](ndis-receive-side-scaling2.md)。

 

 





