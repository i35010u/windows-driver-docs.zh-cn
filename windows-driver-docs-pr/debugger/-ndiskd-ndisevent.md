---
title: ndiskd.ndisevent
description: ！ Ndiskd.ndisevent 扩展显示 NDIS 调试事件日志。
ms.assetid: E042CA22-6521-4DD4-9396-39EC587706D6
keywords:
- ndiskd.ndisevent Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisevent
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d48a4e9e416cf92995ba3f789e62e6b1d2711659
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335952"
---
# <a name="ndiskdndisevent"></a>!ndiskd.ndisevent


**请注意**  第三方网络驱动程序开发人员不应手动使用此扩展命令。 你可以运行它以查看其显示的信息，但不能重复使用它提供了您的驱动程序的详细信息。

 

**！ Ndiskd.ndisevent**扩展显示 NDIS 调试事件日志。

```console
!ndiskd.ndisevent [-handle <x>] [-tagtype <str>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 事件日志的句柄。

<span id="_______-tagtype______"></span><span id="_______-TAGTYPE______"></span> *-tagtype*   
标记的枚举类型。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

若要查看网络适配器的事件日志的输出 ！ ndiskd 中提供了链接到它的状态部分[ **！ ndiskd.netadapter** ](-ndiskd-netadapter.md)输出。 这是比手动方法来查找事件日志的句柄从微型端口块和使用的运行更容易 **！ ndiskd.ndisevent**扩展。

首先，输入 **！ ndiskd.netadapter**命令不带任何参数，以查看在系统上的网络适配器和微型端口驱动程序的列表。 在以下示例中，查找该句柄 Marvell AVASTAR 无线 AC 网络控制器 ffffc804b9e6f1a0 的。

```console
1: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffc804af2e3710   ffffc804b9e6f1a0    Marvell AVASTAR Wireless-AC Network Controller
    ffffc804b99b9020   ffffc804b9c301a0    WAN Miniport (Network Monitor)
    ffffc804b99b9020   ffffc804b9c2a1a0    WAN Miniport (IPv6)
    ffffc804b99b9020   ffffc804b8a8a1a0    WAN Miniport (IP)
    ffffc804ae9d7020   ffffc804b9ceb1a0    WAN Miniport (PPPOE)
    ffffc804b9ca5900   ffffc804b9e601a0    WAN Miniport (PPTP)
    ffffc804b99dc720   ffffc804b99b01a0    WAN Miniport (L2TP)
    ffffc804b86581b0   ffffc804b9c6c1a0    WAN Miniport (IKEv2)
    ffffc804ad4a7250   ffffc804b99651a0    WAN Miniport (SSTP)
    ffffc804b11c4020   ffffc804b85821a0    Microsoft ISATAP Adapter
    ffffc804b11c4020   ffffc804b71731a0    Microsoft ISATAP Adapter #2
    ffffc804ad725020   ffffc804b05e71a0    Surface Ethernet Adapter #2
    ffffc804b0bf0020   ffffc804b0c011a0    Bluetooth Device (Personal Area Network)
    ffffc804aef695e0   ffffc804aed331a0    TAP-Windows Adapter V9
```

现在，单击该 NetAdapter 的链接，或输入 **！ ndiskd.netadapter-处理**命令以查看其详细信息。 查找到的状态部分中的设备即插即用字段右侧的"显示状态历史记录"链接。

```console
1: kd> !ndiskd.netadapter ffffc804b9e6f1a0


MINIPORT

    Marvell AVASTAR Wireless-AC Network Controller

    Ndis handle        ffffc804b9e6f1a0
    Ndis API version   v6.50
    Adapter context    ffffc804af3b1100
    Driver             ffffc804af2e3710 - mrvlpcie8897  v1.0
    Network interface  ffffc804aea60a20

    Media type         802.3
    Physical medium    NdisPhysicalMediumUnspecified
    Device instance    PCI\VEN_11AB&DEV_2B38&SUBSYS_045E0001&REV_00\4&379f07b2&0&00E0
    Device object      ffffc804b9e6f050    More information
    MAC address        c0-33-5e-13-22-f7


STATE

    Miniport           INITIALIZING
    Device PnP         ADDED               Show state history
    Datapath           Normal
    Operational status DOWN
    Operational flags  [No flags set]
    Admin status       ADMIN_UP
    Media              MediaConnectUnknown
    Power              D0
    References         1                   Show detail
    Total resets       0
    Pending OID        None
    Flags              IN_INITIALIZE, NOT_BUS_MASTER, DEFAULT_PORT_ACTIVATED,
                       NOT_SUPPORTS_MEDIA_SENSE, DOES_LOOPBACK, MEDIA_CONNECTED
    PnP flags          PM_SUPPORTED, RECEIVED_START, HARDWARE_DEVICE


WDI

    This system supports WDI.
    Learn more about the associated WDI state


BINDINGS

    Protocol list      Driver              Open               Context           
    No protocols are bound to this miniport

    Filter list        Driver              Module             Context           
    No filters are bound to this miniport



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

现在可以单击"显示状态历史记录"链接或使用网络适配器的句柄输入 **！ ndiskd.netadapter-处理的日志**命令，将显示此微型端口的微型端口驱动程序即插即用事件日志。

```console
1: kd> !ndiskd.netadapter ffffc804b9e6f1a0 -log


MINIPORT PM & PNP EVENTS

    Event              Timestamp           (most recent event at bottom)        
    DeviceAdded
                       13 ms later
    DeviceStart
                       Mon Mar 20 21:27:07.106 2017 (UTC - 7:00) Now?

    Set a breakpoint on the next event
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

 

 






