---
title: 初始化筛选器驱动程序
description: 初始化筛选器驱动程序
ms.assetid: e24b18b5-76d3-4d56-bf60-0dea91ba014e
keywords:
- 筛选器驱动程序 WDK 网络，初始化
- NDIS 筛选器驱动程序 WDK，初始化
- 初始化筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96f59e4d9378b93ac72d29f8f7ff9d74a198af65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824601"
---
# <a name="initializing-a-filter-driver"></a>初始化筛选器驱动程序



筛选器驱动程序初始化在系统加载驱动程序后立即进行。 筛选驱动程序作为系统服务加载。 系统可以在加载微型端口驱动程序之前、期间或之后加载筛选器驱动程序。 当筛选器驱动程序支持的类型的微型端口适配器可用且筛选器驱动程序初始化完成后，NDIS 可以将筛选器模块附加到小型端口适配器。

当驱动程序堆栈正在启动时，系统会加载筛选器驱动程序（如果尚未加载这些驱动程序）。 有关启动包含筛选器模块的驱动程序堆栈的详细信息，请参阅[启动驱动程序堆栈](starting-a-driver-stack.md)。

在加载筛选器驱动程序后，系统将调用驱动程序的[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程。 

系统将两个参数传递给[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)：

-   一个指针，指向由 i/o 系统创建的驱动程序对象。

-   指向注册表路径的指针，该路径指定存储驱动程序特定参数的位置。

如果驱动程序已成功注册为 NDIS 筛选器驱动程序， [DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)将返回 STATUS_SUCCESS 或其等效的 NDIS_STATUS_SUCCESS。 如果**DriverEntry**通过传播**NdisXxx**函数返回的错误状态或内核模式支持例程来初始化失败，则不会保持加载该驱动程序。 **DriverEntry**必须同步执行;也就是说，它不能返回 STATUS_PENDING 或其等效的 NDIS_STATUS_PENDING。

筛选器驱动程序在将 NDIS 注册为筛选器驱动程序时，会将驱动程序对象传递给[NdisFRegisterFilterDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)函数。 驱动程序可以使用注册表路径获取配置信息。 有关如何访问筛选器驱动程序配置信息的详细信息，请参阅[访问筛选器驱动程序的配置信息](accessing-configuration-information-for-a-filter-driver.md)。

筛选器驱动程序从其**DriverEntry**例程调用**NdisFRegisterFilterDriver** 。 筛选器驱动程序通过将[**NDIS\_筛选器\_驱动程序\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_driver_characteristics)结构传递到*FilterCharacteristics*参数处的**NdisFRegisterFilterDriver** ，来导出一组*FilterXxx*函数。

"NDIS\_筛选器"\_驱动程序\_特性结构指定必需的和可选的*FilterXxx*函数的入口点。 某些可选函数可以绕过。 有关跳过函数的详细信息，请参阅[数据绕过模式](data-bypass-mode.md)。

调用[NdisFRegisterFilterDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)的驱动程序必须准备好对其任何*FilterXxx*函数的立即调用。

NDIS\_筛选器\_驱动程序\_特征结构指定这些必需的*FilterXxx*函数的入口点：

[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)

[*FilterDetach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)

[*FilterRestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart)

[*FilterPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause)

NDIS\_筛选器\_驱动程序\_特征结构指定这些可选的入口点，而在运行时*FilterXxx*函数则不可更改：

[*FilterSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)

[*FilterSetModuleOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_set_module_options)

[*FilterOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request)

[*FilterOidRequestComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request_complete)

[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)

[*FilterNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_net_pnp_event)

[*FilterDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_device_pnp_event_notify)

[*FilterCancelSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_send_net_buffer_lists)

NDIS\_筛选器\_驱动程序\_特征结构指定这些可选的默认入口点，并在运行时*FilterXxx*函数中更改：

[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)

[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)

[*FilterReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)

[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)

前面的四个函数也在[**NDIS\_筛选器\_部分\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_partial_characteristics)结构中定义。 此结构通过从[*FilterSetModuleOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_set_module_options)函数调用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数来指定可在运行时更改的函数。 如果筛选器驱动程序将在运行时更改这些部分特征，则必须提供*FilterSetModuleOptions*的入口点。 每个筛选器模块的部分特性可能不同。 有关详细信息，请参阅[启动筛选器模块](starting-a-filter-module.md)。

NDIS 在对**NdisFRegisterFilterDriver**的调用的上下文中调用*FilterSetOptions*函数。 *FilterSetOptions*向 NDIS 注册可选服务。 有关详细信息，请参阅[配置可选筛选器驱动程序服务](configuring-optional-filter-driver-services.md)。

如果对**NdisFRegisterFilterDriver**的调用成功，NDIS 将使用筛选器驱动程序句柄填充*NdisFilterDriverHandle*中的变量。 筛选器驱动程序将保存此句柄，稍后将此句柄传递给需要筛选器驱动程序句柄作为输入参数的 NDIS 函数（如[**NdisFDeregisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfderegisterfilterdriver)）。 卸载驱动程序时，必须调用**NdisFDeregisterFilterDriver**函数来释放由**NdisFRegisterFilterDriver**分配的驱动程序资源。

*FilterSetOptions*返回后，筛选器模块处于*分离*状态。 调用*FilterSetOptions*后，NDIS 可以随时调用筛选器驱动程序的[*FilterAttach*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach)函数。 驱动程序在*FilterAttach*函数中执行筛选器模块特定的初始化。 有关将筛选器模块附加到驱动程序堆栈的详细信息，请参阅[附加筛选器模块](attaching-a-filter-module.md)。

筛选器驱动程序还会执行它在**DriverEntry**中所需的任何其他特定于驱动程序的初始化。 筛选器驱动程序必须释放它在[*FilterDriverUnload*](https://docs.microsoft.com/windows-hardware/drivers/network/unloading-a-filter-driver)例程中分配的特定于驱动程序的资源。 有关详细信息，请参阅[卸载筛选器驱动程序](unloading-a-filter-driver.md)。

 

 





