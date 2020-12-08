---
title: MB USSD 操作
description: 描述使用非结构化补充服务数据发送和接收消息的操作 (USSD) MB 设备的功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee320534d46d95e0a3ca3f59b7bab08c157eb9d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815945"
---
# <a name="mb-ussd-operations"></a>MB USSD 操作


本主题介绍使用非结构化补充服务数据发送和接收消息的操作， (USSD) MB 设备的功能。

USSD 支持是可选的，支持时仅适用于 GSM 网络。 处理 OID wwan 设备 cap 请求时，支持 USSD 的微型端口驱动程序必须将 WWAN " \_ CTRL + \_ cap \_ USSD" 功能标志设置为 [**wwan \_ 设备 \_ cap**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps)结构的 **WwanControlCaps** 成员的一部分。 [ \_ \_ \_](./oid-wwan-device-caps.md) 如果微型端口驱动程序不支持 USSD，则它们不能设置此标志，并且应返回 WWAN \_ 状态 " \_ \_ \_ 对于所有 USSD 相关的 oid 无设备支持"。

MB 驱动程序模型支持下列 USSD 操作：设备启动的操作：

-   在新创建的 USSD 会话上发送 USSD 消息

-   在新创建的 USSD 会话上发送 USSD 消息

-   在现有的 USSD 会话上发送 USSD 消息

-   正在终止 USSD 会话

有关设备启动的操作的详细信息，请参阅 [OID \_ WWAN \_ USSD](./oid-wwan-ussd.md)。

网络启动的操作：

-   接收新创建的 USSD 会话上的 USSD 消息

-   在现有的 USSD 会话中接收 USSD 消息

-   终止 USSD 会话

有关网络启动的操作的详细信息，请参阅 [**NDIS \_ 状态 \_ WWAN \_ USSD**](./ndis-status-wwan-ussd.md)。

USSD 协议将随时允许单个 USSD 会话。 对于设备启动的操作， [**WWAN \_ USSD \_ 请求**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_ussd_request)结构的 **RequestType** 成员表明请求 OID 的用途：

-   **WwanUssdRequestInitiate** 用于创建新的 USSD 会话，并将提供的 USSD 字符串发送到网络。 如果已存在 USSD 会话，则驱动程序必须将请求的 **WwanUssdEventOtherLocalClient** 类型的事件失败。 必须存在 USSD 字符串。 例如，长度必须介于1到160个字节之间。

-   **WwanUssdRequestContinue** 用于在现有会话上发送 USSD 字符串。 必须存在 USSD 字符串。 例如，长度必须介于1到160个字节之间。

-   **WwanUssdRequestCancel** 用于终止现有会话。 驱动程序必须使用类型为 **WwanUssdEventTerminated** 的事件进行响应，即使会话不存在 (这可能会在从网络和本地客户端) 在会话的并发发布期间发生。 对于此请求，必须忽略 USSD 字符串的内容;字符串长度设置为零，以指示没有 USSD 字符串。

对于网络启动的操作， [**WWAN \_ USSD \_ 事件**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_ussd_event)结构的 **事件** 的成员表示指示的高级目的：

-   事件 **WwanUssdEventNoActionRequired** 用于网络启动的 USSD 通知，或在移动启动操作后不需要其他信息时使用。 事件 **WwanUssdEventActionRequired** 用于网络启动的 USSD 请求，或在移动启动操作后需要更多的信息时使用。 这两个事件都要求存在非空的 USSD 字符串。 **SessionState** 成员用于指示 USSD 字符串是否为 USSD 会话的第一条消息;对于网络启动的 USSD 会话的第一条消息，必须将其设置为 **WwanUssdSessionStateNew** ，并在所有其他情况下将其设置为 **WwanUssdSessionStateExisting** 。

-   事件 **WwanUssdEventActionRequired** 还指示该会话仍处于打开状态。 所有其他事件都指示会话已关闭。

-   事件 **WwanUssdEventNoActionRequired** 和 **WWANUSSDEVENTACTIONREQUIRED** 是包含 USSD 字符串的唯一事件。 所有其他事件都必须将 USSD 字符串的长度设置为0，以指示该字符串不存在。 如果不存在字符串，则忽略 **SessionState** 成员的值。

-   事件 **WwanUssdEventTerminated** 用于指示 USSD 会话已终止。

-   事件 **WwanUssdEventOtherLocalClient** 用于指示无法建立新的 USSD 会话，因为已打开一个会话。 这包括对 MB 堆栈不可见的会话，例如 SIM 中的 USSD 会话终止。

-   事件 **WwanUssdEventOperationNotSupported** 用于指示驱动程序或设备不支持以前的请求。

-   事件 **WwanUssdEventNetworkTimeOut** 用于指示会话已由于网络或本地会话超时而关闭。 驱动程序或设备负责实现特定超时后的非活动 USSD 会话。

 

