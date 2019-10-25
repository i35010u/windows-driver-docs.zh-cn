---
title: 初始化 VF 微型端口驱动程序
description: 初始化 VF 微型端口驱动程序
ms.assetid: 23EB2086-E882-4CB6-A910-D8E99E0212E5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac6e759c6e92277324e89f0c91d3d5de265d5d2d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824500"
---
# <a name="initializing-a-vf-miniport-driver"></a>初始化 VF 微型端口驱动程序


本主题介绍为 PCI Express （PCIe）虚拟功能（VF）的微型端口驱动程序编写[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数的准则。 VF 由支持单根 i/o 虚拟化（SR-IOV）的网络适配器公开。

> [!NOTE]
> 这些准则仅适用于 SR-IOV 网络适配器的 VF 微型端口驱动程序。 有关适配器的 PCIe 物理功能（PF）的微型端口驱动程序的初始化准则，请参阅[初始化 PF 微型端口驱动程序](initializing-a-pf-miniport-driver.md)。 

调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，VF 微型端口驱动程序与任何 NDIS 微型端口驱动程序遵循相同的步骤。 有关这些步骤的详细信息，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

除了这些步骤以外，在 NDIS 调用驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数时，VF 微型端口驱动程序还必须执行以下附加步骤：

- VF 微型端口驱动程序调用[**NdisGetHypervisorInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgethypervisorinfo)函数来验证它是否正在 hyper-v 子分区中运行。 此函数将返回[**NDIS\_虚拟机监控程序\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hypervisor_info)结构，该结构定义分区类型。 如果将分区类型报告为**NdisHypervisorPartitionMsHvChild**，则微型端口驱动程序将在附加到适配器上的 PF 的 hyper-v 子分区中运行。

  > [!NOTE] 
  > 如果将分区类型报告为**NdisHypervisorPartitionMsHvParent**，则微型端口驱动程序将在附加到适配器上的 PF 的 hyper-v 父分区中运行。 在这种情况下，微型端口驱动程序不得初始化为 VF 驱动程序。 如果可能，驱动程序必须初始化为 pf 驱动程序，如[Pf 小型端口驱动程序的初始化顺序](initialization-sequence-for-pf-miniport-drivers.md)中所述。     

- 与 PF 小型端口驱动程序不同，VF 微型端口驱动程序不得与 SR-IOV 标准化关键字一起安装，并且不能尝试读取这些关键字。 有关这些关键字的详细信息，请参阅[sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

- VF 微型端口驱动程序通过使用以下方式初始化的[**NDIS\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构来报告基础虚拟网络适配器的 sr-iov 硬件功能：

  1. 微型端口驱动程序初始化**标头**成员。 驱动程序将**标头**的**类型**成员设置为\_对象\_类型\_默认值。

     从 NDIS 6.30 开始，微型端口驱动程序会将**标头**的**修订**成员设置为 NDIS\_SRIOV\_功能 \_修订版本\_1，将**Size**成员设置为 ndis\_SIZEOF\_SRIOV\_功能\_修订版\_1。

  2. 微型端口驱动程序将 NDIS\_SRIOV\_\_CAP 设置为**SriovCapabilities**成员中\_微型端口标志，以报告 sr-iov 功能。

     > [!NOTE]
     > VF 微型端口驱动程序必须将 NDIS\_SRIOV\_CAP 设置为 "VF\_微型端口" 标志，并\_NDIS\_SRIOV\_CAP\_SRIOV\_支持的标志。         

  VF 微型端口驱动程序通过执行以下步骤，注册网络适配器的 SR-IOV 功能：

  1.  微型端口驱动程序初始化[**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

      微型端口驱动程序将**HardwareSriovCapabilities**和**CurrentSriovCapabilities**成员设置为指向 previouslyinitialized [**NDIS\_SRIOV\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_sriov_capabilities)结构的指针。

  2.  驱动程序调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) ，并将*MiniportAttributes*参数设置为指向[**NDIS\_微型端口的指针\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

- VF 微型端口驱动程序不得公布虚拟机队列（VMQ）功能。 但是，驱动程序可以为其他 NDIS 技术（如电源管理和接收方缩放（RSS））公布支持。

  有关 RSS 的详细信息，请参阅[接收方缩放](ndis-receive-side-scaling2.md)。

 

 





