---
title: 虚拟工作站
description: 虚拟工作站
ms.assetid: 6228439c-4c01-4fa9-8b45-b46ed90fa661
keywords:
- 虚拟工作站 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5e8cf4199937dff831f917cd9adb0fba7820ed1
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732521"
---
# <a name="virtual-station"></a>虚拟工作站




 

从 NDIS 6.20 (Windows 7) 开始，操作系统提供了一个虚拟工作站 (VSTA) ，可与802.11 微型端口驱动程序交互。

独立硬件供应商 (IHV) 通过 [IHV 扩展性框架](overview-of-ihv-extensibility.md) 使用 VSTA 功能，而不是通过 api)  (的 Win32 应用程序编程接口。

当 IHV 扩展 DLL 调用 [**Dot11ExtRequestVirtualStation**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_request_virtual_station) 函数时，将启动虚拟机的创建。 操作系统一次仅在计算机上创建一个虚拟机，并且仅当 IHV 扩展 DLL 发出 **Dot11ExtRequestVirtualStation** 请求时。

操作系统将调用 [*Dot11ExtIhvInitVirtualStation*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_virtual_station) 函数，以便为虚拟机操作初始化 IHV 扩展 DLL。 此调用还将初始化操作系统和 DLL 之间的用户模式 API 接口。

**注意**   若要确保以一致的方式创建虚拟工作站，计算机应该只安装一个尝试使用虚拟机功能的 IHV 扩展 DLL。 即使安装了多个 DLL，也只能创建一个虚拟工作站。 在计算机重新启动后，操作系统无法保证哪个 DLL 有权访问虚拟机。 请注意，如果已在对一个 DLL 的请求创建了虚拟机，而另一个 DLL 调用了 **Dot11ExtRequestVirtualStation**，则可能会返回成功代码，但不会创建第二个虚拟机。
IHV 扩展 DLL 在调用 **Dot11ExtRequestVirtualStation** 函数后应设置两分钟计时器。 如果计时器在虚拟机适配器到达事件之前过期，则 DLL 应假定未创建虚拟工作站。

 

### <a name="extensible-apvirtual-station-interactions"></a><a href="" id="extensible-ap-virtual-station-interactions"></a> 可扩展的 AP/虚拟工作站交互

如果你的驱动程序实现虚拟机功能，但不能同时在不同的端口上同时承受 (ExtAP) 和虚拟工作站连接的 [可扩展访问点 ](/previous-versions/windows/hardware/wireless/extensible-access-point-operation-mode) ，则驱动程序应执行以下操作。

-   通知操作系统，用于 ExtAP 的端口是否可以或无法始终维持功能。 具体而言，驱动程序应使用适当的状态代码 ( [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication) - &gt; **StatusCode**) 和原因代码，在 ExtAP 端口上发出以下状态指示：

    <a href="" id="ndis-status-dot11-stop-ap"></a>[NDIS \_ 状态 \_ DOT11 \_ 停止 \_ AP](/previous-versions/windows/hardware/wireless/ndis-status-dot11-stop-ap)  
    指示 AP 功能不能在 ExtAP 端口上保持不变。 在这种情况下，请将[**DOT11 \_ 停止 \_ ap \_ 参数**](/windows-hardware/drivers/ddi/windot11/ns-windot11-_dot11_stop_ap_parameters) - &gt; **ulReason**设置为 "DOT11 \_ 停止 \_ ap \_ 原因 \_ \_ " 设置为 "活动"。 在以下情况下发出此状态指示：

    -   在虚拟工作站端口开始使用共享资源之前，会阻止同时进行虚拟工作站和 ExtAP 连接
    -   如果 ExtAP 端口转换为 ExtAP INIT 状态，虚拟工作站资源使用会阻止成功初始化 ExtAP 端口。

    <a href="" id="---------ndis-status-dot11-can-sustain-ap"></a>[NDIS \_ 状态 \_ DOT11 \_ 可以 \_ 承受 \_ AP](/previous-versions/windows/hardware/wireless/ndis-status-dot11-can-sustain-ap)  
    指示虚拟工作站端口已断开连接，或使用虚拟工作站资源不会阻止成功将端口转换为 ExtAP INIT 状态。

-   连接到虚拟工作站端口时，请调用 [**Dot11ExtSetVirtualStationAPProperties**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_virtual_station_ap_properties) 函数，以提供有关虚拟机连接承载的 AP 实现的信息。

-   如果 ExtAP 端口在操作状态下运行并且发生以下情况之一，则虚拟工作站端口连接将失败：
    -   一个或多个客户端位于 ExtAP 端口上。
    -   虚拟工作站尝试启动复制 [无线托管网络](/windows/win32/nativewifi/about-the-wireless-hosted-network) 设置的连接。

### <a name="native-80211-ihv-extensibility-functions-that-support-a-virtual-station"></a><a href="" id="native-802-11-ihv-extensibility-functions-that-support-a-virtual-stati"></a> 支持虚拟工作站的本机 802.11 IHV 扩展性函数

[**Dot11ExtQueryVirtualStationProperties**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_query_virtual_station_properties)

[**Dot11ExtReleaseVirtualStation**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_release_virtual_station)

[**Dot11ExtRequestVirtualStation**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_request_virtual_station)

[**Dot11ExtSetVirtualStationAPProperties**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_virtual_station_ap_properties)

### <a name="structures-that-support-a-virtual-station"></a><a href="" id="structures-that-support-a-virtual-station"></a> 支持虚拟工作站的结构

[**DOT11EXT \_ 虚拟 \_ 工作站 \_ AP \_ 属性**](/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_virtual_station_ap_property)

[**DOT11EXT \_ 虚拟 \_ 工作站 \_ api**](/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_virtual_station_apis)

 

 