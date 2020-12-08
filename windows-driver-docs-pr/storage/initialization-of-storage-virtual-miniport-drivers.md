---
title: 存储器虚拟微型端口驱动程序的初始化
description: 存储器虚拟微型端口驱动程序的初始化
keywords:
- 存储虚拟微型端口驱动程序 WDK，初始化
- 微型端口驱动程序 WDK 存储
- 初始化 WDK 存储，虚拟微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60dfc030c9d9651e1ec1acf64757b0f5cac9c2cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835151"
---
# <a name="initialization-of-storage-virtual-miniport-drivers"></a>存储器虚拟微型端口驱动程序的初始化


Storport 虚拟小型端口 (VMiniport) 驱动程序具有三个初始化阶段。 在第一种情况下， (VMiniport 通常在其 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程) 调用 [**StorPortInitialize**](/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)，这将指向 [**虚拟 \_ HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data) 结构。

在此结构中，VMiniport 将以下字段设置为指向回调例程：

**HwFindAdapter**。 在第二个初始化阶段需要此例程。

**HwInitialize**。 第三个初始化阶段需要此例程。

**HwInitializeTracing**。 此例程是可选的，对于 Storport 虚拟微型端口驱动程序是唯一的。

**HwStartIo**。 此例程是必需的。 在虚拟微型端口驱动程序中，调用之前，不会调用 **HwStorBuildIo** 接口。 [**HwStorStartIo**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)。 调用之前，不会持有任何锁。 **HwStorStartIo**。 通过虚拟微型端口接口公开的每个逻辑单元的默认队列深度为250。

**HwAdapterControl**。 此例程是必需的。

**HwResetBus**。 此例程是必需的。 虚拟微型端口驱动程序开发人员可以定义 "总线" 的含义。

**HwProcessServiceRequest**。 此例程是可选的，对于 Storport 虚拟微型端口驱动程序是唯一的。 此例程会接收 "反向回调" IRP，此操作将在 VMiniport 更新调用方 (例如用户模式应用程序或内核模式驱动程序) 或要求调用方在 VMiniport 上执行某些操作时完成。

**HwCompleteServiceIrp**。 此例程是可选的，对于 Storport 虚拟微型端口驱动程序是唯一的。 但是，当 **HwProcessServiceRequest** 指向回调例程时，此例程是必需的。 删除虚拟适配器时，将调用 **HwCompleteServiceIrp** ，以便 VMiniport 可以完成任何可能挂起的反向回调 irp。

**HwFreeAdapterResources**。 此例程是必需的，并且对于 Storport 虚拟微型端口驱动程序是唯一的。 删除虚拟适配器时将调用此例程，以便 VMiniport 可以释放在初始化期间分配的任何资源。

**HwCleanupTracing**。 此例程是可选的，对于 Storport 虚拟微型端口驱动程序是唯一的。 但是，当 **HwInitializeTracing** 指向回调例程时，此例程是必需的。

虚拟微型端口驱动程序还必须在相同的结构中设置以下各项：

**HwInitializationDataSize**  = **sizeof** (虚拟 \_ HW \_ 初始化 \_ 数据) 。

**AdapterInterfaceType**  = **内部**。

Storport 虚拟微型端口驱动程序根据需要设置其他字段。 未使用的字段必须设置为零。

如果不持有任何锁，并且在被动 \_ 级别，虚拟微型端口驱动程序将使用指向 [**虚拟 \_ HW \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data)结构的指针调用 [**StorPortInitialize**](/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize) ，然后检查返回的状态。 Storport 驱动程序在此结构中保留其自己的信息副本，微型端口驱动程序无需在 **StorPortInitialize** 返回后保留此结构。

[**虚拟 \_硬件 \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/storport/ns-storport-_virtual_hw_initialization_data) 显示在 Storport. h 中。

 

