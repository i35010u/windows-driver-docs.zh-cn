---
title: ndiskd.ifstacktable
description: Ndiskd.ifstacktable 扩展将显示网络接口堆栈表 (ifStackTable)。
ms.assetid: 8166C088-9366-49C4-9C3A-0089807352A9
keywords:
- ndiskd.ifstacktable Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ifstacktable
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4bac729e35a6f350485237b749f28d409f5fbe19
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336016"
---
# <a name="ndiskdifstacktable"></a>!ndiskd.ifstacktable


**！ Ndiskd.ifstacktable**扩展将显示网络接口堆栈表 (ifStackTable)。

有关接口堆栈表的详细信息，请参阅[维护网络界面栈](https://msdn.microsoft.com/windows/hardware/drivers/network/maintaining-a-network-interface-stack)。

```console
!ndiskd.ifstacktable 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


此扩展没有任何参数。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

运行 **！ ndiskd.ifstacktable**命令来查看 ifStackTable。

```console
3: kd> !ndiskd.ifstacktable


INTERFACE STACK TABLE

    Lower interface    Lower IfIndex       Higher IfIndex     Higher interface  
    ffffdf80139b3a20   6                   15                 ffffdf801494fa20
    ffffdf801494fa20   15                  16                 ffffdf801494c010
    ffffdf801494c010   16                  17                 ffffdf801494ba20
```

NDIS 维护 NDIS 微型端口适配器，NDIS 5.x 筛选器中间驱动程序，在堆栈表和 NDIS 筛选器模块，而[NDIS MUX 中间驱动程序](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-mux-intermediate-drivers)驱动程序所需指定的内部接口关系虚拟微型端口接口和协议之间降低接口。 因此，ifStackTable 可能适用于与更复杂 MUX 驱动程序安装在系统中看到的界面堆栈关系。

由于未安装在此示例中的系统上的 NDIS 中间 MUX 驱动程序，ifStackTable 仅显示了 NDIS 已提供的堆栈关系。 在以下示例中，单击句柄上的第三行 (句柄 ffffdf801494c010，较低 IfIndex 16) 较低的接口显示接口的 QoS 数据包计划程序。

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

继续同一个示例中，单击该句柄，第三行 (句柄 ffffdf801494ba20，更高版本 IfIndex 17) 的更高版本接口显示接口的 WFP 802.3 MAC 层轻型筛选器。

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

这将显示 WFP 802.3 MAC 层轻型筛选器位于网络界面栈中的 QoS 数据包 Scheudler 筛选器的上面。 你可以通过运行确认这一点[ **！ ndiskd.netreport** ](-ndiskd-netreport.md)扩展，其中显示了网络堆栈以可视方式。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[维护网络接口堆栈](https://msdn.microsoft.com/windows/hardware/drivers/network/maintaining-a-network-interface-stack)

[NDIS MUX 中间驱动程序](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-mux-intermediate-drivers)

[**!ndiskd.netreport**](-ndiskd-netreport.md)

 

 






