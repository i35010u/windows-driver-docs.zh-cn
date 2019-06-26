---
title: 无线显示 (Miracast)
description: （可选） 可以通过 Windows 显示器驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序支持无线 (Miracast) 显示。 此功能是从 Windows 8.1 新增功能。
ms.assetid: 1645E14A-EC4A-4EB8-9AFA-6DF0466D2B1A
keywords:
- 无线显示
- Miracast
- Miracast 设计指南
- Miracast 引用
- 无线显示由 Miracast 用户模式驱动程序调用的回调函数
- 无线显示 Miracast 用户模式驱动程序实现的函数
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: df9384f0b556cdbf83b1c48f554e6b2f00e335e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386230"
---
# <a name="wireless-displays-miracast"></a>无线显示 (Miracast)


（可选） 可以通过 Windows 显示器驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序支持无线 (Miracast) 显示。 此功能是从 Windows 8.1 新增功能。

有关驱动程序和支持 Miracast 的显示器的硬件要求的详细信息，请参阅[构建与 Windows 10 的同类最佳的 Miracast 解决方案](https://download.microsoft.com/download/3/F/9/3F9F0453-04AE-4E4B-87EF-729FF931C1F9/Building%20best-in-class%20Miracast%20solutions%20with%20Windows%2010%20.docx)指南和相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)处**Device.Graphics.WDDM13.DisplayRender.WirelessDisplay**。

## <a name="span-idmiracastdesignguidespanspan-idmiracastdesignguidespanspan-idmiracastdesignguidespanmiracast-design-guide"></a><span id="Miracast_design_guide"></span><span id="miracast_design_guide"></span><span id="MIRACAST_DESIGN_GUIDE"></span>Miracast 设计指南


这些设计指南部分介绍了如何显示微型端口驱动程序和 Miracast 用户模式驱动程序支持 Miracast 显示：

-   [WDDM 显示微型端口驱动程序任务以支持 Miracast 无线显示](wddm-display-miniport-driver-tasks-to-support-miracast-wireless-displays.md)
-   [Miracast 用户模式驱动程序任务，以支持 Miracast 无线显示](miracast-user-mode-driver-tasks-to-support-miracast-wireless-displays.md)
-   [报告 Miracast 区块和统计信息进行编码](reporting-miracast-encode-chunks-and-statistics.md)
-   [用于 Miracast 目标调用 DisplayConfig 函数](calling-displayconfig-functions-for-a-miracast-target.md)

## <a name="span-idmiracastreferencespanspan-idmiracastreferencespanspan-idmiracastreferencespanmiracast-reference"></a><span id="Miracast_reference"></span><span id="miracast_reference"></span><span id="MIRACAST_REFERENCE"></span>Miracast 引用


这些参考部分介绍了如何在您的驱动程序中实现此功能：

### <a name="user-mode-device-driver-interfaces-ddis"></a>用户模式设备驱动程序接口 (DDIs)

**无线显示由 Miracast 用户模式驱动程序调用的回调函数**

在本部分中的参考页介绍了操作系统实现的无线显示器 (Miracast) 用户模式下函数。 仅支持 Miracast 用户模式驱动程序可以调用这些函数。 

返回指向 Miracast 显示回调函数的指针[MIRACAST_CALLBACKS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-_miracast_callbacks)结构。

|主题| 描述 |
|:--|:--|
|[PFN_GET_NEXT_CHUNK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)| 提供信息的后续 Miracast 编码已报告给 Microsoft DirectX 图形内核子系统的区块时[DXGK_INTERRUPT_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ne-d3dkmddi-_dxgk_interrupt_type)中断类型是 DXGK_INTERRUPT_MIRACAST_CHUNK_PROCESSING_COMPLETE。| 
|[PFN_MIRACAST_IO_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_miracast_io_control)| 由用户模式显示驱动程序将同步的 I/O 控制请求发送内核模式显示微型端口驱动程序调用。|
|[PFN_REGISTER_DATARATE_NOTIFICATIONS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_register_datarate_notifications)| 由操作系统以接收网络质量 (QoS) 服务通知和 Miracast 连接的当前网络带宽使用注册的用户模式驱动程序调用。|
|[PFN_REPORT_SESSION_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_session_status)| 由用户模式显示驱动程序调用以当前 Miracast 状态报告连接会话。|
|[PFN_REPORT_STATISTIC](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_report_statistic)| 由用户模式显示驱动程序向操作系统报告的统计信息的 Miracast 链接调用。|
 


**无线显示 Miracast 用户模式驱动程序实现的函数**

在本部分中的参考页介绍了 Miracast 用户模式驱动程序必须实现的无线显示器 (Miracast) 函数。 此类型的驱动程序运行在独立的 DLL 中。 

在响应操作系统调用到[QueryMiracastDriverInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-query_miracast_driver_interface)函数，Miracast 用户模式驱动程序必须提供这些函数中的指针[MIRACAST_DRIVER_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-_miracast_driver_interface)结构，除[pfnDataRateNotify](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_datarate_notification)，这是具有中声明指针[RegisterForDataRateNotifications](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_register_datarate_notifications)。

|主题| 描述 |
|:--|:--|
|[PFN_CREATE_MIRACAST_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_create_miracast_context)| 由操作系统来创建用户模式下 Miracast 上下文调用。|
|[PFN_DESTROY_MIRACAST_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_destroy_miracast_context)| 由操作系统来销毁用户模式下 Miracast 上下文调用。|
|[PFN_HANDLE_KMD_MESSAGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_handle_kmd_message)| 由操作系统来处理异步内核模式接收的消息的 Miracast 用户模式驱动程序显示微型端口驱动程序调用时调用[DxgkCbMiracastSendMessage](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)函数。|
|[PFN_DATARATE_NOTIFICATION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_datarate_notification)| 调用以通知 Miracast 网络链接的比特率已更改的 Miracast 用户模式驱动程序的操作系统。 随操作系统一起注册此函数时**RegisterForDataRateNotifications**调用函数。|
|[QUERY_MIRACAST_DRIVER_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-query_miracast_driver_interface)| 由操作系统来查询 Miracast 用户模式驱动程序接口，调用**MIRACAST_DRIVER_INTERFACE**。|
|[PFN_START_MIRACAST_SESSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_start_miracast_session)| 调用由操作系统启动 Miracast 连接会话。|
|[PFN_STOP_MIRACAST_SESSION](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_stop_miracast_session)| 调用由操作系统启动 Miracast 连接之前尚未启动的会话通过调用**StartMiracastSession**函数。|
 

**无线显示 (Miracast) 结构和枚举**

所有用户模式下结构和枚举用于 Miracast 都显示设备驱动程序接口 (DDIs)。

|主题 |描述 |
|:--|:--|
|[MIRACAST_CALLBACKS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-_miracast_callbacks)| 包含指向 Miracast 用户模式驱动程序可以调用的无线显示器 (Miracast) 运行时回调函数的指针。|
|[MIRACAST_CHUNK_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_chunk_data)| 包含对用户模式驱动程序调用无线显示 (Miracast) 时使用的区块数据进行编码[GetNextChunkData](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)函数。|
|[MIRACAST_CHUNK_ID](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_chunk_id)| 标识的无线显示器 (Miracast) 的存储信息对区块进行编码。|
|[MIRACAST_CHUNK_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_chunk_info)| 包含有关指定无线信息显示 (Miracast) 对区块进行编码。|
|[MIRACAST_CHUNK_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ne-netdispumdddi-miracast_chunk_type)| 指定要处理的无线显示器 (Miracast) 块区信息的类型。|
|[MIRACAST_DATARATE_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_datarate_stats)| 包含有关音频/视频编码器的比特率和失败或重试的 Wi-fi 帧无线显示 (Miracast) pfnDataRateNotify 函数中使用的信息。|
|[MIRACAST_DRIVER_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-_miracast_driver_interface)| 包含指向由 Miracast 用户模式驱动程序实现的无线显示器 (Miracast) 函数的指针。|
|[MIRACAST_PROTOCOL_EVENT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ne-netdispumdddi-miracast_protocol_event)| 指定用户模式显示驱动程序应报告的无线显示器 (Miracast) 协议事件的类型。|
|[MIRACAST_SESSION_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_session_info)| 包含信息的无线显示器 (Miracast) 连接会话。|
|[MIRACAST_STATISTIC_DATA](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_statistic_data)| 包含用户模式显示驱动程序向操作系统报告的 Miracast 统计信息数据。|
|[MIRACAST_STATISTIC_TYPE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ne-netdispumdddi-miracast_statistic_type)| 指定类型的用户模式显示驱动程序将生成的 Miracast 统计信息数据。|
|[MIRACAST_STATUS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ne-netdispumdddi-miracast_status)| 指定用户模式显示驱动程序用来报告 Miracast 连接状态的状态类型。|
|[MIRACAST_WFD_CONNECTION_STATS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netdispumdddi/ns-netdispumdddi-miracast_wfd_connection_stats)| 包含 Wi-Fi Direct 连接上的位速率信息。|

这些其他的用户模式下结构和枚举支持 Miracast 的显示器，并将新的或更新的 Windows 8.1:

-   [ **: DISPLAYCONFIG\_目标\_BASE\_类型**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_target_base_type) （新）
-   [ **: DISPLAYCONFIG\_视频\_信号\_信息**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_video_signal_info) (**AdditionalSignalInfo**添加的子结构)
-   [ **: DISPLAYCONFIG\_设备\_信息\_类型**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_device_info_type) (**DISPLAYCONFIG\_设备\_信息\_获取\_目标\_基\_类型**常量添加)
-   [**D3DKMDT\_视频\_信号\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info) (**AdditionalSignalInfo**添加的子结构)
-   [ **: DISPLAYCONFIG\_设备\_信息\_类型**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_device_info_type) (**DISPLAYCONFIG\_设备\_信息\_获取\_目标\_基\_类型**常量添加)

### <a name="kernel-mode-ddis"></a>内核模式 DDIs

**无线显示 (Miracast) 显示回调接口**

Miracast 显示回调接口包含由 Microsoft DirectX 图形内核子系统以支持无线 (Miracast) 显示实现的函数。 在 Windows 8.1 中开始支持此接口。

本部分包含这些内核模式函数的调用由 Windows 显示驱动程序模型 (WDDM) 1.3 和更高版本显示微型端口驱动程序的参考页：

|主题 |描述 |
|:--|:--|
|[DXGKCB_MIRACAST_SEND_MESSAGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message)|将异步消息发送到用户模式显示驱动程序。|
|[DXGKCB_MIRACAST_SEND_MESSAGE_CALLBACK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)|在内核模式下调用消息时发送给用户模式驱动程序通过调用**DxgkCbMiracastSendMessage**函数已完成或已取消。|
|[DXGKCB_MIRACAST_REPORT_CHUNK_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_report_chunk_info)|有关编码区块的报表信息的显示微型端口驱动程序由调用。|

显示微型端口驱动程序必须填写中这些函数的指针[DXGK_MIRACAST_DISPLAY_CALLBACKS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_miracast_display_callbacks)结构。

**无线显示 (Miracast) 接口**

本部分包含由支持无线 (Miracast) 显示的显示微型端口驱动程序实现的内核模式函数。 在 Windows 8.1 中开始支持此接口。

返回指向 Miracast 接口函数的指针[DXGK_MIRACAST_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_miracast_interface)结构。

|主题 |描述 |
|:--|:--|
|[DXGKCB_MIRACAST_SEND_MESSAGE_CALLBACK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message_callback)|当消息已发送到用户模式驱动程序对 DxgkCbMiracastSendMessage 函数的调用已完成或已被取消时，调用在内核模式下。|
|[DXGKDDI_MIRACAST_CREATE_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_create_context)|创建内核模式上下文 Miracast 的设备。|
|[DXGKDDI_MIRACAST_DESTROY_CONTEXT](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_destroy_context)|销毁 Miracast 的设备的实例。|
|[DXGKDDI_MIRACAST_HANDLE_IO_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_handle_io_control)|由操作系统以请求显示微型端口驱动程序处理同步 I/O 控制请求以响应用户模式显示驱动程序调用 MiracastIoControl 函数调用。|
|[DXGKDDI_MIRACAST_QUERY_CAPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_miracast_query_caps) |查询当前的显示适配器的 Miracast 功能。 仅当显示适配器首次启动，然后将存储返回的功能时，操作系统将调用此函数。|


这些额外内核模式结构和枚举支持 Miracast 的显示器，并将新的或更新的 Windows 8.1:

-   [**DXGK\_MIRACAST\_CAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_miracast_caps)
-   [**D3DKMDT\_视频\_输出\_技术**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ne-d3dkmdt-_d3dkmdt_video_output_technology) (**D3DKMDT\_VOT\_MIRACAST**常量添加)
-   [**D3DKMDT\_视频\_信号\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info) (**AdditionalSignalInfo**添加的子结构)
-   [**DXGK\_子\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ns-dispmprt-_dxgk_child_status) (**Miracast**添加的子结构)
-   [**DXGK\_子\_状态\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/ne-dispmprt-_dxgk_child_status_type) (**StatusMiracast**常量添加)
-   [**DXGKARGCB\_通知\_中断\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkargcb_notify_interrupt_data) (**MiracastEncodeChunkCompleted**添加的子结构)

 

 





