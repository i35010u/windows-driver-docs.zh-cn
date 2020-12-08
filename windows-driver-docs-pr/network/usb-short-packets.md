---
title: USB 短数据包
description: USB 短数据包
keywords:
- USB 短数据包 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26ad5b7ebd34f25251fcbb334849530f28625f03
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837897"
---
# <a name="usb-short-packets"></a>USB 短数据包





USB 以 USB 数据包的形式传递数据，不应将其与 NDIS 或网络数据包混淆。 USB 终结点发来或发来的 USB 数据包的最大长度限制为终结点描述符的 **wMaxPacketSize** 字段的值。 对于大容量管道，最大数据包大小为64个字节。 由于某些 USB 主机控制器的限制，在流式传输数据) 时，使用较短的 USB 数据包 (例如，使用较少的64个字节）会产生一定的损失。

若要解决此限制，远程 NDIS USB 设备可能会将零字节填充添加到数据消息，以便不会 ([远程 \_ ndis \_ 初始化 \_ 消息](remote-ndis-initialize-msg.md)) 的 **MaxTransferSize** 字段的约束中出现较短的数据包。 最终 [远程 \_ NDIS \_ 数据包 \_ 消息](remote-ndis-packet-msg.md)的 **MessageLength** 字段不包含这些追加的填充字节。

如果设备已传输其上一次可用的远程 \_ NDIS \_ 数据包 \_ 消息 (因此，在设备的队列) 中不再有其他项，则可以接受发送短的 USB 数据包。

如果 \_ \_ 设备发送远程 ndis 数据消息的最后一个远程 ndis 数据包消息 \_ (没有任何零字节填充时间) 以与该终结点的 **wMaxPacketSize** 长度完全相同的 USB 数据包结束，则设备可能会将额外的单字节的零数据包作为传输的附加部分发送。 某些设备实现通过此限制简化。

同样，某些设备端 USB 芯片集不会检测到以 USB 数据包结尾的已接收 USB 传输结束，其长度为该终结点的 **wMaxPacketSize** 。 出于此原因，主机必须向数据传输追加一个单字节的数据包，否则长度将是接收终结点的 **wMaxPacketSize** 的倍数。 USB 远程 NDIS 设备必须容忍追加的字节。 最终 **MessageLength** 远程 \_ NDIS 数据包消息的 MessageLength 字段 \_ \_ 不包含此追加的字节。

 

 





