---
title: 初始化微型端口驱动程序
description: 初始化微型端口驱动程序
keywords:
- 微型端口驱动程序 WDK 网络，初始化
- 初始化微型端口驱动程序
- NDIS 微型端口驱动程序 WDK，初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aee382e8ff97a025370fc99ff9cde7418a889641
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803701"
---
# <a name="initializing-a-miniport-driver"></a>初始化微型端口驱动程序



当网络设备可用时，系统会加载 NDIS 微型端口驱动程序来管理设备， (如果尚未加载该驱动程序) 。 每个微型端口驱动程序必须提供 [DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 函数。 系统在加载驱动程序后调用 **DriverEntry** 。 **DriverEntry** 会将微型端口驱动程序的特征注册到 ndis (包括受支持的 ndis 版本和驱动程序入口点) 。

系统将两个参数传递给 [DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)：

-   一个指针，指向由 i/o 系统创建的驱动程序对象。

-   指向注册表路径的指针，该路径指定存储驱动程序特定参数的位置。

在 [DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)中，微型端口驱动程序在对 [NdisMRegisterMiniportDriver](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) 函数的调用中传递两个指针。 微型端口驱动程序通过将其入口点存储在 [**NDIS \_ 微型端口 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构中并将该结构传递给 **NdisMRegisterMiniportDriver**，来导出一组标准 *MiniportXxx* 函数。 

微型端口驱动程序的 **DriverEntry** 返回通过调用 **NdisMRegisterMiniportDriver** 返回的值。

微型端口驱动程序还会执行它在 [DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)中所需的任何其他特定于驱动程序的初始化。 驱动程序在 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数中执行适配器特定的初始化。 有关适配器初始化的详细信息，请参阅 [初始化适配器](initializing-a-miniport-adapter.md)。

[DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 可以在堆栈上分配 [**ndis \_ 微型端口 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics) 结构，因为 ndis 库将相关信息复制到其自己的存储中。 **DriverEntry** 应在设置任何驱动程序在其成员中提供的值之前清除 [NdisZeroMemory](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiszeromemory) 的此结构的内存。 **MajorNdisVersion** 和 **MinorNdisVersion** 成员必须包含驱动程序支持的 NDIS 的主要版本和次要版本。 在特征结构的每个 Xxx **处理程序** 成员中， **DriverEntry** 必须设置驱动程序提供的 *MiniportXxx* 函数的入口点，或者该成员必须为 **NULL**。

为了使微型端口驱动程序可以配置可选服务，NDIS 在微型端口驱动程序对[NdisMRegisterMiniportDriver](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)的调用的上下文中调用[MiniportSetOptions](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数。 有关可选服务的详细信息，请参阅 [配置可选微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)。

调用 [NdisMRegisterMiniportDriver](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)的驱动程序必须准备好，以便在 **DriverEntry** 返回后，NDIS 调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数。 此类驱动程序必须将安装和配置信息存储在注册表中，或通过调用 **NdisXxx** 总线类型特定的配置函数来设置任何 NIC 特定的资源，驱动程序将需要执行网络 i/o 操作。

小型端口驱动程序最终必须调用 [**NdisMDeregisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver) 来释放通过调用 [**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)分配的资源。 如果在对 **NdisMRegisterMiniportDriver** 的调用成功之后驱动程序初始化失败，则驱动程序可以从 [DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)中调用 **NdisMDeregisterMiniportDriver** 。 否则，微型端口驱动程序必须释放它在 [*MiniportDriverUnload*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload) 函数中分配的特定于驱动程序的资源。 换言之，如果 NdisMRegisterMiniportDriver 未返回 NDIS_STATUS_SUCCESS，则 **DriverEntry** 必须释放它在返回 control 之前分配的所有资源。 如果出现这种情况，则不会加载驱动程序。 有关详细信息，请参阅 [卸载微型端口驱动程序](unloading-a-miniport-driver.md)。

 

