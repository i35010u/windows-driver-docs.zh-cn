---
title: MB SMS 操作
description: MB SMS 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 334758b0a68a9efe0d738ae1fa2d94b05ba956ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816573"
---
# <a name="mb-sms-operations"></a>MB SMS 操作


本主题介绍使用短消息服务 (SMS) MB 设备的功能配置、读取/接收、发送和删除消息的操作。

SMS 支持是必需的。 小型端口驱动程序必须在 [**WWAN \_ 设备 \_ Cap**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps)结构的 **WwanSmsCaps** 成员中处理 [OID \_ WWAN \_ 设备 \_ cap](./oid-wwan-device-caps.md)查询请求时设置相应的发送和接收短信功能标志。 如果微型端口驱动程序不支持短信，它们应该指定 WWAN \_ sms \_ cap \_ NONE， \_ 并 \_ \_ \_ 为所有 SMS 相关 oid 返回 wwan 状态 "sms 未知错误"。

小型端口驱动程序只应在 [OID \_ WWAN \_ 就绪 \_ 信息](./oid-wwan-ready-info.md) 返回 **WwanReadyStateInitialize** 作为设备就绪状态后处理 SMS 操作。 仅当设备在提供程序网络上注册后，小型端口驱动程序才应处理某些 SMS 操作，如发送 SMS 消息 (但不一定) 的数据服务注册。

MB 服务不区分设备中提供的不同消息存储区。 因此，微型端口驱动程序必须处理所有消息存储，并使用虚拟索引访问单个虚拟消息存储区。 例如，如果设备有三个消息存储，则微型端口驱动程序必须整体处理所有这些消息，并将它们作为单个消息存储显示到服务中。

MB 驱动程序模型支持以下 SMS 操作：

-   SMS 配置

-   阅读短信

-   发送短信

-   删除短信

建议使用微型端口驱动程序来支持 SMS 配置、读取、发送和删除操作，以及向用户通知设备收到的任何新 SMS 消息。

有关 SMS 操作的详细信息，请 [参阅 \_ oid \_ wwan sms \_ 配置](./oid-wwan-sms-configuration.md)、 [oid \_ wwan \_ sms \_ 读取](./oid-wwan-sms-read.md)、 [oid \_ wwan \_ sms \_ 发送](./oid-wwan-sms-send.md)、 [oid \_ wwan \_ sms \_ 删除](./oid-wwan-sms-delete.md)和 [OID \_ wwan \_ sms \_ 状态](./oid-wwan-sms-status.md)。

 

