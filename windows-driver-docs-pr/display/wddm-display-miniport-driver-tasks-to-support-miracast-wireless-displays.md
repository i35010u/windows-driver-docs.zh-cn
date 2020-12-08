---
title: 用于无线显示的 WDDM 显示微型端口驱动程序支持
description: 为了支持 Miracast 无线显示，Windows 显示驱动程序模型 (WDDM) 显示以内核模式运行的微型端口驱动程序需要执行以下任务。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 672406197eb292b6e515e42d22cfbcee0761502b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793823"
---
# <a name="wddm-display-miniport-driver-tasks-to-support-miracast-wireless-displays"></a>用于支持 Miracast 无线显示的 WDDM 显示微型端口驱动程序任务

> [!NOTE]
> 在 Windows 10 中，操作系统包含 Miracast 无线显示器的本机实现。 驱动程序不应再实现自定义的 Miracast 显示组件。 在 Windows 的未来版本中，可能会删除对自定义 Miracast 实现的支持。

为了支持 Miracast 无线显示，Windows 显示驱动程序模型 (WDDM) 显示以内核模式运行的微型端口驱动程序需要执行以下任务。

## <a name="supporting-the-miracast-interface"></a>支持 Miracast 接口


如果显示微型端口驱动程序支持 Miracast 显示，则在 Microsoft DirectX 图形内核子系统调用 [*DxgkDdiQueryInterface*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)函数时，它必须报告 [**DXGK \_ miracast \_ 显示 \_ 接口**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_miracast_interface)结构，该结构包含指向驱动程序实现的 Miracast 函数的指针。

如果操作系统的 DirectX 图形内核子系统 ( # A0) 不会调用 [*DxgkDdiQueryInterface*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface) 函数来查询 miracast 显示界面，则它不支持 miracast 无线显示，并且显示微型端口驱动程序不应报告任何 miracast 目标。

驱动程序不应在任何完整的 WDDM 图形设备上报告多个 Miracast 目标，否则操作系统无法启动适配器。

在 Dxgkrnl 调用 [*DxgkDdiQueryInterface*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface) 以查询 Miracast 显示界面之后，驱动程序可以在设备初始化期间将目标类型报告为 **D3DKMDT \_ VOT \_ Miracast** ，Dxgkrnl 调用 [*DxgkDdiQueryChildRelations*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_relations) 函数。

在 Dxgkrnl 启动 Miracast 连接的会话之前，Miracast 目标应保持断开连接状态。 当 Miracast 会话正在启动，并且监视器连接到 miracast 接收器或驱动程序收到来自 Miracast 用户模式驱动程序的 i/o 请求，因为新的监视器已连接到 Miracast 接收器，所以，显示微型端口驱动程序应该通过调用 [**DxgkCbIndicateChildStatus**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_indicate_child_status) 函数向操作系统报告监视到达热插拔检测 (HPD) 感知值。 在此调用中，驱动程序应设置以下值：

| [**DXGK \_子 \_ 状态**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_child_status) 成员 | “值”                                                                                                                                                                                                                                                                      |
|-------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **类型**                                                    | [**DXGK \_ 子 \_ 状态 \_ 类型**](/windows-hardware/drivers/ddi/dispmprt/ne-dispmprt-_dxgk_child_status_type)枚举的 **StatusMiracast** 常数值                                                                                                                                                       |
| **Miracast**。**已连接**                                  | **TRUE**                                                                                                                                                                                                                                                                   |
| **Miracast**。**MiracastMonitorType**                        | 指示连接类型的值。 如果在监视器或电视中嵌入了 Miracast 接收器，则应将其设置为 [**D3DKMDT \_ 视频 \_ 输出 \_ 技术**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology)枚举的 **D3DKMDT \_ VOT \_ Miracast** 常量值。 |

 

这些是显示微型端口驱动程序实现的 Miracast 函数：

<span id="DxgkDdiMiracastCreateContext"></span><span id="dxgkddimiracastcreatecontext"></span><span id="DXGKDDIMIRACASTCREATECONTEXT"></span>[*DxgkDdiMiracastCreateContext*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_create_context)  
创建上下文以启动 Miracast 显示设备的内核模式实例。

<span id="DxgkDdiMiracastDestroyContext"></span><span id="dxgkddimiracastdestroycontext"></span><span id="DXGKDDIMIRACASTDESTROYCONTEXT"></span>[*DxgkDdiMiracastDestroyContext*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_destroy_context)  
创建上下文以启动 Miracast 显示设备的内核模式实例。

<span id="DxgkDdiMiracastIoControl"></span><span id="dxgkddimiracastiocontrol"></span><span id="DXGKDDIMIRACASTIOCONTROL"></span>[*DxgkDdiMiracastIoControl*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_handle_io_control)  
处理从 Miracast 用户模式驱动程序调用到 [**MiracastIoControl**](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_miracast_io_control)的同步 i/o 请求。

<span id="DxgkDdiMiracastQueryCaps"></span><span id="dxgkddimiracastquerycaps"></span><span id="DXGKDDIMIRACASTQUERYCAPS"></span>[*DxgkDdiMiracastQueryCaps*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_query_caps)  
查询当前显示适配器的 Miracast 功能。

## <a name="span-idmiracast_session_startspanspan-idmiracast_session_startspanspan-idmiracast_session_startspanmiracast-session-start"></a><span id="Miracast_session_start"></span><span id="miracast_session_start"></span><span id="MIRACAST_SESSION_START"></span>Miracast 会话启动


当 Miracast 会话启动后，操作系统将调用 [*DxgkDdiQueryChildStatus*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_status) 函数。 显示微型端口驱动程序应设置 [**DXGK \_ 子 \_ 状态**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_child_status)。**键入** 值 **StatusMiracast** ，并使用 **DXGK \_ 子 \_ 状态** 中的 **Miracast** 子结构。 如果监视器连接到 Miracast 接收器，则驱动程序应设置 **miracast**。**已连接** 到 **D3DKMDT \_ VOT \_ MIRACAST**。

驱动程序必须指定 [**D3DKMDT \_ 视频 \_ 信号 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info)的值。**VsyncFreqDivider**，它是通过 miracast 连接会话显示的监视器的 VSync 速率与 miracast 接收器的 VSync 速率的比值。 例如，如果 Miracast 接收器垂直刷新率为 240 Hz，连接显示器的 VSync 中断频率为 30 Hz，则驱动程序应将 **VsyncFreqDivider** 设置为8。

## <a name="span-idhandling_interrupts_for_completed_encode_chunksspanspan-idhandling_interrupts_for_completed_encode_chunksspanspan-idhandling_interrupts_for_completed_encode_chunksspanhandling-interrupts-for-completed-encode-chunks"></a><span id="Handling_interrupts_for_completed_encode_chunks"></span><span id="handling_interrupts_for_completed_encode_chunks"></span><span id="HANDLING_INTERRUPTS_FOR_COMPLETED_ENCODE_CHUNKS"></span>处理已完成编码区块的中断


跨无线 Miracast 连接传输的单个帧的数据可以划分为一个或多个编码区块。 每次 GPU 完成对其中一个区块的编码时，它必须生成一个中断。 为响应此中断，显示微型端口驱动程序必须调用 [*DxgkCbNotifyInterrupt*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_interrupt)函数，并在 [**DXGKARGCB \_ 通知 \_ 中断 \_ 数据**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkargcb_notify_interrupt_data)结构中完成 **MiracastEncodeChunkCompleted** 子结构，包括将 [**DXGK \_ 中断 \_ 类型**](/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_interrupt_type)中断类型设置为 **DXGK \_ 中断 \_ MICACAST \_ 区块 \_ 处理 \_ 完成**。

作为中断处理的一部分，驱动程序可以选择指定 **MiracastEncodeChunkCompleted**。[**DXGKARGCB \_ 通知 \_ 中断 \_ 数据**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkargcb_notify_interrupt_data)结构中的 **pPrivateDriverData** 和 **PrivateDataDriverSize** 成员。 用户模式驱动程序可以访问 [**MIRACAST \_ 块区 \_ 数据**](/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_chunk_data)中的此私有驱动程序数据。**PrivateDriverData** 成员。

如果在一段时间内，显示微型端口驱动程序生成的数据包数比用户模式显示驱动程序使用的数据包要多，则新区块可用的可用内存空间就会用完。在这种情况下，显示微型端口驱动程序会在 **MiracastEncodeChunkCompleted** 中返回 " **\_ 无 \_ 内存" 状态**。**状态**，并且它必须调用 [*DxgkCbNotifyDpc*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_dpc)函数以通知操作系统的 GPU 计划程序有关错误情况。 调用 [**GetNextChunkData**](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data) 函数将返回 **状态 \_ 连接 \_ 重置** 状态代码，后续调用将开始接收在重置操作后提交的区块。 由于某些区块会丢失，因此建议驱动程序生成并传输新的 I 帧。

## <a name="span-idrestrictions_on_source_modesspanspan-idrestrictions_on_source_modesspanspan-idrestrictions_on_source_modesspanrestrictions-on-source-modes"></a><span id="Restrictions_on_source_modes"></span><span id="restrictions_on_source_modes"></span><span id="RESTRICTIONS_ON_SOURCE_MODES"></span>对源模式的限制


一个 WDDM 显示微型端口驱动程序，用于处理像素管道的约束，通常会限制公开给操作系统的源模式。 该驱动程序通过以下方式来完成此工作：只使用像素管道还支持的监视器公开的模式填充源模式的列表。 例如，驱动程序不会基于像素管道约束来修改 EDID。

同样，对于 Miracast，在枚举源和目标模式集时，对 Miracast 显示的显示微型端口驱动程序会限制向操作系统公开的源模式集。 对于 Miracast，会显示 GPU 编码功能、网络属性和接收器解码功能，从而减少了 Miracast 像素管道可支持的源模式的数量。

如果显示微型端口驱动程序调用 [*DXGK \_ VIDPNSOURCEMODESET \_ 接口：:p fnaddmode*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_addmode) 函数尝试将3-d 立体声模式添加到连接到 Miracast 目标的源中，则函数调用将失败。

## <a name="span-idcalling_operating_system-provided_callback_functionsspanspan-idcalling_operating_system-provided_callback_functionsspanspan-idcalling_operating_system-provided_callback_functionsspancalling-operating-system-provided-callback-functions"></a><span id="Calling_operating_system-provided_callback_functions"></span><span id="calling_operating_system-provided_callback_functions"></span><span id="CALLING_OPERATING_SYSTEM-PROVIDED_CALLBACK_FUNCTIONS"></span>调用操作系统提供的回调函数


以下是操作系统提供的 Miracast 内核模式回调函数：

<span id="DxgkCbMiracastSendMessage"></span><span id="dxgkcbmiracastsendmessage"></span><span id="DXGKCBMIRACASTSENDMESSAGE"></span>[**DxgkCbMiracastSendMessage**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)  
将异步消息发送到用户模式显示驱动程序。

<span id="DxgkCbMiracastSendMessageCallback"></span><span id="dxgkcbmiracastsendmessagecallback"></span><span id="DXGKCBMIRACASTSENDMESSAGECALLBACK"></span>[**DxgkCbMiracastSendMessageCallback**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)  
在对 [**DxgkCbMiracastSendMessage**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message) 的调用中使用，以指定已完成 IRP 的 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构。

<span id="DxgkCbReportChunkInfo"></span><span id="dxgkcbreportchunkinfo"></span><span id="DXGKCBREPORTCHUNKINFO"></span>[**DxgkCbReportChunkInfo**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_report_chunk_info)  
报告有关编码块区的信息。

## <a name="span-idsending_messages_asynchronously_from_kernel-mode_to_user-modespanspan-idsending_messages_asynchronously_from_kernel-mode_to_user-modespanspan-idsending_messages_asynchronously_from_kernel-mode_to_user-modespansending-messages-asynchronously-from-kernel-mode-to-user-mode"></a><span id="Sending_messages_asynchronously_from_kernel-mode_to_user-mode"></span><span id="sending_messages_asynchronously_from_kernel-mode_to_user-mode"></span><span id="SENDING_MESSAGES_ASYNCHRONOUSLY_FROM_KERNEL-MODE_TO_USER-MODE"></span>以异步方式将消息从内核模式发送到用户模式


在启动 Miracast 连接的会话之前，显示微型端口驱动程序发送给其 [*关联的用户*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message) 模式驱动程序的任何消息都不会被传递。 因此，如果尚未调用用户模式驱动程序的 [*StartMiracastSession*](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_start_miracast_session) 函数，则会延迟发送的消息，直到 *StartMiracastSession* 返回。 如果在调用 [*StopMiracastSession*](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_stop_miracast_session)函数后发送消息，则该消息将被操作系统删除，并且在 *pIoStatusBlock* 状态中设置的错误状态调用 [*DxgkCbMiracastSendMessageCallback*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)函数 - &gt; **Status**。

## <a name="span-idmodifying_an_existing_display_miniport_driver_to_support_miracast_displaysspanspan-idmodifying_an_existing_display_miniport_driver_to_support_miracast_displaysspanspan-idmodifying_an_existing_display_miniport_driver_to_support_miracast_displaysspanmodifying-an-existing-display-miniport-driver-to-support-miracast-displays"></a><span id="Modifying_an_existing_display_miniport_driver_to_support_Miracast_displays"></span><span id="modifying_an_existing_display_miniport_driver_to_support_miracast_displays"></span><span id="MODIFYING_AN_EXISTING_DISPLAY_MINIPORT_DRIVER_TO_SUPPORT_MIRACAST_DISPLAYS"></span>修改现有的显示微型端口驱动程序以支持 Miracast 显示


调用 [*DxgkDdiStartDevice*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device) 函数时，显示微型端口驱动程序需要添加新的 Miracast 目标，并应将目标的热插拔检测标记 (HPD) 感知值视为 **HpdAwarenessInterruptible** ，以便操作系统不会轮询此目标。 此外，在调用 [*DxgkDdiQueryChildRelations*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_child_relations) 函数时，驱动程序应将 **D3DKMDT \_ VOT \_ MIRACAST** 报告为其连接类型。

驱动程序不应在任何完整的 WDDM 图形设备上报告多个 Miracast 目标。 如果驱动程序报告多个 Miracast 目标，则操作系统将无法启动适配器。 如果未启动 Miracast 连接会话，驱动程序也不应报告此目标上的任何监视器。

当 DirectX 图形内核子系统调用 [*DxgkDdiQueryInterface*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)函数时，驱动程序还需要报告正确的 [**DXGK \_ MIRACAST \_ 显示 \_ 界面**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_miracast_interface)结构，以及指向内核模式地址空间中的函数的指针。

启动 Miracast 会话并将监视器连接到 Miracast 接收器时，显示微型端口驱动程序应设置 [**DXGK \_ 子 \_ 状态**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_child_status)。**Type** 将成员键入到 **StatusMiracast** 常数值，还应设置 **DXGK \_ 子 \_ 状态**。**Miracast**。**连接** 到 **TRUE**，将监视器到达 HPD 到操作系统。 驱动程序应设置 **DXGK \_ 子 \_ 状态**。**Miracast**。**MiracastMonitorType** 成员到连接到接收器的正确监视器类型。 如果接收器是监视器的一部分，则应将此成员设置为 **D3DKMDT \_ VOT \_ MIRACAST**。

如果驱动程序知道监视器的 EDID，则当操作系统调用 [*DxgkDdiQueryDeviceDescriptor*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_device_descriptor) 函数时，它应报告此 edid。

根据硬件功能、Miracast 接收器模式列表和网络带宽，驱动程序应报告正确的源模式、目标模式、旋转模式和缩放模式。 对于目标模式，驱动程序应在 [**D3DKMDT \_ 视频 \_ 信号 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info)中报告正确的 **VSyncFreqDivider** 成员值。 操作系统将目标模式与监视器模式相匹配，并修剪监视器不支持的任何模式。

 

