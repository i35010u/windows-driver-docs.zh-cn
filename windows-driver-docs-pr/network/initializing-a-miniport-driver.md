---
title: 初始化微型端口驱动程序
description: 初始化微型端口驱动程序
ms.assetid: cda2437c-b292-4d21-b200-89c7b55cd46c
keywords:
- 微型端口驱动程序 WDK 连接网络、 初始化
- 初始化微型端口驱动程序
- NDIS 微型端口驱动程序 WDK，初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b8c3e70b744f0dbae050466f6587b1aab52fa05
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381327"
---
# <a name="initializing-a-miniport-driver"></a>初始化微型端口驱动程序



当网络设备可用时，系统可加载 NDIS 微型端口驱动程序来管理设备 （如果尚未加载该驱动程序）。 每个微型端口驱动程序必须提供[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)函数。 系统调用**DriverEntry**加载驱动程序后。 **DriverEntry**注册 NDIS （包括受支持的 NDIS 版本和驱动程序入口点） 的微型端口驱动程序的特征。

系统将为两个参数传递[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize):

-   指向已通过 I/O 系统的驱动程序对象的指针。

-   指定存储特定于驱动程序的参数的位置的注册表路径指向的指针。

在中[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)，对的调用中的微型端口驱动程序通过这两个这些指针[NdisMRegisterMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)函数。 微型端口驱动程序导出的一组标准*MiniportXxx*通过将存储在其入口点函数[ **NDIS\_微型端口\_驱动程序\_特征** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构并将传递到该结构**NdisMRegisterMiniportDriver**。 

**DriverEntry**微型端口驱动程序返回到调用返回的值**NdisMRegisterMiniportDriver**。

微型端口驱动程序还执行要求中的任何其他特定于驱动程序初始化[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)。 该驱动程序执行中的特定于适配器的初始化[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数。 有关适配器初始化的详细信息，请参阅[初始化适配器](initializing-a-miniport-adapter.md)。

[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)可以分配[ **NDIS\_微型端口\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构在堆栈上，因为 NDIS 库复制对自己存储相关信息。 **DriverEntry**应清除与此结构的内存[NdisZeroMemory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiszeromemory)之前在其成员中设置任何驱动程序所提供的值。 **MajorNdisVersion**并**MinorNdisVersion**成员必须包含的 NDIS 驱动程序支持的主版本号和次版本。 在每个 Xxx**处理程序**特征结构中的成员**DriverEntry**必须设置的驱动程序提供的入口点*MiniportXxx*函数或成员必须是**NULL**。

若要启用微型端口驱动程序以配置可选服务，NDIS 调用[MiniportSetOptions](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)微型端口驱动程序的调用的上下文中的函数[NdisMRegisterMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)。 可选的服务的详细信息，请参阅[配置可选的微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)。

驱动程序调用[NdisMRegisterMiniportDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)必须为 NDIS 调用准备其[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数之后的任何时间**DriverEntry**返回。 此类驱动程序必须具有足够安装和配置信息存储在注册表中，也可以从调用**NdisXxx**总线类型特定的配置函数设置了任何资源，NIC 特定于驱动程序将需要执行网络 I/O 操作。

微型端口驱动程序必须最终调用[ **NdisMDeregisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismderegisterminiportdriver)释放它通过调用分配的资源[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver). 如果驱动程序初始化失败，则在调用后**NdisMRegisterMiniportDriver**成功，驱动程序可以调用**NdisMDeregisterMiniportDriver**中[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize). 否则，微型端口驱动程序必须释放它分配中的特定于驱动程序的资源及其[ *MiniportDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_unload)函数。 换而言之，如果 NdisMRegisterMiniportDriver 不返回 NDIS_STATUS_SUCCESS， **DriverEntry**必须释放任何资源之前会将控件返回对它进行分配。 如果发生这种情况，将不加载该驱动程序。 有关详细信息，请参阅[卸载微型端口驱动程序](unloading-a-miniport-driver.md)。

 

 





