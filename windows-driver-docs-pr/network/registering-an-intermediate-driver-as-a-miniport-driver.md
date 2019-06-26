---
title: 将中间驱动程序注册为微型端口驱动程序
description: 将中间驱动程序注册为微型端口驱动程序
ms.assetid: a01bc0f4-4a03-4d44-88c0-7029042d6953
keywords:
- 注册中间驱动程序
- 驱动程序 WDK 的中间连接网络、 注册
- NDIS 中间层驱动程序 WDK，注册
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95393d5e1858ac892b38a77a51f5eb51a510117a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374781"
---
# <a name="registering-an-intermediate-driver-as-a-miniport-driver"></a>将中间驱动程序注册为微型端口驱动程序





中间的驱动程序调用[ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)若要导出其*MiniportXxx*函数。 *NdisMiniportDriverHandle*返回的**NdisMRegisterMiniportDriver**必须保留中间驱动程序和驱动程序调用时输入到 NDIS [ **NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiminitializedeviceinstanceex)。

中间驱动程序必须：

1.  零初始化[ **NDIS\_微型端口\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构[ **NdisZeroMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiszeromemory).

2.  存储的地址，则为强制*MiniportXxx*函数，为以及任何可选*MiniportXxx*驱动程序将导出的函数。

支持 NDIS 6.0 功能的中间驱动程序必须将注册为版本 6.0 的微型端口驱动程序。 有关指定微型端口驱动程序的版本号的详细信息，请参阅[ **NDIS\_微型端口\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)。

您必须在设置了以下项*MiniportCharacteristics*为有效*MiniportXxx*函数地址，除非该函数是可选的不会导出。 如果该驱动程序不会导出函数，将地址设置为**NULL**。

<a href="" id="setoptionshandler"></a>**SetOptionsHandler**  
[*MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)是一个可选函数。 NDIS 调用*MiniportSetOptions*因此中间驱动程序可以指定可选的处理程序。

<a href="" id="initializehandlerex"></a>**InitializeHandlerEx**  
NDIS 调用[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)中间驱动程序调用**NdisIMInitializeDeviceInstanceEx**来初始化其微型端口适配器正在初始化虚拟微型端口的操作。

<a href="" id="halthandlerex"></a>**HaltHandlerEx**  
[*MiniportHaltEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_halt)是所需的函数。 NDIS 调用*MiniportHaltEx*如果禁用或停止，中间驱动程序公开的虚拟微型端口设备或中间驱动程序调用[ **NdisIMDeInitializeDeviceInstance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisimdeinitializedeviceinstance)启动它被删除。

<a href="" id="unloadhandler"></a>**UnloadHandler**  
[*MiniportDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_unload)是所需的函数。 NDIS 调用*MiniportDriverUnload*卸载中间驱动程序。

<a href="" id="pausehandler"></a>**PauseHandler**  
[*MiniportPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause)是所需的函数。 NDIS 调用*MiniportPause*停止通过中间驱动程序指定虚拟微型端口的网络数据流。

<a href="" id="restarthandler"></a>**RestartHandler**  
[**MiniportRestart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_restart)是所需的函数。 NDIS 调用*MiniportRestart*重启通过中间驱动程序指定虚拟微型端口的网络数据流。

<a href="" id="oidrequesthandler"></a>**OidRequestHandler**  
[*MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)接收 OID\_*XXX*从调用了一个基础驱动程序发出的请求[ **NdisOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisoidrequest)或从 NDIS。 中间驱动程序可能处理请求，或将其传递到基础微型端口驱动程序。

<a href="" id="sendnetbufferlistshandler"></a>**SendNetBufferListsHandler**  
[*MiniportSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_send_net_buffer_lists)接收到一个或多个指针的数组[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)指定网络的结构用于通过网络传输的数据。 每个中间驱动程序应提供*MiniportSendNetBufferLists*函数。 有关详细信息，请参阅[传输网络数据通过中间驱动程序](transmitting-network-data-through-an-intermediate-driver.md)。

<a href="" id="returnnetbufferlistshandler"></a>**ReturnNetBufferListsHandler**  
[*MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)接收返回[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)以前指定给的结构更高级别的驱动程序通过调用**NdisMIndicateReceiveNetBufferLists**。 在调用**NdisMIndicateReceiveNetBufferLists**放弃控制到更高级别的驱动程序指定的资源。 中间驱动程序的更高级别的驱动程序使用每个指示后，分配 NET\_缓冲区\_列表结构以及它所描述的资源返回到*MiniportReturnNetBufferLists*函数。

<a href="" id="cancelsendhandler"></a>**CancelSendHandler**  
[*MiniportCancelSend* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_send)是所需的函数。 NDIS 调用*MiniportCancelSend*取消发送请求。

<a href="" id="checkforhanghandler"></a>**CheckForHangHandler**  
[*MiniportCheckForHangEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_check_for_hang)不是必需的中间驱动程序，因此它们应将此入口点设置为**NULL**。

<a href="" id="resethandlerex"></a>**ResetHandlerEx**  
[*MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)不是必需的中间驱动程序，因此它们应将此入口点设置为**NULL**。

<a href="" id="devicepnpeventnotifyhandler"></a>**DevicePnPEventNotifyHandler**  
入口点[ *MiniportDevicePnPEventNotify* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_device_pnp_event_notify)函数。

<a href="" id="shutdownhandlerex"></a>**ShutdownHandlerEx**  
[*MiniportShutdownEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_shutdown)是所需的函数。 *MiniportShutdownEx*将虚拟微型端口还原到其初始状态 (中间的驱动程序之前**DriverEntry**日常运行)。

<a href="" id="canceloidrequesthandler"></a>**CancelOidRequestHandler**  
[*MiniportCancelOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_cancel_oid_request)是所需的函数。 NDIS 调用*MiniportCancelOidRequest*取消 OID 请求。

中间的驱动程序可能需要其他*MiniportXxx*都特定于实现的函数。 有关注册可选信息，请参阅[配置可选的微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)。

由中间驱动程序永远不会提供某些微型端口驱动程序处理程序函数。 其中的原因包括： 此类驱动程序不管理中断的设备，或此类驱动程序不分配引发 IRQL 中的缓冲区。

**请注意**  中间驱动程序必须包括暂停和重新启动功能。 包括支持暂停和重新启动的虚拟微型端口时，根据需要 NDIS 暂停基础的驱动程序堆栈。 有关暂停和重新启动的详细信息，请参阅[驱动程序堆栈管理](driver-stack-management.md)。

 

 

 





