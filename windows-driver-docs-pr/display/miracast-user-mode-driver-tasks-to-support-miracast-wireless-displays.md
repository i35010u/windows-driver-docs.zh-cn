---
title: Miracast 用户模式驱动程序以支持无线显示
description: 若要启用 Miracast 无线显示，您需要创建独立的实现 Miracast 用户模式驱动程序的唯一 DLL。
ms.assetid: FF5D7760-2407-487A-8363-7AC3B6385F6C
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: aba68fd37f6ab19b942e0d99603743c56cb64183
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524247"
---
# <a name="span-iddisplaymiracastuser-modedrivertaskstosupportmiracastwirelessdisplaysspanmiracast-user-mode-driver-tasks-to-support-miracast-wireless-displays"></a><span id="display.miracast_user-mode_driver_tasks_to_support_miracast_wireless_displays"></span>Miracast 用户模式驱动程序任务，以支持 Miracast 无线显示


若要启用 Miracast 无线显示，您需要创建独立的实现 Miracast 用户模式驱动程序的唯一 DLL。 将专用的会话 0 进程中加载该驱动程序。 作为 INF 文件中的设备软件设置中添加的驱动程序名称**MiracastDriverName**:

``` syntax
[MyDevice_DeviceSettings]
HKR,, MiracastDriverName, %REG_SZ%, Miracast.dll
```

DLL 应具有名为的导出函数[ *QueryMiracastDriverInterface* ](https://msdn.microsoft.com/library/windows/hardware/dn265499)操作系统可调用。 此驱动程序二进制文件不能使用现有 Microsoft Direct3D 用户模式显示驱动程序 DLL。

请注意 Miracast 用户模式驱动程序加载到 UMDF0 进程，因为没有单独的 Windows 上的此驱动程序的 Windows (WOW) 版本所需。 例如，64 位处理器上使用的驱动程序的 64 位版。

操作系统准备就绪准备的步骤连接的 Miracast 会话时，它将调用 Miracast 用户模式驱动程序[ *CreateMiracastContext* ](https://msdn.microsoft.com/library/windows/hardware/dn265169)函数。 当调用此函数时，Miracast 用户模式驱动程序会分配所有需要启动 Miracast 的软件资源连接会话。 在此调用操作系统还提供指向该驱动程序可以在当前的 Miracast 上下文的生存期内调用的回调函数的指针。 然后建立实时流式处理协议 (RTSP) 链接后，操作系统将调用[ *StartMiracastSession* ](https://msdn.microsoft.com/library/windows/hardware/dn265504)实际启动 Miracast 连接会话。 对此函数调用的响应，驱动程序应使用 Winsock [ **getaddrinfo** ](https://msdn.microsoft.com/library/windows/desktop/ms738520)函数或若要获取 Miracast 接收器的 Internet 协议 (IP) 地址，并使用其他相关函数若要创建超文本缓存协议 (HTCP) 远程桌面协议 (RDP) 套接字的标准 Winsock 函数。

Miracast 显示可用时，如果 Miracast 用户模式驱动程序调用的操作系统提供[ **MiracastIoControl** ](https://msdn.microsoft.com/library/windows/hardware/dn265469)函数将 I/O 控制请求发送到显示微型端口驱动程序若要报告监视器到达热插拔检测 (HPD) 感知值。 Miracast 用户模式驱动程序还应查询 Miracast 接收器信息和功能，并报告此信息，例如，监视描述，到显示微型端口驱动程序通过调用的一些**MiracastIoControl**。

Miracast 连接后启动会话，并流式处理数据已准备好之后，将其发送到网络之前，该驱动程序必须调用[ **ReportStatistic** ](https://msdn.microsoft.com/library/windows/hardware/dn265503)回调函数若要向操作系统报告的 Miracast 链接的统计信息。

当操作系统停止响应的连接的 Miracast 会话时，它将调用 Miracast 用户模式驱动程序[ *StopMiracastSession* ](https://msdn.microsoft.com/library/windows/hardware/dn265505)函数。 此函数调用的响应，该驱动程序应关闭其创建和删除流式处理的所有后续数据所有套接字。 该驱动程序不应关闭操作系统为它提供了 RTSP 套接字。 它还应不发送请求到显示微型端口驱动程序报告 HPD 监视器出发。

在对操作系统的调用的响应[ *DestroyMiracastContext* ](https://msdn.microsoft.com/library/windows/hardware/dn265304)函数，Miracast 用户模式驱动程序应释放它分配了中的所有软件资源[*CreateMiracastContext*](https://msdn.microsoft.com/library/windows/hardware/dn265169)。

当显示微型端口驱动程序收到[ *DxgkDdiCommitVidPn* ](https://msdn.microsoft.com/library/windows/hardware/ff559597)请求关闭连接的 Miracast 监视器，该驱动程序应调用的操作系统提供[ *DxgkCbMiracastSendMessage* ](https://msdn.microsoft.com/library/windows/hardware/dn344646)回调函数将一条消息发送到支持 Miracast 的用户模式驱动程序。 Miracast 用户模式驱动程序然后将置于低功耗状态 Miracast 接收器。

[ **RegisterForDataRateNotifications** ](https://msdn.microsoft.com/library/windows/hardware/dn265500) Miracast 用户模式驱动程序将注册要接收一次第二个，网络质量的操作系统可以根据需要调用回调函数服务 (QoS) 通知和 Miracast 连接的当前网络带宽。 此网络信息提供给操作系统调用的[ *pfnDataRateNotify* ](https://msdn.microsoft.com/library/windows/hardware/dn265492)函数。

Miracast 用户模式驱动程序还可以调用操作系统提供的这些可选的回调函数：

<span id="GetNextChunkData"></span><span id="getnextchunkdata"></span><span id="GETNEXTCHUNKDATA"></span>[**GetNextChunkData**](https://msdn.microsoft.com/library/windows/hardware/dn265462)  
提供有关下一个编码块的信息。

<span id="ReportSessionStatus"></span><span id="reportsessionstatus"></span><span id="REPORTSESSIONSTATUS"></span>[**ReportSessionStatus**](https://msdn.microsoft.com/library/windows/hardware/dn265502)  
该驱动程序调用此函数来报告当前连接的 Miracast 会话的状态。

 

 





