---
title: MB USSD 操作
ms.assetid: 49D106BD-F938-4BF8-88EE-A4D0F0E2722A
description: 描述要发送和接收消息使用的 MB 设备的非结构化补充服务数据 (USSD) 功能的操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6409c8be13c890dac5d8c0c156cfc62c2ad7a2dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367579"
---
# <a name="mb-ussd-operations"></a>MB USSD 操作


本主题描述的操作来发送和接收消息使用的 MB 设备的非结构化补充服务数据 (USSD) 功能。

是可选的 USSD 支持以及何时支持才 GSM 网络上可用。 支持 USSD 的微型端口驱动程序必须设置 WWAN\_CTRL\_CAPS\_USSD 作为的一部分的功能标志**WwanControlCaps**隶属[ **WWAN\_设备\_CAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff571204)结构处理时[OID\_WWAN\_设备\_CAPS](https://msdn.microsoft.com/library/windows/hardware/ff569824)请求。 如果微型端口驱动程序不支持 USSD，它们必须不设置此标志，应返回 WWAN\_状态\_否\_设备\_支持所有 USSD 相关 Oid。

MB 驱动程序模型支持以下 USSD 操作：由设备发起的操作：

-   在新创建的 USSD 会话上发送 USSD 消息

-   在新创建的 USSD 会话上发送 USSD 消息

-   现有的 USSD 会话上发送 USSD 消息

-   正在终止 USSD 会话

设备启动的操作的详细信息，请参阅[OID\_WWAN\_USSD](https://msdn.microsoft.com/library/windows/hardware/hh440100)。

网络启动的操作：

-   新创建的 USSD 会话接收 USSD 消息

-   现有的 USSD 会话上接收 USSD 消息

-   终止 USSD 会话

有关网络启动的操作的详细信息，请参阅[ **NDIS\_状态\_WWAN\_USSD**](https://msdn.microsoft.com/library/windows/hardware/hh439822)。

USSD 协议仅允许单个 USSD 会话在任何时间。 设备启动的操作， **RequestType**的成员[ **WWAN\_USSD\_请求**](https://msdn.microsoft.com/library/windows/hardware/hh464138)结构指示的用途请求 OID:

-   **WwanUssdRequestInitiate**用于创建新的 USSD 会话并将所提供的 USSD 字符串发送到网络。 如果 USSD 会话已存在，该驱动程序必须失败的请求类型的事件**WwanUssdEventOtherLocalClient**。 USSD 字符串必须存在。 例如，长度必须介于 1 到 160 字节之间。

-   **WwanUssdRequestContinue**用于现有的会话上发送 USSD 字符串。 USSD 字符串必须存在。 例如，长度必须介于 1 到 160 字节之间。

-   **WwanUssdRequestCancel**用于终止现有会话。 该驱动程序必须使用类型的事件响应**WwanUssdEventTerminated**，即使没有会话已存在 （这可能会发生在从网络和本地客户端会话的并发版本期间）。 必须对此请求; 忽略 USSD 字符串的内容字符串长度设置为零以指示不不存在任何 USSD 字符串。

为网络启动的操作， **EventType**的成员[ **WWAN\_USSD\_事件**](https://msdn.microsoft.com/library/windows/hardware/hh464136)结构指示高级别目的指示：

-   事件**WwanUssdEventNoActionRequired**网络启动的 USSD 通知，或者在移动启动操作之后不需要任何进一步的信息，则将使用。 事件**WwanUssdEventActionRequired**网络启动的 USSD 请求，或者在移动启动操作之后需要进一步的信息，则将使用。 这两个事件需要非空 USSD 字符串必须存在。 **SessionState**成员将用来指示 USSD 字符串是 USSD 会话的第一条消息; 它必须设置为**WwanUssdSessionStateNew**网络的第一条消息启动的 USSD 会话进出**WwanUssdSessionStateExisting**在所有其他情况下。

-   事件**WwanUssdEventActionRequired**还指示，该会话仍处于打开状态。 所有其他事件指示会话已关闭。

-   事件**WwanUssdEventNoActionRequired**并**WwanUssdEventActionRequired**是包含 USSD 字符串的唯一事件。 所有其他事件必须设置 USSD 字符串长度为 0，表示该字符串不存在。 值**SessionState**成员将被忽略，如果不有任何字符串。

-   事件**WwanUssdEventTerminated**用于指示 USSD 会话已终止。

-   事件**WwanUssdEventOtherLocalClient**用于指示无法建立新的 USSD 会话，因为没有已打开的会话。 这包括对 MB 堆栈，如在 SIM USSD 会话终止不可见的会话。

-   事件**WwanUssdEventOperationNotSupported**用于指示在上一个请求不支持由驱动程序或设备。

-   事件**WwanUssdEventNetworkTimeOut**用来指示会话已关闭由于会话超时的网络或本地。 驱动程序或设备负责确定为实现特定超时之后不活动的 USSD 会话超时。

 

 





