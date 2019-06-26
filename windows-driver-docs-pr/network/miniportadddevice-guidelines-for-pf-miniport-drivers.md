---
title: PF 微型端口驱动程序的 MiniportAddDevice 指导原则
description: PF 微型端口驱动程序的 MiniportAddDevice 指导原则
ms.assetid: D67FDBA0-C020-4557-9199-B9FF6F91DE6B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21619f7deaa5c5bad25a523ce92fe49779292428
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380881"
---
# <a name="miniportadddevice-guidelines-for-pf-miniport-drivers"></a>PF 微型端口驱动程序的 MiniportAddDevice 指导原则


本主题介绍进行写入的准则[ *MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)微型端口驱动程序的 PCI Express (PCIe) 物理函数 (PF) 的函数。 PF 是支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器的组件。

**请注意**  这些指南仅适用于 PF 微型端口驱动程序。 微型端口驱动程序的 PCIe 虚拟函数 (VF) 的适配器的初始化准则，请参阅[初始化 VF 微型端口驱动程序](initializing-a-vf-miniport-driver.md)。

 

插即用 (PnP) 管理器会调用 NDIS [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)函数来创建的网络适配器的功能的设备对象 (FDO)。 如果 PF 微型端口驱动程序已注册[ *MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)调用时的入口点[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)，NDIS调用的驱动程序*MiniportAddDevice*函数。

当[ *MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)调用时，PF 微型端口驱动程序可以分配其他软件资源对于 SR-IOV 和网络接口卡 (NIC) 切换。 通常情况下，这些是必须在之前 NDIS 调用驱动程序的分配的资源[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。

该驱动程序可以执行以下操作的调用上下文中[ *MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device):

-   PF 微型端口驱动程序可以调用[ **NdisReadConfiguration** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadconfiguration) SR-IOV 和 NIC 的交换机配置设置从注册表读取。 通过标准化的 SR-IOV 关键字来定义这些配置设置。 有关这些关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

-   基于这些配置设置，PF 微型端口驱动程序会为 SR-IOV 网络适配器分配其他软件资源。

**请注意**  实际分配硬件资源和 PCI 配置空间中的 SR-IOV，启用只能到调用上下文中执行[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize). 由于网络适配器的内存映射 I/O (MMIO) 空间未初始化时[ *MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)调用，微型端口驱动程序必须读取或写入到适配器之前*MiniportInitializeEx*调用。

 

 

 





