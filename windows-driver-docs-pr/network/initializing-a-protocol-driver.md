---
title: 初始化协议驱动程序
description: 初始化协议驱动程序
ms.assetid: 1479d59b-7c8b-495b-86c7-72f1b7e334e4
keywords:
- 协议驱动程序 WDK 连接网络、 初始化
- NDIS 协议驱动程序 WDK，初始化
- 初始化协议驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00b8f2e89a68464950cb87bf9e13ad1a54a390d6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381323"
---
# <a name="initializing-a-protocol-driver"></a>初始化协议驱动程序




系统调用协议驱动程序[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程后它会加载该驱动程序。 协议驱动程序加载为系统服务。 它们可以加载在任何时间之前、 期间或之后的微型端口驱动程序加载。

协议驱动程序分配驱动程序资源和注册*ProtocolXxx*中的函数**DriverEntry**。 这包括的 CoNDIS 客户端和独立调用管理器。 若要注册其*ProtocolXxx* NDIS 函数，协议驱动程序调用[NdisRegisterProtocolDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)函数。

[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)返回 STATUS_SUCCESS 或其等效的 NDIS_STATUS_SUCCESS，如果该驱动程序已成功注册为 NDIS 协议驱动程序。 如果**DriverEntry**传播由返回的错误状态将失败并初始化**NdisXxx**函数或通过内核模式下支持例程，该驱动程序将不继续加载。 **DriverEntry**必须执行同步; 即，它不能返回 STATUS_PENDING 或其等效 NDIS_STATUS_PENDING。

[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize) NDIS 协议驱动程序函数必须调用[NdisRegisterProtocolDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)函数。 若要注册的驱动程序*ProtocolXxx* NDIS 库使用的入口点，协议驱动程序初始化[ **NDIS_PROTOCOL_DRIVER_CHARACTERISTICS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_driver_characteristics)结构和将其传递给**NdisRegisterProtocolDriver**。

调用 NdisRegisterProtocolDriver 的驱动程序必须做好对任何其 ProtocolXxx 函数的直接调用。

协议的 NDIS 驱动程序提供以下*ProtocolXxx*函数，它们是旧驱动程序提供的函数的更新的版本：

[*ProtocolSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)

[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)

[*ProtocolUnbindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)

[*ProtocolOpenAdapterCompleteEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_open_adapter_complete_ex)

[*ProtocolCloseAdapterCompleteEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_close_adapter_complete_ex)

[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)

[*ProtocolUninstall*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_uninstall)

协议的 NDIS 驱动程序提供以下*ProtocolXxx*函数发送和接收操作：

[**ProtocolReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_receive_net_buffer_lists)

[**ProtocolSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)

所有类型的协议的 NDIS 驱动程序应都注册完备[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)并[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)函数来支持插即用 (PnP)。 一般情况下， [DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)函数应调用[NdisRegisterProtocolDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)立即之前它将返回 STATUS_SUCCESS 或 NDIS_STATUS_SUCCESS 将 status 值的控件。

将导出的一组标准的内核模式驱动程序例程，除了其 NDIS 定义任何协议驱动程序*ProtocolXxx*函数必须传递到给定的驱动程序对象中设置这些驱动程序例程的入口点其[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)函数。 有关功能的这样的协议驱动程序的详细信息**DriverEntry**函数中，请参阅[编写 DriverEntry 例程](../kernel/writing-a-driverentry-routine.md)。

如果尝试将驱动程序执行网络 I/O 操作失败，所需的资源分配[DriverEntry](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)应释放所有资源已分配之前它将返回具有的状态不是 STATUS_ 控件成功或 NDIS_STATUS_SUCCESS。

如果在成功调用后出现错误[NdisRegisterProtocolDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisregisterprotocoldriver)，该驱动程序必须调用[NdisDeregisterProtocolDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisderegisterprotocoldriver)函数之前**DriverEntry**返回。

若要允许协议驱动程序以配置可选服务，NDIS 调用*ProtocolSetOptions*协议驱动程序的调用的上下文中的函数**NdisRegisterProtocolDriver**。 可选的服务的详细信息，请参阅[配置可选协议驱动程序服务](configuring-optional-protocol-driver-services.md)。

CoNDIS 客户端驱动程序必须调用[NdisSetOptionalHandlers](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数从[ *ProtocolSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数。 该驱动程序初始化[ **NDIS_CO_CLIENT_OPTIONAL_HANDLERS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_client_optional_handlers)结构，并将其在传递*OptionalHandlers*参数**NdisSetOptionalHandlers**。

此外必须调用独立调用管理器的 CoNDIS [NdisSetOptionalHandlers](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数从[ *ProtocolSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数。 该驱动程序初始化[ **NDIS_CO_CALL_MANAGER_OPTIONAL_HANDLERS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构，并将其在传递*OptionalHandlers*参数**NdisSetOptionalHandlers**。

MCMs 不是协议驱动程序。 因此，它们必须调用[NdisSetOptionalHandlers](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数从[MiniportSetOptions](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数。 初始化 MCM [ **NDIS_CO_CALL_MANAGER_OPTIONAL_HANDLERS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构，并将其在传递*OptionalHandlers*参数**NdisSetOptionalHandlers**。

NDIS 中注销，协议驱动程序调用[NdisDeregisterProtocolDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisderegisterprotocoldriver)从其[卸载](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程。

若要卸载协议驱动程序之前，请执行清理操作，协议驱动程序可以注册[ *ProtocolUninstall* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_uninstall)函数。 *ProtocolUninstall*函数是可选的。 例如，可能需要中间驱动程序的协议下边缘*ProtocolUninstall*函数。 中间驱动程序可以释放在其协议边缘资源*ProtocolUninstall* NDIS 调用前其[ *MiniportDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_unload)函数。

 

 





