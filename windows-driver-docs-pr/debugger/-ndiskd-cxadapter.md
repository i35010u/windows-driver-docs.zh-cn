---
title: ndiskd.cxadapter
description: Ndiskd. cxadapter 扩展显示有关 GET-NETADAPTER 对象的信息。
keywords:
- ndiskd cxadapter Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.cxadapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ed321ff413e87c7caeb1428699c7cd6da3727370
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798409"
---
# <a name="ndiskdcxadapter"></a>!ndiskd.cxadapter


**！ Ndiskd cxadapter** 扩展显示有关 get-netadapter 对象的信息。

有关网络适配器 WDF 类扩展的详细信息 (NetAdapterCx) ，请参阅 [网络适配器 Wdf Class extension (Cx) ](../netcx/index.md)。

```console
!ndiskd.cxadapter [-handle <x>] [-basic] [-power] [-datapath] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
必需。 GET-NETADAPTER 的句柄。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span>*-基本*   
显示基本信息。

<span id="_______-power______"></span><span id="_______-POWER______"></span>*-power*   
显示有关 GET-NETADAPTER 的 NETPOWERSETTINGS 对象的信息。

<span id="_______-datapath______"></span><span id="_______-DATAPATH______"></span>*-数据路径*   
显示有关数据路径队列的信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

若要获取 GET-NETADAPTER 对象的句柄，请首先运行 [**！ ndiskd**](-ndiskd-netadapter.md) 命令，以查看系统上所有 NIC 驱动程序和 NetAdapters 的列表。 在下面的示例中，查找名为 Realtek PCIe GBE 系列控制器 Get-netadapter 示例驱动程序2的 Get-netadapter 的句柄 \# 。 它的句柄为 ffffd1022d048030。

```console
0: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffd1022e8ecae0   ffffd1022d048030    Realtek PCIe GBE Family Controller NetAdapter Sample Driver #2
    ffffd1022ed908e0   ffffd1022e8611a0    Microsoft Kernel Debug Network Adapter
```

通过单击此 Get-netadapter 的句柄，或在命令行上使用其句柄输入 **！ ndiskd** 命令，你可以查看此 get-netadapter 的详细信息，包括其 get-netadapter 对象。 Realtek PCIe GBE 系列控制器 Get-netadapter 示例驱动程序 \# 2 的 get-netadapter 句柄为00002efdd0e5f988。

```console
0: kd> !ndiskd.netadapter ffffd1022d048030


NETADAPTER

    Realtek PCIe GBE Family Controller NetAdapter Sample Driver #2

    Ndis handle        ffffd1022d048030    
    NETADAPTER         00002efdd0e5f988    More information
    WDFDEVICE          00002efdcf45f2f8
    Driver             ffffd1022e8ecae0 - RtEthSample  v0.0
    Network interface  ffffd1022e395a20

    Media type         802.3
    Device instance    PCI\VEN_10EC&DEV_8168&SUBSYS_816810EC&REV_03\4&22bb23f1&0&0038
    Device object      ffffd1022de127f0    More information
    MAC address        00-e0-4c-68-00-8b


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
    Flags              NOT_BUS_MASTER, WDF, DEFAULT_PORT_ACTIVATED,
                       SUPPORTS_MEDIA_SENSE, DOES_NOT_DO_LOOPBACK,
                       MEDIA_CONNECTED
    PnP flags          PM_SUPPORTED, DEVICE_POWER_ENABLED,
                       DEVICE_POWER_WAKE_ENABLE, HARDWARE_DEVICE,
                       NDIS_WDM_DRIVER, WAKE_CAPABLE


IP ADDRESS SUMMARY

    10.137.188.169                         See all IP addresses on this adapter
    fe80::3cad:81bb:5dad:1066


BINDINGS

    Protocol list      Driver              Open               Context           
    MSLLDP             ffffd1023043f6a0    ffffd1022e786a90   ffffd102307465c0
    LLTDIO             ffffd1022c6b7830    ffffd1022ef8cc00   ffffd1022f1e5730
    TCPIP6             ffffd1022e2c7c10    ffffd10230b98310   ffffd102304d9010
    (RASPPPOE)         Not running
    (RDMANDK)          ffffd1022d574a70    Declined with NDIS_STATUS_NOT_RECOGNIZED
    RSPNDR             ffffd1022c71a830    ffffd1022de0cc00   ffffd1022d03f6a0
    TCPIP              ffffd1022e2cbc10    ffffd1022de067f0   ffffd1022d03f010
    NDISUIO            ffffd1022de07670    ffffd1022cd648d0   ffffd10231131970

    Filter list        Driver              Module             Context           
    WFP 802.3 MAC Layer LightWeight Filter-0000
                       ffffd1022e384d70    ffffd1022f271660   ffffd10230cfe2c0
    QoS Packet Scheduler-0000
                       ffffd1022d56f220    ffffd1022f26d660   ffffd10231778700
    WFP Native MAC Layer LightWeight Filter-0000
                       ffffd1022e384ad0    ffffd1022f26b660   ffffd1022ed59c20



MORE INFORMATION

    Driver handlers                        Task offloads
    Power management                       PM protocol offloads
    Pending OIDs
    Pending NBLs                           Receive side throttling
    Wake-on-LAN (WoL)                      Packet filter
    Receive queues                         Receive filtering
    RSS                                    NIC switch
                                           Selective suspend
    NDIS ports                             WMI guids
    Diagnostic log
```

由于 GET-NETADAPTER 对象是一个 WDF 对象，因此单击其控点将导致调试程序运行 [**！ wdfkd**](-wdfkd-wdfhandle.md) 命令，该命令将从 WDF 角度为你显示有关它的详细信息。 若要从网络角度查看有关 GET-NETADAPTER 的更多详细信息，请单击 GET-NETADAPTER 的句柄右侧的 "详细信息" 链接，以使用其句柄运行 **cxadapter** 命令。

```console
0: kd> !ndiskd.cxadapter ffffd1022f1a0720


NETADAPTER

    Miniport           ffffd1022d048030 - Realtek PCIe GBE Family Controller NetAdapter Sample Driver #2
    NETADAPTER         00002efdd0e5f988    
    WDFDEVICE          00002efdcf45f2f8    

    Event Callbacks                        Function pointer   Symbol (if available)
    EvtAdapterCreateTxQueue                fffff80034151508   RtEthSample+1508
    EvtAdapterCreateRxQueue                fffff800341510ec   RtEthSample+10ec

    Show datapath info
    Show NETPOWERSETTINGS info
```

你还可以将此命令与其他参数（如 *-数据路径* ）结合起来，查看此 get-netadapter 的详细信息。

```console
0: kd> !ndiskd.cxadapter ffffd1022f1a0720 -basic -datapath


NETADAPTER

    Miniport           ffffd1022d048030 - Realtek PCIe GBE Family Controller NetAdapter Sample Driver #2
    NETADAPTER         00002efdd0e5f988    
    WDFDEVICE          00002efdcf45f2f8    

    Event Callbacks                        Function pointer   Symbol (if available)
    EvtAdapterCreateTxQueue                fffff80034151508   RtEthSample+1508
    EvtAdapterCreateRxQueue                fffff800341510ec   RtEthSample+10ec


DATAPATH QUEUES

    NETTXQUEUE         ffffd1022f512700
    NETRXQUEUE         ffffd1022cc7b0d0
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[网络适配器 WDF 类扩展 (Cx) ](../netcx/index.md)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!wdfkd.wdfhandle**](-wdfkd-wdfhandle.md)

 

