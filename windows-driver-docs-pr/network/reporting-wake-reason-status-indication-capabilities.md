---
title: 报告唤醒原因状态指示功能
description: 报告唤醒原因状态指示功能
ms.assetid: A72D04F7-EB09-4B1B-9AF5-7FEBC2514CE9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01595a4a45e6ec441fa339af107be0cc27dad5cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349423"
---
# <a name="reporting-wake-reason-status-indication-capabilities"></a>报告唤醒原因状态指示功能


从开始 NDIS 6.30，微型端口驱动程序必须报告它是否可以发出 NDIS 唤醒原因状态指示 ([**NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)) 来报告唤醒事件由以下项之一引起：

-   网络适配器接收到与 LAN 唤醒 (WOL) 模式匹配的数据包。 这包括与指定的对象标识符 (OID) 组请求通过接收筛选器匹配的数据包的回执[OID\_代\_当前\_数据包\_筛选器](https://msdn.microsoft.com/library/windows/hardware/ff569575)。

    **请注意**  唤醒原因状态指示此类型，网络适配器必须能够保存所接收的数据包。 该驱动程序必须返回的状态指示在接收到的数据包。

     

-   网络适配器检测到特定于媒体的事件，如从 802.11 访问点 (AP) 或移动的宽带 (MB) 短消息服务 (SMS) 消息的接收解除关联。

-   网络适配器检测到不是特定于 WOL 模式的另一个启用了的事件或媒体类型 (*独立于媒体的事件*)。 例如，微型端口驱动程序问题[ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状态指示，指示是否启用网络适配器若要检测媒体连接或断开连接。

**请注意**  支持 NDIS 唤醒原因状态指示是可选的移动宽带 (MB) 微型端口驱动程序。

 

NDIS 时调用的驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数，微型端口驱动程序报告其唤醒原因状态指示功能通过执行以下步骤：

1.  微型端口驱动程序初始化[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构与基础硬件的电源管理功能。

    若要支持唤醒原因状态指示，微型端口驱动程序必须设置的成员[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构，如下所示：

    -   微型端口驱动程序必须指定 NDIS\_PM\_功能\_修订\_2 和 NDIS\_SIZEOF\_NDIS\_PM\_功能\_修订\_修订版本和长度的 2 [ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)内结构的结构**标头**成员。
    -   如果网络适配器可以存储所接收的数据包，导致系统唤醒事件，微型端口驱动程序设置 NDIS\_PM\_唤醒\_数据包\_指示\_内的支持标志**标志**此结构的成员。

        如果设置此标志，网络适配器必须能够保存所接收的数据包，导致适配器以生成唤醒事件。 此外，微型端口驱动程序必须能够执行以下操作与这个数据包后网络适配器将转换为全功率状态：

        -   微型端口驱动程序必须能够通过调用指示数据包[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)。

        -   微型端口驱动程序必须能够发出[ **NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状态指示并且必须通过包含的数据包指示。

    -   微型端口驱动程序集**MaxWoLPacketSaveBuffer**成员添加到的最大大小，以包含导致系统唤醒事件的 WOL 数据包缓冲区的字节为单位。

        值**MaxWoLPacketSaveBuffer**成员必须是小于或等于以字节为单位的最大传输单元 (MTU) 的大小和媒体访问控制 (MAC) 的网络介质标头。 该驱动程序报告通过 OID 的查询请求的 MTU 大小[OID\_代\_最大\_帧\_大小](https://msdn.microsoft.com/library/windows/hardware/ff569598)。

    -   微型端口驱动程序集**SupportedWakeUpEvents**的网络适配器支持，如生成唤醒事件时该适配器将成为连接到网络接口的独立于媒体的唤醒事件。

    -   微型端口驱动程序集**MediaSpecificWakeUpEvents**的网络适配器支持的特定于媒体的唤醒事件。 这些事件包括生成唤醒事件时使用 AP 802.11 适配器将成为解除关联。

2.  微型端口驱动程序初始化[ **NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)结构和集**PowerManagementCapabilitiesEx**成员添加到的地址初始化[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构。

3.  微型端口驱动程序调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数以注册其电源管理功能。 当微型端口驱动程序调用此函数时，它会设置*MiniportAttributes*参数的地址[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)结构。

微型端口驱动程序用于报告唤醒原因状态指示功能的方法基于报告电源管理功能的 NDIS 6.20 方法。 有关此方法的详细信息，请参阅[报告电源管理功能](reporting-power-management-capabilities.md)。

有关适配器初始化过程的详细信息，请参阅[初始化微型端口适配器](initializing-a-miniport-adapter.md)。

有关如何对报表电源管理功能的详细信息，请参阅[报告电源管理功能](reporting-power-management-capabilities.md)。

 

 





