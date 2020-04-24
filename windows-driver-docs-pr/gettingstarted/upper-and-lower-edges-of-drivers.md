---
title: 驱动程序的上沿和下沿
description: 参与 I/O 请求的驱动程序序列称为“请求的驱动程序堆栈”。
ms.assetid: EA1C36F4-B9BD-4A9E-A6D4-6B4EC5455030
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f050749d4d784809238816968c1f79dc0fd76247
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "67385173"
---
# <a name="upper-and-lower-edges-of-drivers"></a>驱动程序的上沿和下沿


参与 I/O 请求的驱动程序序列称为“请求的驱动程序堆栈”。 驱动程序可以调用堆栈中低层驱动程序的上沿。 驱动程序也可以调用堆栈中高层驱动程序的下沿。

在阅读本主题之前，应了解[设备节点和设备堆栈](device-nodes-and-device-stacks.md)以及[驱动程序堆栈](driver-stacks.md)中介绍的理念。

I/O 请求首先由驱动程序堆栈中的顶层驱动程序处理，然后由下一层驱动程序处理，依此类推，直到完全处理请求。

当驱动程序实现一组高层驱动程序可以调用的函数时，该组函数称为“驱动程序的上沿”  ，或者“驱动程序的上沿接口”  。

当驱动程序实现一组低层驱动程序可以调用的函数时，该组函数称为“驱动程序的下沿”  ，或者“驱动程序的下沿接口”  。

### <a name="span-idaudio_examplespanspan-idaudio_examplespanspan-idaudio_examplespanaudio-example"></a><span id="Audio_example"></span><span id="audio_example"></span><span id="AUDIO_EXAMPLE"></span>音频示例

我们可以想象一个音频微型端口驱动程序位于驱动程序堆栈中音频端口驱动程序的下面。 该端口驱动程序调用微型端口驱动程序的上沿。 微型端口驱动程序调用端口驱动程序的下沿。

![微型端口驱动程序上面的音频端口驱动程序图](images/audiodrvstack.png)

上面的图说明，有时将端口驱动程序想象成位于驱动程序堆栈中的微型端口驱动程序之上是有用的。 因为 I/O 请求首先由端口驱动程序处理，然后再由微型端口驱动程序处理，所以将端口驱动程序视为高于微型端口驱动程序是合理的。 但是，请记住（微型端口，端口）驱动程序对通常位于设备堆栈中的单层，如此处所示。

![包含（微型端口/端口）对的设备堆栈图](images/upperloweredge01.png)

请注意，设备堆栈  不同于驱动程序堆栈  。 有关这些术语的定义，以及对于一对驱动程序如何形成单一 WDM 驱动程序（在设备堆栈中占用一层）的讨论，请参阅[微型驱动程序和驱动程序对](minidrivers-and-driver-pairs.md)。

下面是绘制相同设备节点和设备堆栈图的另一种方法：

![端口驱动程序在微型端口上面的设备堆栈图](images/upperloweredge02.png)

在上图中我们看到，（微型端口，端口）对形成与设备堆栈中单一设备对象 (FDO) 关联的单一 WDM 驱动程序；即，（微型端口，端口）对仅占用设备堆栈中的一层。 但我们也看到微型端口和端口驱动程序之间的垂直关系。 端口驱动程序显示在微型端口驱动程序的上面，这表示端口驱动程序首先处理 I/O 请求，然后调用微型端口驱动程序以进行其他处理。

关键点在于，当端口驱动程序调用微型端口驱动程序的上沿接口时，这不同于将 I/O 请求向下传递到设备堆栈。 在驱动程序堆栈（不是设备堆栈）中，可以选择在微型端口驱动程序的上面绘制端口驱动程序，但这并非意味着该端口驱动程序位于设备堆栈中微型驱动程序的上面。

### <a name="span-idndis_examplespanspan-idndis_examplespanspan-idndis_examplespanndis-example"></a><span id="NDIS_example"></span><span id="ndis_example"></span><span id="NDIS_EXAMPLE"></span>NDIS 示例

有时，驱动程序直接调用低层驱动程序的上沿。 例如，假设 [TCP/IP 协议驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/introduction-to-ndis-protocol-drivers)在驱动程序堆栈中位于 [NDIS](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-drivers) 微型端口驱动程序的上面。 该微型端口驱动程序将实现一组 *MiniportXxx* 函数，它们形成微型端口驱动程序的上沿。 我们称之为 TCP/IP 协议驱动程序绑定  到 NDIS 微型端口驱动程序的上沿。 但 TCP/IP 驱动程序不直接调用 MiniportXxx  函数。 而是调用 NDIS 库中的函数，然后这些函数再调用 MiniportXxx  函数。

![TCP/IP 和 NDIS 微型端口堆栈图](images/upperloweredge03.png)

上图显示了驱动程序堆栈。 下面是相同驱动程序的另一个视图。

![用于网卡的设备堆栈图](images/upperloweredge04.png)

上图显示了用于网络接口卡 (NIC) 的设备节点。 该设备节点位于即插即用 (PnP) 设备树中。 NIC 的设备节点具有一个包含三个设备对象的设备堆栈。 请注意，NDIS 微型端口驱动程序和 NDIS 库是成对工作的。 (MyMiniport.sys, Ndis.sys) 对形成单一 WDM 驱动程序，由功能设备对象 (FDO) 表示。

另请注意，协议驱动程序 Tcpip.sys 不属于 NIC 的设备堆栈。 实际上，Tcpip.sys 根本不是 PnP 设备树的一部分。

## <a name="span-idsummaryspanspan-idsummaryspanspan-idsummaryspansummary"></a><span id="Summary"></span><span id="summary"></span><span id="SUMMARY"></span>摘要


术语“上沿”  和“下沿”  用于描述堆栈中的驱动程序用来相互通信的接口。 [*驱动程序堆栈*](driver-stacks.md)不同于[*设备堆栈*](device-nodes-and-device-stacks.md)。 在驱动程序堆栈中垂直显示的两个驱动程序可能形成位于设备堆栈中单层上的驱动程序对。 某些驱动程序不是 PnP 设备树的一部分。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[适用于所有驱动程序开发人员的概念](concepts-and-knowledge-for-all-driver-developers.md)

[设备节点和设备堆栈](device-nodes-and-device-stacks.md)

[驱动程序堆栈](driver-stacks.md)

[音频设备](https://docs.microsoft.com/windows-hardware/drivers/audio/portal-audio-ref)

[从 Windows Vista 开始的网络驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570021(v=vs.85))

 

 






