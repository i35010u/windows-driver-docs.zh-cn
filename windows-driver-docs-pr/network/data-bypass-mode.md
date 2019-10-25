---
title: 数据旁路模式
description: 数据旁路模式
ms.assetid: 98061803-22de-4fa2-8582-2d382f84dd75
keywords:
- 筛选器驱动程序 WDK 网络，数据旁路模式
- NDIS 筛选器驱动程序 WDK，数据旁路模式
- 数据绕过模式 WDK 网络
- 旁路模式 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d84b72157aa7e54d084d68dba326e263cf4876f8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838174"
---
# <a name="data-bypass-mode"></a>数据旁路模式





筛选器驱动程序*数据旁路模式*可以提高系统性能。 NDIS 不会调用被绕过的*FilterXxx*函数。 例如，如果给定筛选器应用程序不需要发送和接收服务，则筛选器驱动程序可以绕过发送和接收功能。

筛选器驱动程序在调用[**NdisFRegisterFilterDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfregisterfilterdriver)函数时，为可以绕过的函数指定默认入口点。 默认情况下，这些入口点对于被绕过的函数是**NULL** 。 有关初始化的详细信息，请参阅[初始化筛选器驱动程序](initializing-a-filter-driver.md)。

若要在运行时更改绕过状态，驱动程序必须在驱动程序初始化过程中为[*FilterSetModuleOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_set_module_options)函数指定入口点。 驱动程序可以初始化[**NDIS\_筛选器\_部分\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_partial_characteristics)结构，并从 FilterSetModuleOptions 的上下文中将新特征传递到[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数.

在重启操作开始时，NDIS 将调用*FilterSetModuleOptions*函数（如果有）。 筛选器驱动程序可以独立地为每个筛选器模块设置旁路模式。 有关详细信息，请参阅[启动筛选器模块](starting-a-filter-module.md)。

筛选器驱动程序可以绕过 NDIS\_筛选器中指定的以下可选*FilterXxx*函数[ **\_DRIVER\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_driver_characteristics)结构：

[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)

[*FilterSendNetBufferListsComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists_complete)

[*FilterCancelSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_send_net_buffer_lists)

[*FilterReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)

[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)

若要将*FilterXxx*函数设置为绕过模式，筛选器驱动程序为该函数的入口点指定了**NULL** 。 但是，如果驱动程序调用具有关联的*FilterXxx*函数的任何 NDIS 函数，则它必须为该*FilterXxx*函数提供入口点。 例如，如果驱动程序调用[**NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)函数，则它必须提供[*FilterReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)函数。

如果筛选器驱动程序指定[*FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)函数并将发送请求排队，则它还必须指定[*FilterCancelSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_cancel_send_net_buffer_lists)函数。

如果筛选器驱动程序指定了[*FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_receive_net_buffer_lists)或[**FilterReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_return_net_buffer_lists)函数，则驱动程序还必须指定[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)函数。

若要在运行时更改其旁路模式设置，筛选器驱动程序可以调用[**NdisFRestartFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfrestartfilter)函数。 **NdisFRestartFilter**计划一个暂停操作，后跟指定筛选器模块的重新启动操作。 当 NDIS 调用*FilterSetModuleOptions*时，筛选器驱动程序可以通过调用**NdisSetOptionalHandlers**并指定新的入口点集来更改该筛选器模块的函数。

**请注意**，  暂停和重新启动可能会导致某些网络数据包被丢弃到传输路径或接收路径上，或同时丢弃这两者。 如果数据包丢失，则提供可靠传输机制的网络协议可能会重试网络 i/o 操作，但是其他不保证可靠性的协议不会重试该操作。

 

筛选器驱动程序可以注册支持可选的驱动程序服务的其他可选函数。 驱动程序在[*FilterSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数中注册这些可选服务。 有关这些可选服务的详细信息，请参阅[配置可选筛选器驱动程序服务](configuring-optional-filter-driver-services.md)。

 

 





