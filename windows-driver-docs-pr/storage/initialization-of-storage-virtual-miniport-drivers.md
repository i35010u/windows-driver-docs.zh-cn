---
title: 存储器虚拟微型端口驱动程序的初始化
description: 存储器虚拟微型端口驱动程序的初始化
ms.assetid: 35f7bb00-56e0-4535-9f13-9fd33afaa0b5
keywords:
- 存储虚拟微型端口驱动程序 WDK、 初始化
- 微型端口驱动程序 WDK 存储
- 初始化 WDK 存储，虚拟微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15c466f5f3ec9a8ecd6fb75931038ef45b6002fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379103"
---
# <a name="initialization-of-storage-virtual-miniport-drivers"></a>存储器虚拟微型端口驱动程序的初始化


Storport 虚拟微型端口 (VMiniport) 驱动程序包含三个阶段的初始化。 在第一个 VMiniport (通常是在其[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程) 调用[ **StorPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)，它指向[**虚拟\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)结构。

在此结构 VMiniport 设置以下字段，用于指向回调例程：

**HwFindAdapter**。 此例程用于初始化的第二个阶段是必需的。

**HwInitialize**。 此例程用于初始化的第三个阶段是必需的。

**HwInitializeTracing**。 此例程是可选的并且是唯一的 Storport 虚拟微型端口驱动程序。

**HwStartIo**。 此例程是必需的。 在虚拟微型端口驱动程序， **HwStorBuildIo**接口不会调用之前调用。 [**HwStorStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio). 不持有锁之前调用。 **HwStorStartIo**。 通过虚拟微型端口接口公开每个逻辑单元的默认队列深度为 250 个字符。

**HwAdapterControl**。 此例程是必需的。

**HwResetBus**。 此例程是必需的。 可通过虚拟微型端口驱动程序开发人员定义的"总线"的含义。

**HwProcessServiceRequest**。 此例程是可选的并且是唯一的 Storport 虚拟微型端口驱动程序。 此例程会收到"反向回叫"IRP，VMiniport 更新 （如用户模式应用程序或内核模式驱动程序） 调用方或要求调用方执行某些 VMiniport 代表操作时将完成。

**HwCompleteServiceIrp**。 此例程是可选的并且是唯一的 Storport 虚拟微型端口驱动程序。 但是，此例程时，必须**HwProcessServiceRequest**指向回调例程。 **HwCompleteServiceIrp** ，以便 VMiniport 可以完成任何可能处于挂起状态的反向回调 Irp 正在移除虚拟适配器时调用。

**HwFreeAdapterResources**。 此例程是必需的并且是唯一的 Storport 虚拟微型端口驱动程序。 此例程称为时正在删除虚拟适配器，以便 VMiniport 可以释放在初始化期间分配的任何资源。

**HwCleanupTracing**。 此例程是可选的并且是唯一的 Storport 虚拟微型端口驱动程序。 但是，此例程时，必须**HwInitializeTracing**指向回调例程。

虚拟微型端口驱动程序还必须在同一结构中设置以下：

**HwInitializationDataSize** = **sizeof**(虚拟\_HW\_初始化\_数据)。

**AdapterInterfaceType** = **内部**。

Storport 虚拟微型端口驱动程序根据需要设置其他字段。 未使用的字段必须设置为零。

无需按任何锁，而在被动\_级别，虚拟微型端口驱动程序调用[ **StorPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportinitialize)用一个指针指向[**虚拟\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data)结构，然后检查返回的状态。 Storport 驱动程序将保留其自己的此结构中的信息副本和微型端口驱动程序不需要保留后的此结构**StorPortInitialize**返回。

[**虚拟\_HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_virtual_hw_initialization_data) Storport.h 所示。

 

 




