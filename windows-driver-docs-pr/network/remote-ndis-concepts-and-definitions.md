---
title: 远程 NDIS 的概念和定义
description: 远程 NDIS 的概念和定义
ms.assetid: caf01e69-9368-4b9b-a343-ef17a2154bb8
keywords:
- 远程 NDIS WDK 网络，概念
- 远程 NDIS WDK 网络，定义
- 远程 NDIS WDK 网络，控制通道
- 远程 NDIS WDK 网络，数据通道
- 远程 NDIS WDK 网络，暂停
- 控制通道 WDK 网络
- 控制通道 WDK 网络，初始化
- 控制通道 WDK 网络，拆卸
- 数据通道 WDK 网络
- 数据通道 WDK 网络，初始化
- 数据通道 WDK 网络，拆卸
- 远程 NDIS WDK 网络，设备状态
- 设备状态 WDK 网络
- 远程 NDIS WDK 网络，流控制
- 远程 NDIS WDK 网络，重置通信通道
- 通信通道 WDK 网络
- 远程 NDIS WDK 网络，消息封装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ed26ea97e369bcb62f28d2f714b7d06c2bb4e2d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211965"
---
# <a name="remote-ndis-concepts-and-definitions"></a>远程 NDIS 的概念和定义





本部分概述了用于在主机与远程 NDIS 设备之间进行通信的通信通道和下层驱动程序上的远程 NDIS 要求。 本部分还介绍设备状态转换和主要操作（如初始化、停止和重置）。

-   **控制通道**

    控制通道必须可靠，并确保按顺序传递。 它用于除网络数据包传输之外的所有通信。 除了 [远程 \_ ndis \_ 停止 \_ 消息](/previous-versions/ff570613(v=vs.85)) 和远程 ndis 外，所有必需的控制消息都 [ \_ \_ 表示 \_ 状态 \_ 消息](/previous-versions/ff570617(v=vs.85))，即主机启动的请求和响应交换。 设备必须在为每个总线指定的超时期限内响应。

-   **数据通道**

    数据通道仅用于传输网络数据包。 它可能包含多个 subchannels (例如，为适当的总线定义的服务质量) 不同。

-   **初始化和拆卸**

    控件和数据通道按为适当的总线指定的方式进行初始化和设置。 主机向远程 NDIS 设备发送 [远程 \_ ndis \_ 初始化 \_ 消息](/previous-versions/ff570624(v=vs.85)) 消息。 远程 NDIS 设备提供有关其类型 (无连接或面向连接的) 、受支持的介质，以及响应消息 [远程 \_ NDIS \_ 初始化 \_ CMPLT](/previous-versions/ff570621(v=vs.85))中的版本的信息。

    主机或远程 NDIS 设备可以通过 [远程 \_ ndis \_ 暂停 \_ 消息](/previous-versions/ff570613(v=vs.85)) 消息来拆卸信道。 收到此消息时，将丢弃所有未完成的请求和数据包。

-   **设备状态定义**

    在执行总线级别的初始化后，设备被称为 RNDIS 未初始化。 接收到 [远程 \_ ndis \_ initialize \_ 消息](/previous-versions/ff570624(v=vs.85)) 并使用远程 \_ NDIS \_ initialize CMPLT （ \_ 状态为 RNDIS 状态成功）进行响应时 \_ \_ ，设备将进入 RNDIS 初始化状态。

    接收远程 \_ NDIS \_ SET MSG 后 \_ ，为 OID 生成当前数据包筛选器指定一个非零筛选器值 \_ \_ \_ \_ ，设备将进入 RNDIS 数据初始化状态。

    处于 RNDIS 状态时，如果为 \_ \_ OID 生成 \_ 当前数据包筛选器指定零筛选器值，则对远程 NDIS SET MSG 的接收将 \_ \_ \_ \_ 强制设备恢复到 RNDIS 的状态。

    远程 \_ NDIS \_ 暂停 \_ 消息或总线级断开连接或任何时候都可以进行硬重置会强制设备处于 RNDIS 未初始化状态。

-   **Halt**

    无论何时设备处于 RNDIS 初始化或 RNDIS 数据初始化状态，主机都可以通过 \_ 向设备发送远程 ndis \_ 停止消息来终止设备的远程 ndis 功能 \_ 。

-   **重置通信通道**

    发生错误（如消息超时）时，将重置信道。 当设备处于 RNDIS 初始化状态时，主机可能会通过将消息 " [远程 \_ NDIS \_ 重置 \_ ](/previous-versions/ff570648(v=vs.85)) 消息" 发送到设备，并在设备完成重置后发送响应消息，随时启动重置。 例如，当发生错误（如消息超时）时，主机可能会启动重置。

    请注意，这是一个软重置，其中任何句柄 (例如，面向连接的设备的 VCs) 在重置后仍然有效。 在重置过程中，远程 NDIS 设备将丢弃所有未完成的请求和数据包。 远程设备可能会重置其某些硬件组件，但会使信道保持不变。

    如果远程 NDIS 设备执行重新启动，则此事件相当于 "删除"，然后是 "添加" 即插即用事件。 主机 NDIS 微型端口驱动程序将暂停并删除，并将添加并启动一个新的实例。 将重新执行所有总线级别和远程 NDIS 初始化。 当出现严重的设备故障时，远程 NDIS 设备可能会重新启动。

-   **流控制**

    远程 NDIS 设备可能需要运动控制，以防止主机用数据包溢出其数据缓冲区。 任何流控制规定或要求都是特定于总线的。

-   **数字字节排序**

    远程 NDIS 消息中的所有数字值都必须采用小字节序格式编码 (最小字节数优先) 。

-   **NDIS 消息封装**

    不存在用于将 NDIS 消息封装在本机总线消息或基元中的方式的远程 NDIS 规范。

 

