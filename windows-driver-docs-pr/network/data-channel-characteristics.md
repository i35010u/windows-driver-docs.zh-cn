---
title: 数据通道特征
description: 数据通道特征
keywords:
- 批量 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3c27b92bce117b6f59ca6b7618e68124ea78014
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826961"
---
# <a name="data-channel-characteristics"></a>数据通道特征





设备的数据通道包含 *数据类* 接口中的 *批量* 输入和输出终结点。

任意一个方向的单个 USB 数据传输可能由单个 [远程 \_ NDIS \_ 数据包 \_ 消息](remote-ndis-packet-msg.md) 或较长的 multipacket 消息组成。

将数据消息从主机发送到设备的 USB 传输是向数据类接口的大容量终结点进行的标准 USB 大容量传输。

将数据消息从设备发送到主机的 USB 传输是从数据类接口的大容量终结点进行的标准 USB 大容量传输。 主机将读取到 [远程 \_ NDIS \_ 初始化 \_ 消息](remote-ndis-initialize-msg.md)的 *MaxTransferSize* 字段所指示的字节数，这将不会超过 USB 1.1 设备的0x4000 字节。

 

 





