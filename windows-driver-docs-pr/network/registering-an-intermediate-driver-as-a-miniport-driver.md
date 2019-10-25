---
title: 将中间驱动程序注册为微型端口驱动程序
description: 将中间驱动程序注册为微型端口驱动程序
ms.assetid: a01bc0f4-4a03-4d44-88c0-7029042d6953
keywords:
- 注册中间驱动程序
- 中间驱动程序 WDK 网络，注册
- NDIS 中间驱动程序 WDK，注册
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bcd14daa235809e21b47446e4279c68b8a23708
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842109"
---
# <a name="registering-an-intermediate-driver-as-a-miniport-driver"></a>将中间驱动程序注册为微型端口驱动程序





中间驱动程序调用[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)来导出其*MiniportXxx*函数。 当驱动程序调用[**NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)时， **NdisMRegisterMiniportDriver**返回的*NdisMiniportDriverHandle*必须由中间驱动程序和到 NDIS 的输入保留。

中间驱动程序必须：

1.  使用[**NdisZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiszeromemory)将[**NDIS\_微型端口\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构的零初始化。

2.  存储必需的*MiniportXxx*函数的地址，以及驱动程序导出的任何可选*MiniportXxx*函数。

支持 NDIS 6.0 功能的中间驱动程序必须注册为版本6.0 微型端口驱动程序。 有关指定微型端口驱动程序版本号的详细信息，请参阅[**NDIS\_微型端口\_驱动程序\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)。

必须将*MiniportCharacteristics*中的以下条目设置为有效的*MiniportXxx*函数地址，除非该函数是可选的且不会导出。 如果驱动程序没有导出函数，请将地址设置为**NULL**。

<a href="" id="setoptionshandler"></a>**SetOptionsHandler**  
[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)是一个可选函数。 NDIS 调用*MiniportSetOptions* ，以便中间驱动程序可以指定可选的处理程序。

<a href="" id="initializehandlerex"></a>**InitializeHandlerEx**  
由于中间驱动程序调用**NdisIMInitializeDeviceInstanceEx**来初始化其要初始化的虚拟小型端口适配器操作，因此 NDIS 调用[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 。

<a href="" id="halthandlerex"></a>**HaltHandlerEx**  
[*MiniportHaltEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)是必需的函数。 如果启动了中间驱动程序公开的或停止了中间驱动程序，或中间驱动程序调用[**NdisIMDeInitializeDeviceInstance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimdeinitializedeviceinstance)来启动删除，NDIS 将调用*MiniportHaltEx* 。

<a href="" id="unloadhandler"></a>**UnloadHandler**  
[*MiniportDriverUnload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload)是必需的函数。 NDIS 调用*MiniportDriverUnload*来卸载中间驱动程序。

<a href="" id="pausehandler"></a>**PauseHandler**  
[*MiniportPause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)是必需的函数。 NDIS 通过中间驱动程序的指定虚拟小型端口调用*MiniportPause*来停止网络数据流。

<a href="" id="restarthandler"></a>**RestartHandler**  
[**MiniportRestart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)是必需的函数。 NDIS 通过中间驱动程序的指定虚拟小型端口调用*MiniportRestart*来重新启动网络数据流。

<a href="" id="oidrequesthandler"></a>**OidRequestHandler**  
[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)从已调用[**NdisOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisoidrequest)的过量驱动程序或从 NDIS 接收*源自请求的*OID\_。 中间驱动程序可以处理请求，或将其传递给基础微型端口驱动程序。

<a href="" id="sendnetbufferlistshandler"></a>**SendNetBufferListsHandler**  
[*MiniportSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)接收到网络[ **\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的一个或多个指针的数组，该数组指定用于通过网络传输的网络数据。 每个中间驱动程序应提供*MiniportSendNetBufferLists*函数。 有关详细信息，请参阅[通过中间驱动程序传输网络数据](transmitting-network-data-through-an-intermediate-driver.md)。

<a href="" id="returnnetbufferlistshandler"></a>**ReturnNetBufferListsHandler**  
[*MiniportReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_return_net_buffer_lists)通过调用**NdisMIndicateReceiveNetBufferLists**，接收返回的已返回的[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构，该结构之前指定给更高级别的驱动程序。 对**NdisMIndicateReceiveNetBufferLists**让给的调用可控制向更高级别的驱动程序指示的资源。 当高级驱动程序使用每个指示时，中间驱动程序分配的 NET\_缓冲区\_列表结构及其描述的资源将返回到*MiniportReturnNetBufferLists*函数。

<a href="" id="cancelsendhandler"></a>**CancelSendHandler**  
[*MiniportCancelSend*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_send)是必需的函数。 NDIS 调用*MiniportCancelSend*来取消发送请求。

<a href="" id="checkforhanghandler"></a>**CheckForHangHandler**  
中间驱动程序不需要[*MiniportCheckForHangEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_check_for_hang) ，因此应将此入口点设置为**NULL**。

<a href="" id="resethandlerex"></a>**ResetHandlerEx**  
中间驱动程序不需要[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset) ，因此应将此入口点设置为**NULL**。

<a href="" id="devicepnpeventnotifyhandler"></a>**DevicePnPEventNotifyHandler**  
[*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)函数的入口点。

<a href="" id="shutdownhandlerex"></a>**ShutdownHandlerEx**  
[*MiniportShutdownEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)是必需的函数。 *MiniportShutdownEx*会将虚拟微型端口还原为其初始状态（在中间驱动程序的**DriverEntry**例程运行之前）。

<a href="" id="canceloidrequesthandler"></a>**CancelOidRequestHandler**  
[*MiniportCancelOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_cancel_oid_request)是必需的函数。 NDIS 调用*MiniportCancelOidRequest*来取消 OID 请求。

中间驱动程序可能需要其他特定于实现的*MiniportXxx*函数。 有关注册可选的信息，请参阅[配置可选微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)。

某些微型端口驱动程序处理程序函数永远不会由中间驱动程序提供。 出现这种情况的原因包括：此类驱动程序不管理中断的设备，或此类驱动程序在引发的 IRQL 时不分配缓冲区。

**请注意**  中间驱动程序必须包括暂停和重新启动功能。 如果需要，在 NDIS 暂停基础驱动程序堆栈时，支持暂停和重新启动虚拟微型端口。 有关暂停和重新启动的详细信息，请参阅[驱动程序堆栈管理](driver-stack-management.md)。

 

 

 





