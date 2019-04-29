---
title: 数据通道特征
description: 数据通道特征
ms.assetid: 3e178d82-32de-468c-8175-4b0c2684be76
keywords:
- 大容量 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa88c38ed4c0c2ad4dcbe6f12951df8196d42d60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362328"
---
# <a name="data-channel-characteristics"></a>数据通道特征





设备的数据通道组成*大容量*中的 IN 和 OUT 终结点*数据类*接口。

一个可能包含单个 USB 数据传输在任一方向[远程\_NDIS\_数据包\_MSG](remote-ndis-packet-msg.md)或更长的 multipacket 消息。

USB 传输从主机到设备发送数据消息是标准的 USB 批量传输到数据类接口的大容量 OUT 终结点。

USB 传输将数据消息从设备发送到该主机是中的数据类接口的大容量在终结点的标准 USB 大容量复制。 主机将所指示的字节数最多读取*MaxTransferSize*字段[远程\_NDIS\_初始化\_MSG](remote-ndis-initialize-msg.md)，这将是不应超过0x4000 USB 1.1 设备的字节数。

 

 





