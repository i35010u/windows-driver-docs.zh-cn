---
title: USB 短数据包
description: USB 短数据包
ms.assetid: e59476cf-754e-4550-849f-3aa645defe09
keywords:
- USB 短数据包 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bf6be1c082d5b96a25156a8f0e177e074cad94f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519048"
---
# <a name="usb-short-packets"></a>USB 短数据包





USB USB 数据包，而这不应混淆 NDIS 或网络数据包的形式在网络上传递数据。 USB 数据包到或从 USB 终结点的最大长度的值仅限于**wMaxPacketSize**终结点的描述符字段。 对于批量传输管道的最大数据包大小是 64 字节。 由于某些 USB 主控制器的限制，没有与使用短 USB 数据包 （例如，那些流式处理数据时更少然后 64 字节） 对产生负面影响。

若要解决此限制，远程 NDIS USB 设备可能将附加零字节填充到数据消息，以便短数据包将不会发生 (的约束内**MaxTransferSize**字段[远程\_NDIS\_初始化\_MSG](remote-ndis-initialize-msg.md))。 **MessageLength**字段的最终[远程\_NDIS\_数据包\_MSG](remote-ndis-packet-msg.md)不包括这些附加填充字节。

如果设备具有传输其最后一个可用的远程\_NDIS\_数据包\_MSG （因此不能保留在设备的队列中的详细信息），则它是可以接受将短 USB 数据包发送。

如果最后一个远程\_NDIS\_数据包\_（不带任何零字节填充） 远程 NDIS 设备发送的数据消息的消息结尾其长度正好是一个 USB 数据包**wMaxPacketSize**为此，终结点，则表示设备可能会发送额外的一个字节零个数据包追加过程中传输。 通过此限额，某些设备实现进行了简化。

同样，某些设备端 USB 芯片集未检测到的结尾，长度是一个 USB 数据包接收 USB 传输结束**wMaxPacketSize**该终结点。 出于此原因，主机必须将单字节零个数据包到数据传输，否则会产生，其长度为倍数**wMaxPacketSize**接收终结点。 USB 远程 NDIS 设备必须允许追加的字节。 **MessageLength**字段的最后一个远程\_NDIS\_数据包\_消息不包括此追加的字节。

 

 





