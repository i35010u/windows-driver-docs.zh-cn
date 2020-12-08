---
title: ndiskd.ifstacktable
description: Ifstacktable 扩展 (ifStackTable) 中显示网络接口堆栈。
keywords:
- ndiskd ifstacktable Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ifstacktable
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 28186ba1bf7c67d81f103fed320291c595080f1b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803319"
---
# <a name="ndiskdifstacktable"></a>!ndiskd.ifstacktable


**！ Ndiskd ifstacktable** (ifstacktable) 中显示网络接口堆栈。

有关接口堆栈的详细信息，请参阅 [维护网络接口堆栈](../network/maintaining-a-network-interface-stack.md)。

```console
!ndiskd.ifstacktable 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


此扩展没有参数。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

运行 **！ ndiskd. ifstacktable** 命令以查看 ifstacktable。

```console
3: kd> !ndiskd.ifstacktable


INTERFACE STACK TABLE

    Lower interface    Lower IfIndex       Higher IfIndex     Higher interface  
    ffffdf80139b3a20   6                   15                 ffffdf801494fa20
    ffffdf801494fa20   15                  16                 ffffdf801494c010
    ffffdf801494c010   16                  17                 ffffdf801494ba20
```

NDIS 为 NDIS 微型端口适配器、NDIS 1.x 筛选器中间驱动程序和 NDIS 筛选器模块维护堆栈表，而 [NDIS MUX 中间驱动](../network/ndis-mux-intermediate-drivers.md) 程序驱动程序则需要指定虚拟微型端口接口和协议下限接口之间的内部接口关系。 因此，在安装了更复杂 MUX 驱动程序的系统中，ifStackTable 可能非常有用。

由于此示例系统上没有安装 NDIS MUX 中间驱动程序，ifStackTable 仅显示 NDIS 提供的堆栈关系。 在下面的示例中，单击第三行的下一个接口的句柄 (处理 ffffdf801494c010，Lower IfIndex 16) 显示 QoS 数据包计划程序的接口。

```console
3: kd> !ndiskd.interface ffffdf801494c010


INTERFACE

    [Zero-length string]

    Ndis handle        ffffdf801494c010 
    IfProvider         ffffdf80131ca8d0 - The NDIS interface provider
    NDIS filter        ffffdf801494dc70 - Microsoft Kernel Debug Network Adapter-QoS Packet Scheduler-0000

    ifType             IF_TYPE_ETHERNET_CSMACD
    Media type         802.3
    Physical medium    NdisPhysicalMediumOther
    Access type        BROADCAST
    Direction type     SEND_AND_RECEIVE
    Connection type    DEDICATED

    ifConnectorPresent No

    Network            ffffdf80139b8900 - [Unnamed network]
    Compartment        ffffdf80139b9940 - Compartment #1


IDENTIFIERS

    ifAlias            [Zero-length string]
    ifDescr            Microsoft Kernel Debug Network Adapter-QoS Packet Scheduler-0000
    ifName (NET_LUID)  06:01
    ifPhysAddress      18-03-73-c1-e8-72

    ifIndex            0n16
    ifGuid             fc2a0ae1-b103-11e6-b724-806e6f6e6963


STATE

    Connected          Connected
    ifOperStatus       DORMANT
    ifOperStatusFlags  DORMANT_PAUSED

    Link speed         1000000000 (1 Gbps)
    ifMtu              0n1500
    Duplex             FullDuplex

    Refer to RFC 2863 for definitions of many of these terms
```

继续同一个示例，单击第三行 (处理 ffffdf801494ba20、较高 IfIndex 17) 的接口的句柄，显示 WFP 802.3 MAC 层轻型筛选器的接口。

```console
3: kd> !ndiskd.interface ffffdf801494ba20


INTERFACE

    [Zero-length string]

    Ndis handle        ffffdf801494ba20    [type it]
    IfProvider         ffffdf80131ca8d0 - The NDIS interface provider
    NDIS filter        ffffdf801494c670 - Microsoft Kernel Debug Network Adapter-WFP 802.3 MAC Layer LightWeight Filter-0000

    ifType             IF_TYPE_ETHERNET_CSMACD
    Media type         802.3
    Physical medium    NdisPhysicalMediumOther
    Access type        BROADCAST
    Direction type     SEND_AND_RECEIVE
    Connection type    DEDICATED

    ifConnectorPresent No

    Network            ffffdf80139b8900 - [Unnamed network]
    Compartment        ffffdf80139b9940 - Compartment #1


IDENTIFIERS

    ifAlias            [Zero-length string]
    ifDescr            Microsoft Kernel Debug Network Adapter-WFP 802.3 MAC Layer LightWeight Filter-0000
    ifName (NET_LUID)  06:02
    ifPhysAddress      18-03-73-c1-e8-72

    ifIndex            0n17
    ifGuid             fc2a0ae0-b103-11e6-b724-806e6f6e6963


STATE

    Connected          Connected
    ifOperStatus       DORMANT
    ifOperStatusFlags  DORMANT_PAUSED

    Link speed         1000000000 (1 Gbps)
    ifMtu              0n1500
    Duplex             FullDuplex

    Refer to RFC 2863 for definitions of many of these terms
```

这表明 WFP 802.3 MAC 层轻型筛选器位于网络接口堆栈中的 QoS 数据包 Scheudler 筛选器之上。 可以通过运行 [**！ ndiskd. netreport**](-ndiskd-netreport.md) 扩展来确认这一点，该扩展会以可视方式显示网络堆栈。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[维护网络接口堆栈](../network/maintaining-a-network-interface-stack.md)

[NDIS MUX 中间驱动程序](../network/ndis-mux-intermediate-drivers.md)

[**!ndiskd.netreport**](-ndiskd-netreport.md)

 

