---
title: ndiskd. get-netadapter
description: Ndiskd. get-netadapter 扩展显示有关在系统上处于活动状态的 NDIS 微型端口或网络适配器的信息。
keywords:
- ndiskd get-netadapter Windows 调试
ms.date: 06/23/2020
topic_type:
- apiref
api_name:
- ndiskd.netadapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 18c7b403f42765848ea43b09592eb02f55e86416
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833235"
---
# <a name="ndiskdnetadapter"></a>!ndiskd.netadapter

**！ Ndiskd get-netadapter** 扩展显示有关在系统上处于活动状态的 NDIS 微型端口或网络适配器的信息。 如果在没有参数的情况下运行此命令，！ ndiskd 将显示所有网络适配器的列表。

```console
     !ndiskd.netadapter [-handle <x>] [-basic] [-diag] [-state] [-bindings] 
        [-ports] [-offloads] [-filterdb] [-timers] [-rst]
        [-pm] [-ss] [-aoac] [-wol] [-protocoloffloads]
        [-rss] [-hw] [-device] [-wmi] [-customwmi]
        [-ndiswmi] [-ref] [-log] [-grovel] [-findname <any>]
        [-rcvfilter] [-nicswitch] [-rcvqueues] [-nicswitches] [-iov]
        [-vfs] [-vports] [-iftrace] [-ip]
```

## <a name="parameters"></a>参数

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
NDIS 小型端口的句柄。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span>*-基本*   
显示有关微型端口的摘要信息。

<span id="_______-diag______"></span><span id="_______-DIAG______"></span>*-诊断*   
显示自动诊断警报 (是否有任何) 。

<span id="_______-state______"></span><span id="_______-STATE______"></span>*-state*   
显示微型端口的当前状态。

<span id="_______-bindings______"></span><span id="_______-BINDINGS______"></span>*-bindings*   
显示微型端口绑定。

<span id="_______-ports______"></span><span id="_______-PORTS______"></span>*-端口*   
显示 NDIS 端口的列表。

<span id="_______-offloads______"></span><span id="_______-OFFLOADS______"></span>*-卸载*   
显示任务卸载状态和功能。

<span id="_______-filterdb______"></span><span id="_______-FILTERDB______"></span>*-filterdb*   
显示当前的数据包筛选器。

<span id="_______-timers______"></span><span id="_______-TIMERS______"></span>*-计时器*   
显示微型端口分配的计时器对象。

<span id="_______-rst______"></span><span id="_______-RST______"></span>*-rst*   
显示 Receive-Side 限制状态。

<span id="_______-pm______"></span><span id="_______-PM______"></span>*-pm*   
显示电源管理状态和功能。

<span id="_______-ss______"></span><span id="_______-SS______"></span>*-ss*   
显示选择性挂起状态。

<span id="_______-aoac______"></span><span id="_______-AOAC______"></span>*-aoac*   
显示 AOAC (连接待机) 状态。

<span id="_______-wol______"></span><span id="_______-WOL______"></span>*-wol*   
显示 LAN 唤醒 (WoL) 配置。

<span id="_______-protocoloffloads______"></span><span id="_______-PROTOCOLOFFLOADS______"></span>*-protocoloffloads*   
显示活动电源管理协议卸载。

<span id="_______-rss______"></span><span id="_______-RSS______"></span>*-rss*   
显示接收方缩放参数。

<span id="_______-hw______"></span><span id="_______-HW______"></span>*-hw*   
显示硬件资源。

<span id="_______-device______"></span><span id="_______-DEVICE______"></span>*-设备*   
显示有关基础 NT 设备对象的信息。

<span id="_______-wmi______"></span><span id="_______-WMI______"></span>*-wmi*   
显示注册到适配器的 WMI Guid。

<span id="_______-customwmi______"></span><span id="_______-CUSTOMWMI______"></span>*-customwmi*   
显示小型端口注册的自定义 WMI Guid。

<span id="_______-ndiswmi______"></span><span id="_______-NDISWMI______"></span>*-ndiswmi*   
显示 NDIS 提供的 WMI Guid。

<span id="_______-ref______"></span><span id="_______-REF______"></span>*-ref*   
显示对小型端口上的引用的细分。

<span id="_______-log______"></span><span id="_______-LOG______"></span>*-日志*   
显示 PnP 和电源事件日志。

<span id="_______-grovel______"></span><span id="_______-GROVEL______"></span>*-grovel*   
在内存中强制搜索微型端口块。

<span id="_______-findname______"></span><span id="_______-FINDNAME______"></span>*-system.windows.frameworkelement.findname*   
按名称前缀筛选微型端口。

<span id="_______-rcvfilter______"></span><span id="_______-RCVFILTER______"></span>*-rcvfilter*   
显示接收筛选功能。

<span id="_______-nicswitch______"></span><span id="_______-NICSWITCH______"></span>*-nicswitch*   
显示 NIC 交换机功能。

<span id="_______-rcvqueues______"></span><span id="_______-RCVQUEUES______"></span>*-rcvqueues*   
显示接收队列。

<span id="_______-nicswitches______"></span><span id="_______-NICSWITCHES______"></span>*-nicswitches*   
显示 NIC 交换机。

<span id="_______-iov______"></span><span id="_______-IOV______"></span>*-*   
显示 SR-IOV (单根 i/o 虚拟化) 功能。

<span id="_______-vfs______"></span><span id="_______-VFS______"></span>*-vfs*   
显示 SR-IOV VFs (虚拟筛选器) 。

<span id="_______-vports______"></span><span id="_______-VPORTS______"></span>*-vports*   
显示 Vports (虚拟端口) 。

<span id="_______-ifrtrace______"></span><span id="_______-IFRTRACE______"></span>*-ifrtrace*   
显示正在进行的记录器跟踪。

<span id="_______-ip______"></span><span id="_______-IP______"></span>*-ip*   
显示网络接口上的 IP 地址。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

通过运行不带参数的 **！ ndiskd** ，你可以获取系统上所有网络适配器的列表及其关联的微型端口驱动程序。 在此示例输出中，查找 "Microsoft 内核调试" 网络适配器，其句柄为 ffffdf80140c71a0。 有关内核调试网络适配器用途的详细信息，请参阅 NDIS 博客上 [的通过网络进行内核调试](/archive/blogs/ndis/kernel-debugging-over-the-network) 。

```console
3: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffdf8015a98380   ffffdf8015aa11a0    Microsoft ISATAP Adapter #2
    ffffdf801418d650   ffffdf80140c71a0    Microsoft Kernel Debug Network Adapter
```

通过单击微型端口驱动程序的句柄或输入 **！ ndiskd**，你现在可以看到该设备上的所有 NDIS 状态。 这对于解决网络驱动程序或查明问题在网络堆栈中的位置非常有用。 例如，可以查看驱动程序的数据路径状态，并查看其是否已连接。

在此网络适配器报表的底部，可以单击多个其他链接来浏览其他信息，如任何挂起的 Oid 以及任务卸载的状态。 这些链接对应于 **！ ndiskd. get-netadapter** 的许多参数。

```console
3: kd> !ndiskd.netadapter ffffdf80140c71a0


MINIPORT

    Microsoft Kernel Debug Network Adapter

    Ndis handle        ffffdf80140c71a0
    Ndis API version   v6.20
    Adapter context    ffffdf80147d7230
    Driver             ffffdf801418d650 - kdnic  v4.2
    Network interface  ffffdf80139b3a20

    Media type         802.3
    Physical medium    NdisPhysicalMediumOther
    Device instance    ROOT\KDNIC\0000
    Device object      ffffdf80140c7050    More information
    MAC address        18-03-73-c1-e8-72


STATE

    Miniport           Running
    Device PnP         Started             Show state history
    Datapath           Normal
    Interface          Up
    Media              Connected
    Power              D0
    References         0n10                Show detail
    Total resets       0
    Pending OID        None
    Flags              NOT_BUS_MASTER, ALLOW_BUGCHECK_CALLBACK,
                       BUGCHECK_CALLBACK_REGISTERED, DEFAULT_PORT_ACTIVATED,
                       SUPPORTS_MEDIA_SENSE, DOES_NOT_DO_LOOPBACK,
                       MEDIA_CONNECTED
    PnP flags          VIRTUAL_DEVICE, HIDDEN, NO_HALT_ON_SUSPEND,
                       RECEIVED_START


BINDINGS

    Protocol list      Driver              Open               Context           
    MSLLDP             ffffdf80120a5c10    ffffdf8015a749c0   ffffdf8015d325e0
    TCPIP              ffffdf80131cc010    ffffdf801494a650   ffffdf801494aa50
    NDISUIO            ffffdf8015a58140    ffffdf8015a78c10   ffffdf8015a77e00
    TCPIP6             ffffdf80131c9c10    ffffdf80147875a0   ffffdf801494f010
    (RASPPPOE)         Not running
    RSPNDR             ffffdf80120a0c10    ffffdf8015a79c10   ffffdf8015a79010
    LLTDIO             ffffdf8015a5f9b0    ffffdf801406f010   ffffdf8015a786c0
    (RDMANDK)          ffffdf801406d8f0    Declined with NDIS_STATUS_NOT_RECOGNIZED

    Filter list        Driver              Module             Context           
    WFP 802.3 MAC Layer LightWeight Filter-0000
                       ffffdf80139a5a70    ffffdf801494c670   ffffdf801494a010
    QoS Packet Scheduler-0000
                       ffffdf8014039d90    ffffdf801494dc70   ffffdf80147dc2b0
    WFP Native MAC Layer LightWeight Filter-0000
                       ffffdf80139fcd70    ffffdf8014950c70   ffffdf8014950880



MORE INFORMATION

    Driver handlers                        Task offloads
    Power management                       PM protocol offloads
    Pending OIDs                           Timers
    Pending NBLs                           Receive side throttling
    Wake-on-LAN (WoL)                      Packet filter
    Receive queues                         Receive filtering
    RSS                                    NIC switch
    Hardware resources                     Selective suspend
    NDIS ports                             WMI guids
    Diagnostic log
```

例如，使用 **！ ndiskd** 作为进一步调试的开始位置，单击报表底部的 "驱动程序处理程序" 链接可查看此网络适配器的微型端口驱动程序的所有已注册驱动程序回调处理程序的列表。 在下面的示例中，单击链接会导致！ ndiskd 与此网络适配器的微型端口驱动程序的句柄一起运行 [**！ ndiskd。**](-ndiskd-minidriver.md) 微型端口驱动程序是 kdnic 4.2 及其句柄 ffffdf801418d650。

```console
3: kd> !ndiskd.minidriver ffffdf801418d650 -handlers


HANDLERS

    NDIS Handler                           Function pointer   Symbol (if available)
    InitializeHandlerEx                    fffff80f1fd78230  bp
    SetOptionsHandler                      fffff80f1fd72800  bp
    HaltHandlerEx                          fffff80f1fd78040  bp
    ShutdownHandlerEx                      fffff80f1fd722c0  bp

    CheckForHangHandlerEx                  fffff80f1fd72810  bp
    ResetHandlerEx                         fffff80f1fd72f70  bp

    PauseHandler                           fffff80f1fd78000  bp
    RestartHandler                         fffff80f1fd78940  bp

    OidRequestHandler                      fffff80f1fd71c90  bp
    CancelOidRequestHandler                fffff80f1fd722c0  bp
    DirectOidRequestHandler                [None]
    CancelDirectOidRequestHandler          [None]
    DevicePnPEventNotifyHandler            fffff80f1fd789a0  bp

    SendNetBufferListsHandler              fffff80f1fd71870  bp
    ReturnNetBufferListsHandler            fffff80f1fd71b50  bp
    CancelSendHandler                      fffff80f1fd722c0  bp
```

你现在可以单击每个处理程序右侧的 "最佳实践" 链接，以在该处理程序上设置一个断点来调试特定的问题。 例如，如果数据路径中存在挂起，你可以调查驱动程序的 SendNetBufferListsHandler 或 ReturnNetBufferListsHandler。

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[通过网络进行内核调试](/archive/blogs/ndis/kernel-debugging-over-the-network)

[**!ndiskd.minidriver**](-ndiskd-minidriver.md)
