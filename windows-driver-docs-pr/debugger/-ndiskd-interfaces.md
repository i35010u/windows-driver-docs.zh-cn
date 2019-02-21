---
title: ndiskd.interfaces
description: Ndiskd.interfaces 扩展显示有关网络接口的信息。
ms.assetid: AC458FDF-CCB6-4A65-8C9C-38C436062017
keywords:
- ndiskd.interfaces Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.interfaces
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cd9407a23995113b7fde4e7d613607621d334c01
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547424"
---
# <a name="ndiskdinterfaces"></a>!ndiskd.interfaces


**！ Ndiskd.interfaces**扩展显示有关网络接口的信息。 如果不带任何参数运行此扩展 ！ ndiskd 将显示所有网络接口的列表。

有关网络接口的详细信息，请参阅[NDIS 网络接口](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-network-interfaces2)。

```console
!ndiskd.interfaces [-handle <x>] [-luid <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
网络接口的句柄。

<span id="_______-luid______"></span><span id="_______-LUID______"></span> *-luid*   
[NetLuid](https://msdn.microsoft.com/windows/hardware/drivers/network/net-luid-value) （Net 本地唯一标识符） 的网络接口。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

运行 **！ ndiskd.interfaces**扩展不带任何参数，以查看在系统上的所有网络接口的列表。 在此示例中，查找 intel （） 82579LM 千兆网络连接接口。 其句柄是 ffffdf80139f8a20。

```console
1: kd> !ndiskd.interfaces
    Interface                                                                   
    ffffdf801494fa20 - Microsoft Kernel Debug Network Adapter-WFP Native MAC Layer LightWeight Filter-0000
    ffffdf801494c010 - Microsoft Kernel Debug Network Adapter-QoS Packet Scheduler-0000
    ffffdf801494ba20 - Microsoft Kernel Debug Network Adapter-WFP 802.3 MAC Layer LightWeight Filter-0000
    ffffdf80139b3a20 - Microsoft Kernel Debug Network Adapter
    ffffdf80139f8a20 - Intel(R) 82579LM Gigabit Network Connection
    ffffdf80139baa20 - WAN Miniport (IP)
    ffffdf80139a4a20 - WAN Miniport (IPv6)
    ffffdf80131d0010 - WAN Miniport (Network Monitor)
    ffffdf80131cda20 - WAN Miniport (PPPOE)
    ffffdf80139b6a20 - Software Loopback Interface 1
    ffffdf80139b0a20 - Microsoft ISATAP Adapter
    ffffdf80139ada20 - WAN Miniport (SSTP)
    ffffdf80131cf010 - WAN Miniport (IKEv2)
    ffffdf80139fea20 - WAN Miniport (L2TP)
    ffffdf80139a7a20 - WAN Miniport (PPTP)
    ffffdf80139aaa20 - Microsoft ISATAP Adapter #2
    ffffdf80139fba20 - Teredo Tunneling Pseudo-Interface
```

通过单击接口或通过输入的句柄 **！ ndiskd.interfaces-处理**命令，可以看到有关该接口，包括其标识符信息和其当前状态的详细信息。 在此示例中，可以看到，intel （） 82579LM 千兆网络连接的以太网连接 (其 ifAlias) 并处于连接 MediaConnectUnknown 状态 （因为它已被 Windows 内核调试程序保留供使用）。

```console
1: kd> !ndiskd.interfaces ffffdf80139f8a20


INTERFACE

    Ethernet

    Ndis handle        ffffdf80139f8a20
    IfProvider         ffffdf80131ca8d0 - The NDIS interface provider
    Provider context   ffffdf80139f8a20

    ifType             IF_TYPE_ETHERNET_CSMACD
    Media type         802.3
    Physical medium    802.3
    Access type        BROADCAST
    Direction type     SEND_AND_RECEIVE
    Connection type    DEDICATED

    ifConnectorPresent No

    Network            ffffdf80139b8900 - [Unnamed network]
    Compartment        ffffdf80139b9940 - Compartment #1


IDENTIFIERS

    ifAlias            Ethernet
    ifDescr            Intel(R) 82579LM Gigabit Network Connection
    ifName (NET_LUID)  06:8001
    ifPhysAddress      18-03-73-c1-e8-72

    ifIndex            0n14
    ifGuid             cbddfde1-5570-4c65-9d47-52d63abce00c


STATE

    Connected          MediaConnectUnknown
    ifOperStatus       NOT_PRESENT

    Link speed         0 [Speed is not applicable]
    ifMtu              0
    Duplex             UnknownDuplex

    Refer to RFC 2863 for definitions of many of these terms
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[NDIS 网络接口](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-network-interfaces2)

[NET\_LUID 值](https://msdn.microsoft.com/windows/hardware/drivers/network/net-luid-value)

 

 






