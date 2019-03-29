---
title: ndiskd.cxadapter
description: Ndiskd.cxadapter 扩展显示有关 NETADAPTER 对象的信息。
ms.assetid: 5BE91B1C-9795-4E2C-834A-B7424FF1FCDB
keywords:
- ndiskd.cxadapter Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.cxadapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c84337a548d858c21f9fcf3938bb2d02441c654b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566287"
---
# <a name="ndiskdcxadapter"></a>!ndiskd.cxadapter


**！ Ndiskd.cxadapter**扩展显示 NETADAPTER 对象有关的信息。

有关网络适配器 WDF 类扩展 (NetAdapterCx) 的详细信息，请参阅[网络适配器 WDF 类扩展 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)。

```console
!ndiskd.cxadapter [-handle <x>] [-basic] [-power] [-datapath] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 NETADAPTER 句柄。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
显示基本信息。

<span id="_______-power______"></span><span id="_______-POWER______"></span> *-power*   
显示有关 NETADAPTER NETPOWERSETTINGS 对象的信息。

<span id="_______-datapath______"></span><span id="_______-DATAPATH______"></span> *-datapath*   
显示有关数据路径队列的信息。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

若要获取的 NETADAPTER 对象的句柄，首次运行[ **！ ndiskd.netadapter** ](-ndiskd-netadapter.md)命令，查看在系统上的所有 NIC 驱动程序和 NetAdapters 列表。 在以下示例中，查找该句柄 NetAdapter 名为 Realtek PCIe GBE 系列控制器 NetAdapter 示例驱动程序\#2。 其句柄是 ffffd1022d048030。

```console
0: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffd1022e8ecae0   ffffd1022d048030    Realtek PCIe GBE Family Controller NetAdapter Sample Driver #2
    ffffd1022ed908e0   ffffd1022e8611a0    Microsoft Kernel Debug Network Adapter
```

通过单击此 NetAdapter 句柄上或通过输入 **！ ndiskd.netadapter-处理**命令与命令行上其句柄可以用于此 NetAdapter，包括其 NETADAPTER 对象查看详细信息。 Realtek PCIe GBE 系列控制器 NetAdapter 示例驱动程序\#2 的 NETADAPTER 句柄是 00002efdd0e5f988。

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

由于 NETADAPTER 对象是 WDF 对象，单击其句柄将导致调试器运行[ **！ wdfkd.wdfhandle** ](-wdfkd-wdfhandle.md)命令，这将让你从 WDF 角度来看有关它的详细信息。 若要查看有关从网络角度来看 NETADAPTER 更详细信息，请单击 NETADAPTER 的句柄的权限，若要运行的"详细信息"链接 **！ ndiskd.cxadapter**命令和其句柄。

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

您也可以组合此命令的其他参数，如*的数据路径*若要查看此 NETADAPTER 的详细信息。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[网络适配器 WDF 类扩展 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!wdfkd.wdfhandle**](-wdfkd-wdfhandle.md)

 

 






