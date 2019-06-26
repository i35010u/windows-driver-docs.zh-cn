---
title: 无线显示 WDDM 显示微型端口驱动程序支持
description: 若要支持的 Miracast 无线显示，Windows 显示驱动程序模型 (WDDM) 显示在内核模式下运行的微型端口驱动程序需要执行以下任务。
ms.assetid: D67CAC4F-0409-4E8D-A31A-78C3EB473556
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: ba4383daec6b83061541b323b378541c64b9433d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376121"
---
# <a name="wddm-display-miniport-driver-tasks-to-support-miracast-wireless-displays"></a>用于支持 Miracast 无线显示的 WDDM 显示微型端口驱动程序任务


若要支持的 Miracast 无线显示，Windows 显示驱动程序模型 (WDDM) 显示在内核模式下运行的微型端口驱动程序需要执行以下任务。

## <a name="supporting-the-miracast-interface"></a>支持 Miracast 接口


如果显示微型端口驱动程序支持 Miracast 的显示器，必须将错误报告[ **DXGK\_MIRACAST\_显示\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_miracast_interface)结构，它具有指针驱动程序实现 Miracast 函数，当调用 Microsoft DirectX 图形内核子系统[ *DxgkDdiQueryInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)函数。

如果操作系统的 DirectX 图形内核子系统 (Dxgkrnl.sys) 不会调用[ *DxgkDdiQueryInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)函数查询 Miracast 显示界面，则它不支持Miracast 无线显示器和显示微型端口驱动程序不应报告任何 Miracast 目标。

该驱动程序不应该完全 WDDM 图形在任何设备上，否则为操作系统无法启动适配器报告多个 Miracast 目标。

Dxgkrnl 调用后[ *DxgkDdiQueryInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)若要查询的 Miracast 显示接口，该驱动程序可以然后报告形式的目标类型**D3DKMDT\_VOT\_MIRACAST**在设备初始化时 Dxgkrnl 调用期间[ *DxgkDdiQueryChildRelations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)函数。

Miracast 目标应保留在断开连接状态直到 Dxgkrnl 启动 Miracast 连接会话。 当 Miracast 会话从开始，和显示器连接到支持 Miracast 接收器或驱动程序从 Miracast 用户模式驱动程序接收的 I/O 请求，因为新的监视器已连接到支持 Miracast 接收器时，显示微型端口驱动程序应报告监视器到达热插拔检测 (HPD) 感知值到通过调用操作系统[ **DxgkCbIndicateChildStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_indicate_child_status)函数。 在此调用驱动程序应设置这些值：

| [**DXGK\_子\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_child_status)成员 | 值                                                                                                                                                                                                                                                                      |
|-------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Type**                                                    | **StatusMiracast**常数值[ **DXGK\_子\_状态\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ne-dispmprt-_dxgk_child_status_type)枚举                                                                                                                                                       |
| **Miracast**。**连接**                                  | **TRUE**                                                                                                                                                                                                                                                                   |
| **Miracast**.**MiracastMonitorType**                        | 值，该值指示连接类型。 如果 Miracast 接收器嵌入在监视器或电视，这应设置为**D3DKMDT\_VOT\_MIRACAST**常量值[ **D3DKMDT\_视频\_输出\_技术**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology)枚举。 |

 

以下是显示微型端口驱动程序实现的 Miracast 函数：

<span id="DxgkDdiMiracastCreateContext"></span><span id="dxgkddimiracastcreatecontext"></span><span id="DXGKDDIMIRACASTCREATECONTEXT"></span>[*DxgkDdiMiracastCreateContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_create_context)  
创建用于启动 Miracast 显示设备的内核模式实例的上下文。

<span id="DxgkDdiMiracastDestroyContext"></span><span id="dxgkddimiracastdestroycontext"></span><span id="DXGKDDIMIRACASTDESTROYCONTEXT"></span>[*DxgkDdiMiracastDestroyContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_destroy_context)  
创建用于启动 Miracast 显示设备的内核模式实例的上下文。

<span id="DxgkDdiMiracastIoControl"></span><span id="dxgkddimiracastiocontrol"></span><span id="DXGKDDIMIRACASTIOCONTROL"></span>[*DxgkDdiMiracastIoControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_handle_io_control)  
处理源自 Miracast 用户模式驱动程序调用的同步 I/O 请求[ **MiracastIoControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_miracast_io_control)。

<span id="DxgkDdiMiracastQueryCaps"></span><span id="dxgkddimiracastquerycaps"></span><span id="DXGKDDIMIRACASTQUERYCAPS"></span>[*DxgkDdiMiracastQueryCaps*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_query_caps)  
查询当前的显示适配器的 Miracast 功能。

## <a name="span-idmiracastsessionstartspanspan-idmiracastsessionstartspanspan-idmiracastsessionstartspanmiracast-session-start"></a><span id="Miracast_session_start"></span><span id="miracast_session_start"></span><span id="MIRACAST_SESSION_START"></span>Miracast 会话开始


启动 Miracast 会话后，操作系统将调用[ *DxgkDdiQueryChildStatus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_child_status)函数。 显示微型端口驱动程序应设置[ **DXGK\_子\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_child_status)。**类型**为值**StatusMiracast** ，并应使用**Miracast**中的子结构**DXGK\_子\_状态**. 如果监视器已连接到支持 Miracast 接收器，该驱动程序应设置**Miracast**。**连接**到**D3DKMDT\_VOT\_MIRACAST**。

该驱动程序必须指定的值[ **D3DKMDT\_视频\_信号\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info)。**VsyncFreqDivider**，即显示通过 Miracast 的显示器的垂直同步速率比连接到支持 Miracast 接收器的 VSync 速率会话。 例如，如果连接显示的 VSync 中断频率为 30 Hz Miracast 接收器垂直刷新率是 240 Hz，驱动程序应设置**VsyncFreqDivider**为 8。

## <a name="span-idhandlinginterruptsforcompletedencodechunksspanspan-idhandlinginterruptsforcompletedencodechunksspanspan-idhandlinginterruptsforcompletedencodechunksspanhandling-interrupts-for-completed-encode-chunks"></a><span id="Handling_interrupts_for_completed_encode_chunks"></span><span id="handling_interrupts_for_completed_encode_chunks"></span><span id="HANDLING_INTERRUPTS_FOR_COMPLETED_ENCODE_CHUNKS"></span>已完成处理中断对区块进行编码


单个框架通过无线 Miracast 连接传输的数据可以分解为一个或更多编码区块。 GPU 完成编码一个这些区块，每次它必须生成中断。 在此中断响应，显示微型端口驱动程序必须调用[ *DxgkCbNotifyInterrupt* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_interrupt)函数，并完成**MiracastEncodeChunkCompleted**子结构中[ **DXGKARGCB\_通知\_中断\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkargcb_notify_interrupt_data)结构，其中包括设置[ **DXGK\_中断\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_interrupt_type)中断类型设置为**DXGK\_中断\_MICACAST\_块区\_处理\_完成**。

中断处理的一部分，可以选择指定驱动程序**MiracastEncodeChunkCompleted**。**pPrivateDriverData**并**PrivateDataDriverSize**中的成员[ **DXGKARGCB\_通知\_中断\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkargcb_notify_interrupt_data)结构。 用户模式驱动程序可以访问此专用驱动程序数据[ **MIRACAST\_区块\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_chunk_data)。**PrivateDriverData**成员。

如果一段时间，显示微型端口驱动程序会生成比区块数据的更多数据包用户模式显示驱动程序会占用，则新区块的可用内存空间可以用完。在这种情况下显示微型端口驱动程序返回**状态\_否\_内存**中**MiracastEncodeChunkCompleted**。**状态**，并且它必须调用[ *DxgkCbNotifyDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_dpc)函数，以通知有关错误条件的操作系统的 GPU 计划程序。 调用[ **GetNextChunkData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)函数将返回**状态\_连接\_重置**状态代码和后续调用将开始接收后重置操作已提交的块。 因为某些区块将已丢失，我们建议的驱动程序生成和传输中的新我的框架。

## <a name="span-idrestrictionsonsourcemodesspanspan-idrestrictionsonsourcemodesspanspan-idrestrictionsonsourcemodesspanrestrictions-on-source-modes"></a><span id="Restrictions_on_source_modes"></span><span id="restrictions_on_source_modes"></span><span id="RESTRICTIONS_ON_SOURCE_MODES"></span>对源模式的限制


WDDM 显示微型端口驱动程序，以处理约束像素管道中，通常会公开源模式限制对操作系统。 该驱动程序执行此操作通过仅填充的源模式的使用模式公开的像素管道还支持的监视器列表。 例如，驱动程序不会修改基于像素管道约束 EDID。

同样，Miracast 的显示器的显示微型端口驱动程序会限制公开的源模式的一对操作系统时枚举的源和目标模式集。 Miracast 显示 GPU 编码功能，网络属性和接收器解码的功能可以减少 Miracast 像素管道可以支持的源模式的数量。

如果显示微型端口驱动程序调用[ *DXGK\_VIDPNSOURCEMODESET\_INTERFACE::pfnAddMode* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_addmode)函数尝试将三维立体声模式添加到已连接到源Miracast 目标函数调用将失败。

## <a name="span-idcallingoperatingsystem-providedcallbackfunctionsspanspan-idcallingoperatingsystem-providedcallbackfunctionsspanspan-idcallingoperatingsystem-providedcallbackfunctionsspancalling-operating-system-provided-callback-functions"></a><span id="Calling_operating_system-provided_callback_functions"></span><span id="calling_operating_system-provided_callback_functions"></span><span id="CALLING_OPERATING_SYSTEM-PROVIDED_CALLBACK_FUNCTIONS"></span>调用操作系统所提供的回调函数


它们是操作系统提供的 Miracast 内核模式回调函数：

<span id="DxgkCbMiracastSendMessage"></span><span id="dxgkcbmiracastsendmessage"></span><span id="DXGKCBMIRACASTSENDMESSAGE"></span>[**DxgkCbMiracastSendMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)  
将异步消息发送到用户模式显示驱动程序。

<span id="DxgkCbMiracastSendMessageCallback"></span><span id="dxgkcbmiracastsendmessagecallback"></span><span id="DXGKCBMIRACASTSENDMESSAGECALLBACK"></span>[**DxgkCbMiracastSendMessageCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)  
对调用中使用[ **DxgkCbMiracastSendMessage** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)若要指定[ **IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)已完成的 IRP 的结构。

<span id="DxgkCbReportChunkInfo"></span><span id="dxgkcbreportchunkinfo"></span><span id="DXGKCBREPORTCHUNKINFO"></span>[**DxgkCbReportChunkInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_report_chunk_info)  
有关编码区块报告信息。

## <a name="span-idsendingmessagesasynchronouslyfromkernel-modetouser-modespanspan-idsendingmessagesasynchronouslyfromkernel-modetouser-modespanspan-idsendingmessagesasynchronouslyfromkernel-modetouser-modespansending-messages-asynchronously-from-kernel-mode-to-user-mode"></a><span id="Sending_messages_asynchronously_from_kernel-mode_to_user-mode"></span><span id="sending_messages_asynchronously_from_kernel-mode_to_user-mode"></span><span id="SENDING_MESSAGES_ASYNCHRONOUSLY_FROM_KERNEL-MODE_TO_USER-MODE"></span>从内核模式以异步方式发送消息，为用户模式


调用时，显示微型端口驱动程序将发送到其关联的用户模式驱动程序的任何消息[ *DxgkCbMiracastSendMessage* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message) Miracast 连接会话之前不会传递函数已开始。 因此，如果在用户模式驱动程序[ *StartMiracastSession* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_start_miracast_session)尚未调用函数，将延迟发送的消息，直到*StartMiracastSession*返回。 如果消息发送后[ *StopMiracastSession* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_stop_miracast_session)调用函数，然后由操作系统中，会丢弃该消息并[ *DxgkCbMiracastSendMessageCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)函数调用中设置的错误状态*pIoStatusBlock*-&gt;**状态**.

## <a name="span-idmodifyinganexistingdisplayminiportdrivertosupportmiracastdisplaysspanspan-idmodifyinganexistingdisplayminiportdrivertosupportmiracastdisplaysspanspan-idmodifyinganexistingdisplayminiportdrivertosupportmiracastdisplaysspanmodifying-an-existing-display-miniport-driver-to-support-miracast-displays"></a><span id="Modifying_an_existing_display_miniport_driver_to_support_Miracast_displays"></span><span id="modifying_an_existing_display_miniport_driver_to_support_miracast_displays"></span><span id="MODIFYING_AN_EXISTING_DISPLAY_MINIPORT_DRIVER_TO_SUPPORT_MIRACAST_DISPLAYS"></span>修改现有显示微型端口驱动程序以支持 Miracast 的显示器


当[ *DxgkDdiStartDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_start_device)函数被调用时，显示微型端口驱动程序应具有可添加新的 Miracast 目标，应将标记目标的热插拔检测 (HPD) 感知值作为**HpdAwarenessInterruptible** ，以便操作系统不会轮询此目标。 此外，当[ *DxgkDdiQueryChildRelations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_child_relations)调用函数时，该驱动程序应报告**D3DKMDT\_VOT\_MIRACAST**为其连接类型。

驱动程序应报告任何完全 WDDM 图形设备上的多个 Miracast 目标。 如果驱动程序报告多个 Miracast 目标，操作系统将失败的适配器启动。 驱动程序应还未报告任何监视器在此目标中，如果 Miracast 连接会话未启动。

该驱动程序还需要报告的正确[ **DXGK\_MIRACAST\_显示\_接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_miracast_interface)结构，其中的内核模式中的函数的指针地址空间，当调用 DirectX 图形内核子系统[ *DxgkDdiQueryInterface* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)函数。

当 Miracast 会话正在启动，并且连接监视器显示微型端口驱动程序应设置 Miracast 接收器[ **DXGK\_子\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_child_status)。**类型**成员添加到**StatusMiracast**常量值，并且还应设置**DXGK\_子\_状态**。**Miracast**。**连接**到**TRUE**、 向操作系统报告监视器到达 HPD。 该驱动程序应设置**DXGK\_子\_状态**。**Miracast**。**MiracastMonitorType**成员添加到已连接到接收器的正确的监视器类型。 如果接收器是监视器的一部分，此成员应设置为**D3DKMDT\_VOT\_MIRACAST**。

如果驱动程序知道监视器 EDID，操作系统将调用时，它应报告此 EDID [ *DxgkDdiQueryDeviceDescriptor* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_device_descriptor)函数。

具体取决于硬件功能、 Miracast 接收器模式列表，以及网络带宽，该驱动程序应报告正确的源模式、 目标模式、 旋转模式和缩放模式。 对于目标模式中，驱动程序应报告正确**VSyncFreqDivider**中的成员值[ **D3DKMDT\_视频\_信号\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info). 操作系统匹配监视模式下针对的目标模式，并会清理此监视器不支持任何模式。

 

 





