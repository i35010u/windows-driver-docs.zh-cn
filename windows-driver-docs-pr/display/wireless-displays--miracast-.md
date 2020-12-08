---
title: 无线显示 (Miracast)
description: Windows 显示驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序可以选择支持无线 (Miracast) 显示。 此功能是从 Windows 8.1 开始的新功能。
keywords:
- 无线显示
- Miracast
- Miracast 设计指南
- Miracast 参考
- 由 Miracast 用户模式驱动程序调用的无线显示回调函数
- 由 Miracast 用户模式驱动程序实现的无线显示功能
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 926591136dc86cadde98d55fc2ae05b2c2435eb1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818517"
---
# <a name="wireless-displays-miracast"></a>无线显示 (Miracast)

> [!NOTE]
> 本文档介绍了驱动程序如何在 Windows 8.1 中实现自定义 Miracast 堆栈。 从 Windows 10 开始，操作系统附带了可用于任何 GPU 的内置 Miracast 堆栈，并且不再建议驱动程序实现自定义 Miracast 堆栈。 因此，此文档已弃用，Microsoft 可能会在将来的 Windows 版本中删除对自定义 Miracast 堆栈的支持。

Windows 显示驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序可以选择支持无线 (Miracast) 显示。 此功能是从 Windows 8.1 开始的新功能。

有关支持 Miracast 显示的驱动程序和硬件要求的详细信息，请参阅 [通过 Windows 10 指南构建同类最佳无线投影解决方案](/windows-hardware/design/device-experiences/wireless-projection) 和相关的 [WHCK 文档](/windows-hardware/test/hlk/windows-hardware-lab-kit) 。 **WDDM13. DisplayRender. WirelessDisplay**。

## <a name="span-idmiracast_design_guidespanspan-idmiracast_design_guidespanspan-idmiracast_design_guidespanmiracast-design-guide"></a><span id="Miracast_design_guide"></span><span id="miracast_design_guide"></span><span id="MIRACAST_DESIGN_GUIDE"></span>Miracast 设计指南


这些设计指南部分介绍了显示微型端口驱动程序和 Miracast 用户模式驱动程序如何支持 Miracast 显示：

-   [用于支持 Miracast 无线显示的 WDDM 显示微型端口驱动程序任务](wddm-display-miniport-driver-tasks-to-support-miracast-wireless-displays.md)
-   [用于支持 Miracast 无线显示的 Miracast 用户模式驱动程序任务](miracast-user-mode-driver-tasks-to-support-miracast-wireless-displays.md)
-   [报告 Miracast 编码区块和统计信息](reporting-miracast-encode-chunks-and-statistics.md)
-   [对 Miracast 目标调用 DisplayConfig 函数](calling-displayconfig-functions-for-a-miracast-target.md)

## <a name="span-idmiracast_referencespanspan-idmiracast_referencespanspan-idmiracast_referencespanmiracast-reference"></a><span id="Miracast_reference"></span><span id="miracast_reference"></span><span id="MIRACAST_REFERENCE"></span>Miracast 参考


这些参考部分介绍如何在你的驱动程序中实现此功能：

### <a name="user-mode-device-driver-interfaces-ddis"></a>用户模式设备驱动程序接口 (DDIs) 

**由 Miracast 用户模式驱动程序调用的无线显示回调函数**

此部分中的参考页面描述了 (Miracast) 操作系统实现的用户模式功能的无线显示。 只有 Miracast 用户模式驱动程序才能调用这些功能。 

指向 Miracast 显示回调函数的指针将在 [MIRACAST_CALLBACKS](/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-_miracast_callbacks) 结构中返回。

|主题| 描述 |
|:--|:--|
|[PFN_GET_NEXT_CHUNK_DATA](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)| 提供有关 DXGK_INTERRUPT_MIRACAST_CHUNK_PROCESSING_COMPLETE [DXGK_INTERRUPT_TYPE](/windows-hardware/drivers/ddi/d3dkmddi/ne-d3dkmddi-_dxgk_interrupt_type) 中断类型时报告给 Microsoft DirectX 图形内核子系统的下一个 Miracast 编码区块的信息。| 
|[PFN_MIRACAST_IO_CONTROL](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_miracast_io_control)| 由用户模式显示驱动程序调用，以向同步 i/o 控制请求发送内核模式显示微型端口驱动程序。|
|[PFN_REGISTER_DATARATE_NOTIFICATIONS](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_register_datarate_notifications)| 由用户模式驱动程序调用，以向操作系统注册，以接收网络服务质量 (QoS) 通知和 Miracast 连接的当前网络带宽。|
|[PFN_REPORT_SESSION_STATUS](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_session_status)| 由用户模式显示驱动程序调用，以报告当前 Miracast 连接会话的状态。|
|[PFN_REPORT_STATISTIC](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)| 由用户模式显示驱动程序调用，用于报告到操作系统的 Miracast 链接的统计信息。|
 


**由 Miracast 用户模式驱动程序实现的无线显示功能**

此部分中的参考页面描述了 Miracast 用户模式驱动程序必须实现 (Miracast) 函数的无线显示。 此类驱动程序在独立 DLL 中运行。 

为了响应对 [QueryMiracastDriverInterface](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-query_miracast_driver_interface) 函数的操作系统调用，Miracast 用户模式驱动程序必须在 [MIRACAST_DRIVER_INTERFACE](/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-_miracast_driver_interface) 结构中提供指向这些函数的指针，但 [PfnDataRateNotify](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_datarate_notification)除外，其中包含 [RegisterForDataRateNotifications](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_register_datarate_notifications)中声明的指针。

|主题| 描述 |
|:--|:--|
|[PFN_CREATE_MIRACAST_CONTEXT](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_create_miracast_context)| 由操作系统调用以创建用户模式 Miracast 上下文。|
|[PFN_DESTROY_MIRACAST_CONTEXT](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_destroy_miracast_context)| 由操作系统调用以销毁用户模式的 Miracast 上下文。|
|[PFN_HANDLE_KMD_MESSAGE](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_handle_kmd_message)| 由操作系统调用，用于处理当显示微型端口驱动程序调用 [DxgkCbMiracastSendMessage](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message) 函数时，Miracast 用户模式驱动程序收到的异步内核模式消息。|
|[PFN_DATARATE_NOTIFICATION](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_datarate_notification)| 由操作系统调用以通知 Miracast 用户模式驱动程序，Miracast 网络链接的比特率已更改。 调用 **RegisterForDataRateNotifications** 函数时，此函数将注册到操作系统。|
|[QUERY_MIRACAST_DRIVER_INTERFACE](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-query_miracast_driver_interface)| 由操作系统调用以查询 Miracast 用户模式驱动程序接口， **MIRACAST_DRIVER_INTERFACE**。|
|[PFN_START_MIRACAST_SESSION](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_start_miracast_session)| 由操作系统调用以启动 Miracast 连接的会话。|
|[PFN_STOP_MIRACAST_SESSION](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_stop_miracast_session)| 由操作系统调用，以启动已通过调用 **StartMiracastSession** 函数启动的 Miracast 连接会话。|
 

**(Miracast) 结构和枚举的无线显示**

与 Miracast 显示设备驱动程序接口一起使用的所有用户模式结构和枚举 (DDIs) 。

|主题 |描述 |
|:--|:--|
|[MIRACAST_CALLBACKS](/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-_miracast_callbacks)| 包含一个指向 (Miracast 的无线显示的指针) Miracast 用户模式驱动程序可调用的运行时回调函数。|
|[MIRACAST_CHUNK_DATA](/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_chunk_data)| 包含编码区块数据，当用户模式驱动程序调用 (Miracast) [GetNextChunkData](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data) 函数的无线显示时使用。|
|[MIRACAST_CHUNK_ID](/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_chunk_id)| 存储用于标识 (Miracast) 编码区块的无线显示的信息。|
|[MIRACAST_CHUNK_INFO](/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_chunk_info)| 包含有关 (Miracast) 编码区块的指定无线显示的信息。|
|[MIRACAST_CHUNK_TYPE](/windows-hardware/drivers/ddi/netdispumdddi/ne-netdispumdddi-miracast_chunk_type)| 指定要处理 (Miracast) 区块信息的无线显示类型。|
|[MIRACAST_DATARATE_STATS](/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_datarate_stats)| 包含无线显示中使用的信息 (Miracast) pfnDataRateNotify 函数有关音频/视频编码器比特率，Wi-Fi 帧失败或重试。|
|[MIRACAST_DRIVER_INTERFACE](/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-_miracast_driver_interface)| 包含指向由 Miracast 用户模式驱动程序实现 (Miracast) 函数的无线显示的指针。|
|[MIRACAST_PROTOCOL_EVENT](/windows-hardware/drivers/ddi/netdispumdddi/ne-netdispumdddi-miracast_protocol_event)| 指定用户模式显示驱动程序应报告的 (Miracast) 协议事件的无线显示类型。|
|[MIRACAST_SESSION_INFO](/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_session_info)| 包含有关无线显示器 (Miracast) 连接会话的信息。|
|[MIRACAST_STATISTIC_DATA](/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_statistic_data)| 包含用户模式显示驱动程序向操作系统报告的 Miracast 统计信息数据。|
|[MIRACAST_STATISTIC_TYPE](/windows-hardware/drivers/ddi/netdispumdddi/ne-netdispumdddi-miracast_statistic_type)| 指定用户模式显示驱动程序生成的 Miracast 统计数据的类型。|
|[MIRACAST_STATUS](/windows-hardware/drivers/ddi/netdispumdddi/ne-netdispumdddi-miracast_status)| 指定用户模式显示驱动程序用来报告 Miracast 连接状态的状态类型。|
|[MIRACAST_WFD_CONNECTION_STATS](/windows-hardware/drivers/ddi/netdispumdddi/ns-netdispumdddi-miracast_wfd_connection_stats)| Wi-Fi 直接连接上包含比特率信息。|

这些附加的用户模式结构和枚举支持 Miracast 显示，并是新的或更新的 Windows 8.1 的：

-   [**DISPLAYCONFIG \_目标 \_ 基 \_ 类型**](/windows/win32/api/wingdi/ns-wingdi-displayconfig_target_base_type) (new) 
-   [**DISPLAYCONFIG \_添加 \_ \_**](/windows/win32/api/wingdi/ns-wingdi-displayconfig_video_signal_info) 了 **ADDITIONALSIGNALINFO** 子结构 (视频信号信息) 
-   [**DISPLAYCONFIG \_添加了设备 \_ 信息 \_ 类型**](/windows/win32/api/wingdi/ne-wingdi-displayconfig_device_info_type) (**DISPLAYCONFIG \_ 设备 \_ 信息 \_ 获取 \_ 目标 \_ 基本 \_ 类型** 常量) 
-   [**D3DKMDT \_添加 \_ \_**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info) 了 **ADDITIONALSIGNALINFO** 子结构 (视频信号信息) 
-   [**DISPLAYCONFIG \_添加了设备 \_ 信息 \_ 类型**](/windows/win32/api/wingdi/ne-wingdi-displayconfig_device_info_type) (**DISPLAYCONFIG \_ 设备 \_ 信息 \_ 获取 \_ 目标 \_ 基本 \_ 类型** 常量) 

### <a name="kernel-mode-ddis"></a>内核模式 DDIs

**(Miracast) 显示回调接口的无线显示**

Miracast 显示回调接口包含由 Microsoft DirectX 图形内核子系统实现的函数，以支持无线 (Miracast) 显示。 从 Windows 8.1 开始支持此接口。

本部分包含这些内核模式功能的参考页面，Windows 显示驱动程序模型 (WDDM) 1.3 和更高版本的显示微型端口驱动程序调用这些功能：

|主题 |描述 |
|:--|:--|
|[DXGKCB_MIRACAST_SEND_MESSAGE](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)|将异步消息发送到用户模式显示驱动程序。|
|[DXGKCB_MIRACAST_SEND_MESSAGE_CALLBACK](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)|当通过调用 **DxgkCbMiracastSendMessage** 函数发送到用户模式驱动程序的消息完成或已取消时，在内核模式下调用。|
|[DXGKCB_MIRACAST_REPORT_CHUNK_INFO](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_report_chunk_info)|由显示微型端口驱动程序调用以报告有关编码块区的信息。|

显示微型端口驱动程序必须填写指向 [DXGK_MIRACAST_DISPLAY_CALLBACKS](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_miracast_display_callbacks) 结构中这些函数的指针。

**(Miracast) 接口的无线显示**

本部分包含的内核模式功能由支持无线 (Miracast) 显示的显示微型端口驱动程序实现。 从 Windows 8.1 开始支持此接口。

在 [DXGK_MIRACAST_INTERFACE](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_miracast_interface) 结构中返回 Miracast 接口函数的指针。

|主题 |描述 |
|:--|:--|
|[DXGKCB_MIRACAST_SEND_MESSAGE_CALLBACK](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)|当通过调用 DxgkCbMiracastSendMessage 函数发送到用户模式驱动程序的消息完成或已取消时，在内核模式下调用。|
|[DXGKDDI_MIRACAST_CREATE_CONTEXT](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_create_context)|为 Miracast 设备创建内核模式上下文。|
|[DXGKDDI_MIRACAST_DESTROY_CONTEXT](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_destroy_context)|销毁 Miracast 设备的实例。|
|[DXGKDDI_MIRACAST_HANDLE_IO_CONTROL](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_handle_io_control)|由操作系统调用，请求显示微型端口驱动程序处理同步 i/o 控制请求，以响应对 MiracastIoControl 函数的用户模式显示驱动程序调用。|
|[DXGKDDI_MIRACAST_QUERY_CAPS](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_miracast_query_caps) |查询当前显示适配器的 Miracast 功能。 只有首次启动显示适配器，然后存储返回的功能时，操作系统才会调用此函数。|


这些附加的内核模式结构和枚举支持 Miracast 显示，并是新的或更新的 Windows 8.1 的：

-   [**DXGK \_ MIRACAST \_ CAP**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_miracast_caps)
-   [**D3DKMDT \_添加 \_ \_**](/windows-hardware/drivers/ddi/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology) 了 **D3DKMDT \_ VOT \_ MIRACAST** 常量 (视频输出技术) 
-   [**D3DKMDT \_添加 \_ \_**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info) 了 **ADDITIONALSIGNALINFO** 子结构 (视频信号信息) 
-   [**DXGK \_添加 \_ 的子**](/windows-hardware/drivers/ddi/dispmprt/ns-dispmprt-_dxgk_child_status) (**Miracast** 子结构的子状态) 
-   [**DXGK \_添加的子 \_ 状态 \_ 类型**](/windows-hardware/drivers/ddi/dispmprt/ne-dispmprt-_dxgk_child_status_type) (**StatusMiracast** 常量) 
-   [**DXGKARGCB \_向 \_ \_**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkargcb_notify_interrupt_data) **添加 (子** 结构) 通知中断数据

 

