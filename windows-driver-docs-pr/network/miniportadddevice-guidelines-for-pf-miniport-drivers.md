---
title: PF 微型端口驱动程序的 MiniportAddDevice 指导原则
description: PF 微型端口驱动程序的 MiniportAddDevice 指导原则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f40046f38771c3f138d4ed3a1beb6ec832280ccf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786111"
---
# <a name="miniportadddevice-guidelines-for-pf-miniport-drivers"></a>PF 微型端口驱动程序的 MiniportAddDevice 指导原则


本主题介绍了为 PCI Express (PCIe 的微型端口驱动程序编写 [*MiniportAddDevice*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device) 函数的准则) 物理功能 (PF) 。 PF 是网络适配器的一个组件，它支持 (SR-IOV) 的单个根 i/o 虚拟化。

**注意**  这些准则仅适用于 PF 小型端口驱动程序。 有关使用 (VF) 适配器的 PCIe 虚函数的小型端口驱动程序的初始化准则，请参阅 [初始化 VF 微型端口驱动程序](initializing-a-vf-miniport-driver.md)。

 

即插即用 (PnP) 管理器调用 NDIS [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 函数为网络适配器创建 (FDO) 的功能设备对象。 如果 PF 微型端口驱动程序在调用 [**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)时注册了 [*MiniportAddDevice*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)入口点，NDIS 将调用驱动程序的 *MiniportAddDevice* 函数。

调用 [*MiniportAddDevice*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device) 时，PF 微型端口驱动程序可以为 sr-iov 和网络接口卡分配其他软件资源， (NIC) 交换机。 通常，这些资源必须在 NDIS 调用驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数之前分配。

驱动程序可以在对 [*MiniportAddDevice*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)的调用上下文中执行以下操作：

-   PF 微型端口驱动程序可以调用 [**NdisReadConfiguration**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration) 从注册表中读取 SR-IOV 和 NIC 交换机的配置设置。 这些配置设置是通过标准化 SR-IOV 关键字定义的。 有关这些关键字的详细信息，请参阅 [sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

-   根据这些配置设置，PF 微型端口驱动程序为 SR-IOV 网络适配器分配额外的软件资源。

**注意**  硬件资源的实际分配和 PCI 配置空间中的 SR-IOV 启用只能在对 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)的调用的上下文中完成。 由于网络适配器的内存映射 i/o (MMIO) 空间在调用 [*MiniportAddDevice*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device) 时未初始化，因此，在调用 *MiniportInitializeEx* 之前，微型端口驱动程序不得读取或写入适配器。

 

 

