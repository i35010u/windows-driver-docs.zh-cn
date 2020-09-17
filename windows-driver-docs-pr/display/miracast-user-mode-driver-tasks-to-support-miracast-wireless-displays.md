---
title: 支持无线显示的 Miracast 用户模式驱动程序
description: 若要启用 Miracast 无线显示，需要创建实现 Miracast 用户模式驱动程序的独立的唯一 DLL。
ms.assetid: FF5D7760-2407-487A-8363-7AC3B6385F6C
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 6c4c2ceeffef986fdb290c4a855c95d8c219cdca
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715666"
---
# <a name="span-iddisplaymiracast_user-mode_driver_tasks_to_support_miracast_wireless_displaysspanmiracast-user-mode-driver-tasks-to-support-miracast-wireless-displays"></a><span id="display.miracast_user-mode_driver_tasks_to_support_miracast_wireless_displays"></span>用于支持 Miracast 无线显示的 Miracast 用户模式驱动程序任务

> [!NOTE]
> 在 Windows 10 中，操作系统包含 Miracast 无线显示器的本机实现。 驱动程序不应再实现自定义的 Miracast 显示组件。 在 Windows 的未来版本中，可能会删除对自定义 Miracast 实现的支持。

若要启用 Miracast 无线显示，需要创建实现 Miracast 用户模式驱动程序的独立的唯一 DLL。 此驱动程序将在专用会话0进程中加载。 在 INF 文件中的设备软件设置中添加驱动程序的名称，如 **MiracastDriverName**：

``` syntax
[MyDevice_DeviceSettings]
HKR,, MiracastDriverName, %REG_SZ%, Miracast.dll
```

DLL 应具有一个名为 [*QueryMiracastDriverInterface*](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-query_miracast_driver_interface) 的导出函数，操作系统可调用该函数。 此驱动程序二进制文件不得使用现有的 Microsoft Direct3D 用户模式显示驱动程序 DLL。

请注意，由于 Miracast 用户模式驱动程序已加载到 UMDF0 进程中，因此需要此驱动程序的 Windows (WOW) 版本。 例如，在64位处理器上，使用的是64的驱动程序版本。

当操作系统准备好为 Miracast 连接会话做好准备时，它将调用 Miracast 用户模式驱动程序的 [*CreateMiracastContext*](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_create_miracast_context) 函数。 调用此函数时，Miracast 用户模式驱动程序会分配启动 Miracast 连接的会话所需的所有软件资源。 在此调用中，操作系统还提供了在当前 Miracast 上下文的生存期内驱动程序可调用的回调函数的指针。 然后，在建立实时流式处理协议 (RTSP) 链接后，操作系统将调用 [*StartMiracastSession*](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_start_miracast_session) 以实际启动 Miracast 连接会话。 当响应此函数调用时，驱动程序应使用 Winsock [**getaddrinfo**](/windows/win32/api/ws2tcpip/nf-ws2tcpip-getaddrinfo) 函数或其他相关函数来获取 (Miracast 接收器的 IP) 地址的 Internet (协议，并使用标准 Winsock 函数创建超文本缓存协议 HTCP) 远程桌面协议 (RDP) 套接字。

如果提供了 Miracast 显示，则 Miracast 用户模式驱动程序会调用操作系统提供的 [**MiracastIoControl**](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_miracast_io_control) 函数，将 i/o 控制请求发送到显示微型端口驱动程序，以报告监视器到达热插拔检测 (HPD) 感知值。 Miracast 用户模式驱动程序还应查询 Miracast 接收器信息和功能，并通过调用 **MiracastIoControl**将此类信息（如监视器说明）报告给显示微型端口驱动程序。

在启动了 Miracast 连接会话之后，并且在准备好流式处理数据并将其发送到网络之前，驱动程序需要调用 [**ReportStatistic**](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_statistic) 回调函数以报告到操作系统的 Miracast 链接的统计信息。

当操作系统停止 Miracast 连接的会话时，它将调用 Miracast 用户模式驱动程序的 [*StopMiracastSession*](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_stop_miracast_session) 函数。 为了响应此函数调用，驱动程序应关闭其创建的所有套接字，并删除所有进一步的数据流。 驱动程序不应关闭操作系统提供的 RTSP 套接字。 它也不应向显示微型端口驱动程序发送请求，以在监视器出发上报告 HPD。

在响应操作系统对 [*DestroyMiracastContext*](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_destroy_miracast_context) 函数的调用时，Miracast 用户模式驱动程序应释放它在 [*CreateMiracastContext*](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_create_miracast_context)中分配的所有软件资源。

当显示微型端口驱动程序收到关闭连接的 Miracast 监视器的 [*DxgkDdiCommitVidPn*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_commitvidpn) 请求时，驱动程序应调用操作系统提供的 [*DxgkCbMiracastSendMessage*](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkcb_miracast_send_message) 回调函数以将消息发送到 Miracast 用户模式驱动程序。 然后，Miracast 用户模式驱动程序应将 Miracast 接收器置于低功耗状态。

[**RegisterForDataRateNotifications**](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_register_datarate_notifications)回调函数可以选择性地由 Miracast 用户模式驱动程序调用，以注册到要接收的操作系统，每次使用网络服务质量 (QoS) 通知和 Miracast 连接的当前网络带宽。 此网络信息由对 [*pfnDataRateNotify*](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_datarate_notification) 函数的操作系统调用提供。

Miracast 用户模式驱动程序还可以调用由操作系统提供的以下可选回调函数：

<span id="GetNextChunkData"></span><span id="getnextchunkdata"></span><span id="GETNEXTCHUNKDATA"></span>[**GetNextChunkData**](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_get_next_chunk_data)  
提供有关下一个编码块区的信息。

<span id="ReportSessionStatus"></span><span id="reportsessionstatus"></span><span id="REPORTSESSIONSTATUS"></span>[**ReportSessionStatus**](/windows-hardware/drivers/ddi/netdispumdddi/nc-netdispumdddi-pfn_report_session_status)  
驱动程序调用此函数以报告当前 Miracast 连接会话的状态。

 

