---
title: PF 微型端口驱动程序的 DriverEntry 指导原则
description: PF 微型端口驱动程序的 DriverEntry 指导原则
ms.assetid: 6F885379-41EC-411E-8909-4DF48042849A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69c2cc2ff57eba7f7f92599e2c405d88b43f88fd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386552"
---
# <a name="driverentry-guidelines-for-pf-miniport-drivers"></a>PF 微型端口驱动程序的 DriverEntry 指导原则


本主题介绍进行写入的准则[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)微型端口驱动程序的 PCI Express (PCIe) 物理函数 (PF) 的函数。 PF 是支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器的组件。

**请注意**  这些指南仅适用于 PF 微型端口驱动程序。 微型端口驱动程序的 PCIe 虚拟函数 (VF) 的适配器的初始化准则，请参阅[初始化 VF 微型端口驱动程序](initializing-a-vf-miniport-driver.md)。

 

SR-IOV 网络适配器必须实现通过在适配器上的物理端口和内部虚拟端口 (VPorts) 转发网络流量的硬件桥梁。 此桥称为*NIC 交换机*。 有关详细信息，请参阅[NIC 开关](nic-switches.md)。

如果 PF 微型端口驱动程序支持 SR-IOV 网络适配器上的静态创建的 NIC 开关，它可能需要的功能的设备对象 (FDO) 创建设备堆栈中的网络适配器时分配交换机的资源。 在这种情况下，驱动程序必须分配这些资源之前 NDIS 调用[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)。 若要执行此操作，驱动程序必须注册可选即插即用 Play (PnP) 处理程序，以便它可以参与过程添加或从设备堆栈中删除适配器的 FDO 时。

微型端口驱动程序必须提供[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数来注册这些即插即用的处理程序函数。 若要执行此操作，驱动程序按照以下步骤从上下文调用其[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)函数：

1.  微型端口驱动程序初始化[ **NDIS\_微型端口\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构的入口点*MiniportXxx*函数。 具体而言，驱动程序设置**SetOptionsHandler**成员添加到驱动程序的入口点[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数。

2.  微型端口驱动程序调用[ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)函数以注册其入口点。 此调用的上下文中，从 NDIS 调用驱动程序的[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数

3.  当调用 NDIS [ *MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)，微型端口驱动程序调用[ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数，并指定[ **NDIS\_微型端口\_PNP\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_pnp_characteristics)结构。 此结构定义的入口点[ *MiniportAddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)， [ *MiniportRemoveDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_remove_device)， [ *MiniportStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pnp_irp)，并[ *MiniportFilterResourceRequirements* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pnp_irp)函数。 当处理 PCI 总线驱动程序发出的即插即用的 I/O 请求数据包 (Irp) 时，NDIS 调用这些处理程序函数。

    PF 微型端口驱动程序如果必须为 NIC 开关中分配额外的软件资源之前 NDIS 调用驱动程序的[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数，该驱动程序必须注册[*MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)函数。 当调用 NDIS *MiniportAddDevice*函数，PF 微型端口驱动程序可以调用[ **NdisReadConfiguration** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadconfiguration)读取 NIC 交换机配置关键字设置从注册表中。 有关这些关键字的详细信息，请参阅[SR-IOV 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

    详细了解的准则[ *MiniportAddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_add_device)函数中，请参阅[ *MiniportAddDevice* PF 微型端口驱动程序的准则](miniportadddevice-guidelines-for-pf-miniport-drivers.md).

有关如何创建 NIC 开关的详细信息，请参阅[创建 NIC 交换机](creating-a-nic-switch.md)。

 

 





