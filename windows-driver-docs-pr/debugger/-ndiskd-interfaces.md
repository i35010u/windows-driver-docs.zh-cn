---
title: ndiskd 接口
description: Ndiskd 扩展显示有关网络接口的信息。
ms.assetid: AC458FDF-CCB6-4A65-8C9C-38C436062017
keywords:
- ndiskd Windows 调试
ms.date: 06/15/2020
topic_type:
- apiref
api_name:
- ndiskd.interfaces
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3bf85177d4cee8d2c062e7d1cedfe543d5a7fc8f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216770"
---
# <a name="ndiskdinterfaces"></a>!ndiskd.interfaces

**！ Ndiskd**扩展显示有关网络接口的信息。 如果运行不带参数的扩展，！ ndiskd 将显示所有网络接口的列表。

有关网络接口的详细信息，请参阅 [NDIS 网络接口](../network/ndis-network-interfaces2.md)。

```console
!ndiskd.interfaces -handle <x> [-luid <x>]
```

## <a name="parameters"></a>参数

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
网络接口的可选句柄。

<span id="_______-luid______"></span><span id="_______-LUID______"></span>*-luid*   
[NetLuid](../network/net-luid-value.md) (网络接口的本地唯一标识符) 。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

运行不带参数的 **！ ndiskd** 扩展，以查看系统上所有网络接口的列表。 在此示例中，查找 Intel (R) 82579LM 千兆网络连接接口。 它的句柄为 ffffdf80139f8a20。

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

通过单击接口的句柄或输入 **！ ndiskd** 命令，你可以查看有关该接口的详细信息，包括其标识符信息及其当前状态。 在此示例中，你可以看到 Intel (R) 82579LM 千兆网络连接是 (其 ifAlias) 的以太网连接，并且它的连接 (处于 MediaConnectUnknown 状态，因为它已保留供 Windows 内核调试器) 使用。

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

## <a name="see-also"></a>另请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0) **](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[NDIS 网络接口](../network/ndis-network-interfaces2.md)

[NET \_ LUID 值](../network/net-luid-value.md)