---
title: 初始化协议驱动程序
description: 初始化协议驱动程序
keywords:
- 协议驱动程序 WDK 网络，初始化
- NDIS 协议驱动程序 WDK，初始化
- 初始化协议驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e52d041c2de27405abb5203bfda564dc12f1a607
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803695"
---
# <a name="initializing-a-protocol-driver"></a>初始化协议驱动程序




系统将在加载驱动程序后调用协议驱动程序的 [DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程。 协议驱动程序作为系统服务加载。 它们可以在加载微型端口驱动程序之前、期间或之后的任何时间加载。

协议驱动程序在 **DriverEntry** 中分配驱动程序资源并注册 *ProtocolXxx* 函数。 这包括 CoNDIS 客户端和独立调用管理器。 若要使用 NDIS 注册其 *ProtocolXxx* 函数，协议驱动程序将调用 [NdisRegisterProtocolDriver](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver) 函数。

如果已成功注册为 NDIS 协议驱动程序的驱动程序， [DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)将返回 STATUS_SUCCESS 或其等效 NDIS_STATUS_SUCCESS。 如果 **DriverEntry** 通过传播 **NdisXxx** 函数返回的错误状态或内核模式支持例程来初始化失败，则不会保持加载该驱动程序。 **DriverEntry** 必须同步执行;也就是说，它不能返回 STATUS_PENDING 或其等效 NDIS_STATUS_PENDING。

NDIS 协议驱动程序的 [DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 函数必须调用 [NdisRegisterProtocolDriver](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver) 函数。 若要向 NDIS 库注册驱动程序的 *ProtocolXxx* 入口点，协议驱动程序将初始化 [**NDIS_PROTOCOL_DRIVER_CHARACTERISTICS**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_driver_characteristics) 结构并将其传递给 **NdisRegisterProtocolDriver**。

调用 NdisRegisterProtocolDriver 的驱动程序必须准备好对其任何 ProtocolXxx 函数的立即调用。

NDIS 协议驱动程序提供以下 *ProtocolXxx* 函数，它们是旧驱动程序提供的函数的更新版本：

[*ProtocolSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)

[*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)

[*ProtocolUnbindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)

[*ProtocolOpenAdapterCompleteEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_open_adapter_complete_ex)

[*ProtocolCloseAdapterCompleteEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_close_adapter_complete_ex)

[*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)

[*ProtocolUninstall*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_uninstall)

NDIS 协议驱动程序提供以下用于发送和接收操作的 *ProtocolXxx* 函数：

[**ProtocolReceiveNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_receive_net_buffer_lists)

[**ProtocolSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_send_net_buffer_lists_complete)

所有类型的 NDIS 协议驱动程序都应该注册功能齐全的 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex) 和 [*ProtocolUnbindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex) 函数，以支持即插即用 (PnP) 。 通常， [DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 函数应立即调用 [NdisRegisterProtocolDriver](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver) ，然后再返回 STATUS_SUCCESS 或 NDIS_STATUS_SUCCESS 状态值控制。

除了其 NDIS 定义的 *ProtocolXxx* 函数外，任何用于导出一组标准内核模式驱动程序例程的协议驱动程序都必须在传递到其 [DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 函数的给定驱动程序对象中设置这些驱动程序例程的入口点。 有关此类协议驱动程序的 **DriverEntry** 函数的功能的详细信息，请参阅 [编写 DriverEntry 例程](../kernel/writing-a-driverentry-routine.md)。

如果尝试分配驱动程序执行网络 i/o 操作所需的资源失败，则 [DriverEntry](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 应释放已分配的所有资源，然后再返回 STATUS_SUCCESS 或 NDIS_STATUS_SUCCESS 以外的状态控制。

如果在对 [NdisRegisterProtocolDriver](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)的成功调用之后发生错误，则在 **DriverEntry** 返回之前，驱动程序必须调用 [NdisDeregisterProtocolDriver](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisderegisterprotocoldriver)函数。

为了允许协议驱动程序配置可选服务，NDIS 在对 **NdisRegisterProtocolDriver** 的协议驱动程序调用的上下文中调用 *ProtocolSetOptions* 函数。 有关可选服务的详细信息，请参阅 [配置可选的协议驱动程序服务](configuring-optional-protocol-driver-services.md)。

CoNDIS 客户端驱动程序必须从 [*ProtocolSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用 [NdisSetOptionalHandlers](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数。 驱动程序初始化 [**NDIS_CO_CLIENT_OPTIONAL_HANDLERS**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_client_optional_handlers)结构并将其传递到 **NdisSetOptionalHandlers** 的 *OptionalHandlers* 参数。

CoNDIS 独立调用管理器还必须从 [*ProtocolSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用 [NdisSetOptionalHandlers](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数。 驱动程序初始化 [**NDIS_CO_CALL_MANAGER_OPTIONAL_HANDLERS**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构并将其传递到 **NdisSetOptionalHandlers** 的 *OptionalHandlers* 参数。

MCMs 不是协议驱动程序。 因此，它们必须从[MiniportSetOptions](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用[NdisSetOptionalHandlers](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数。 MCM 初始化 [**NDIS_CO_CALL_MANAGER_OPTIONAL_HANDLERS**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_co_call_manager_optional_handlers)结构，并将其传递到 **NdisSetOptionalHandlers** 的 *OptionalHandlers* 参数。

若要向 NDIS 注销，协议驱动程序会从其[卸载](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)例程调用[NdisDeregisterProtocolDriver](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisderegisterprotocoldriver) 。

若要在卸载协议驱动程序之前执行清理操作，协议驱动程序可以注册 [*ProtocolUninstall*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_uninstall) 函数。 *ProtocolUninstall* 函数是可选的。 例如，中间驱动程序的协议下边缘可能需要 *ProtocolUninstall* 函数。 中间驱动程序可以在 NDIS 调用其 [*MiniportDriverUnload*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload)函数之前，释放其在 *ProtocolUninstall* 中的协议边缘资源。

 

