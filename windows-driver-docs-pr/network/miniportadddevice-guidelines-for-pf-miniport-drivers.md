---
title: MiniportAddDevice PF 微型端口驱动程序的指导原则
description: MiniportAddDevice PF 微型端口驱动程序的指导原则
ms.assetid: D67FDBA0-C020-4557-9199-B9FF6F91DE6B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76d3f86315c42456580a13f8bc893b8fd0e03c12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533700"
---
# <a name="miniportadddevice-guidelines-for-pf-miniport-drivers"></a>MiniportAddDevice PF 微型端口驱动程序的指导原则


本主题介绍进行写入的准则[ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)微型端口驱动程序的 PCI Express (PCIe) 物理函数 (PF) 的函数。 PF 是支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器的组件。

**请注意**  这些指南仅适用于 PF 微型端口驱动程序。 微型端口驱动程序的 PCIe 虚拟函数 (VF) 的适配器的初始化准则，请参阅[初始化 VF 微型端口驱动程序](initializing-a-vf-miniport-driver.md)。

 

插即用 (PnP) 管理器会调用 NDIS [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)函数来创建的网络适配器的功能的设备对象 (FDO)。 如果 PF 微型端口驱动程序已注册[ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)调用时的入口点[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)，NDIS调用的驱动程序*MiniportAddDevice*函数。

当[ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)调用时，PF 微型端口驱动程序可以分配其他软件资源对于 SR-IOV 和网络接口卡 (NIC) 切换。 通常情况下，这些是必须在之前 NDIS 调用驱动程序的分配的资源[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。

该驱动程序可以执行以下操作的调用上下文中[ *MiniportAddDevice*](https://msdn.microsoft.com/library/windows/hardware/ff559332):

-   PF 微型端口驱动程序可以调用[ **NdisReadConfiguration** ](https://msdn.microsoft.com/library/windows/hardware/ff564511) SR-IOV 和 NIC 的交换机配置设置从注册表读取。 通过标准化的 SR-IOV 关键字来定义这些配置设置。 有关这些关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

-   基于这些配置设置，PF 微型端口驱动程序会为 SR-IOV 网络适配器分配其他软件资源。

**请注意**  实际分配硬件资源和 PCI 配置空间中的 SR-IOV，启用只能到调用上下文中执行[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389). 由于网络适配器的内存映射 I/O (MMIO) 空间未初始化时[ *MiniportAddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff559332)调用，微型端口驱动程序必须读取或写入到适配器之前*MiniportInitializeEx*调用。

 

 

 





