---
title: PF 微型端口驱动程序的 DriverEntry 指导原则
description: PF 微型端口驱动程序的 DriverEntry 指导原则
ms.assetid: 6F885379-41EC-411E-8909-4DF48042849A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: accbf48f956754a0e38ef05d4baec396c73186e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838131"
---
# <a name="driverentry-guidelines-for-pf-miniport-drivers"></a>PF 微型端口驱动程序的 DriverEntry 指导原则


本主题介绍为 PCI Express （PCIe）物理功能（PF）的微型端口驱动程序编写[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)函数的准则。 PF 是支持单根 i/o 虚拟化（SR-IOV）的网络适配器组件。

**请注意**  这些准则仅适用于 PF 小型端口驱动程序。 有关适配器的 PCIe 虚拟功能（VF）的微型端口驱动程序的初始化准则，请参阅[初始化 VF 微型端口驱动程序](initializing-a-vf-miniport-driver.md)。

 

SR-IOV 网络适配器必须实现一个硬件桥，该桥将网络流量转发到适配器上的物理端口和内部虚拟端口（VPorts）。 此桥称为*NIC 交换机*。 有关详细信息，请参阅[NIC 交换机](nic-switches.md)。

如果 PF 微型端口驱动程序支持在 SR-IOV 网络适配器上静态创建 NIC 交换机，则在为设备堆栈中的网络适配器创建功能设备对象（FDO）时，可能需要分配交换机资源。 在这种情况下，驱动程序必须在 NDIS 调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)之前分配这些资源。 若要执行此操作，驱动程序必须注册可选的即插即用（PnP）处理程序，以便在设备堆栈中添加或删除适配器的 FDO 时可以参与此过程。

微型端口驱动程序必须提供[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数来注册这些 PnP 处理程序函数。 为此，驱动程序将从调用其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)函数的上下文中执行以下步骤：

1.  微型端口驱动程序使用*MiniportXxx*函数的入口点初始化[**NDIS\_微型端口\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构。 具体而言，驱动程序将**SetOptionsHandler**成员设置为驱动程序的[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数的入口点。

2.  微型端口驱动程序调用[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)函数来注册其入口点。 在此调用的上下文中，NDIS 调用驱动程序的[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数

3.  当 NDIS 调用[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)时，微型端口驱动程序会调用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数并指定一个[**NDIS\_微型\_PNP\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)结构。 此结构定义了[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)、 [*MiniportRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_remove_device)、 [*MiniportStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)和[*MiniportFilterResourceRequirements*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pnp_irp)函数的入口点。 当 NDIS 处理 PCI 总线驱动程序发出的 PnP i/o 请求数据包（Irp）时，NDIS 会调用这些处理程序函数。

    如果在 NDIS 调用驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数之前，PF 微型端口驱动程序必须为 NIC 交换机分配其他软件资源，则驱动程序必须注册[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)函数。 当 NDIS 调用*MiniportAddDevice*函数时，PF 微型端口驱动程序可以调用[**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)来读取注册表中的 NIC 交换机配置关键字设置。 有关这些关键字的详细信息，请参阅[sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

    有关[*MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_add_device)函数的准则的详细信息，请参阅[PF 微型端口驱动程序的*MiniportAddDevice*指南](miniportadddevice-guidelines-for-pf-miniport-drivers.md)。

有关如何创建 NIC 交换机的详细信息，请参阅[创建 Nic 交换机](creating-a-nic-switch.md)。

 

 





