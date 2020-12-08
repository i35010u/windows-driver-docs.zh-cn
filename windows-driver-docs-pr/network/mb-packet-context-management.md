---
title: MB 数据包上下文管理
description: MB 数据包上下文管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa19617f4d51f06180a65c9e233023204ec3b9a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816591"
---
# <a name="mb-packet-context-management"></a>MB 数据包上下文管理


本主题介绍数据包上下文的管理，这是一组特定的网络配置参数，用于在第2层的物理 MB 连接之上设置 *虚拟线路* 或 *流* 。 在基于 GSM 的设备中，这对应于数据包数据协议 (PDP) 的概念。 在基于 CDMA 的设备中，这对应于一个网络配置文件。

在大多数情况下，数据包上下文的详细设置可以由 Ihv 和/或 MB 设备的网络提供程序预配，也可以通过无线 (OTA) 或使用短信进行预配。 无论是哪种情况，最终用户通常都不需要提供大多数设置 (例如，服务质量 (QoS) 、安全代码、移动 IP 等) 。 但是，最终用户可能需要提供网络访问字符串、用户名和密码。 这是这些用户可配置的设置，这些设置构成了从 MB 服务角度来的数据包上下文内容。

MB 驱动程序模型未提供显式 OID，因此无法设置或拆卸 WWAN 的第2层连接。 相反，激活第一个数据包上下文会导致设置基础第2层连接，停用最后一个数据包上下文会有效地断开底层的第2层连接。

在任意给定时间，在任何给定时间，MB 驱动程序模型都基于以下两个约束建立：

1.  每个数据包上下文只能激活一次。

2.  在任意给定时间，只能激活单个数据包上下文。

当响应 [OID \_ wwan \_ 设备 \_ cap](./oid-wwan-device-caps.md)查询请求时，任何符合 MB 驱动程序模型的微型端口驱动程序都必须将 [**WWAN \_ 设备 \_ cap**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps)结构的 **MaxActivatedContexts** 成员设置为一个。 即使微型端口驱动程序将此值设置为大于1，MB 服务也可确保在任何给定时间，最多只能激活一个数据包上下文。

由于每个数据包上下文只能激活一次，因此可以使用静态数据包上下文标识符来识别激活后的虚拟线路。 只要第一个约束仍保留，则使用此静态标识符仍然有效。

有关包上下文管理的详细信息，请参阅 [oid \_ wwan \_ 预配 \_ 上下文](./oid-wwan-provisioned-contexts.md) 和 [oid \_ wwan \_ CONNECT](./oid-wwan-connect.md)。

 

