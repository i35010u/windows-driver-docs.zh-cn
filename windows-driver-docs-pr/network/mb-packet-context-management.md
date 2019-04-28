---
title: MB 数据包上下文管理
description: MB 数据包上下文管理
ms.assetid: 52d72def-8aee-4e04-ad42-1a4537cda899
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 333b153d408c4cea8016b2006346ec06b6e53778
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343265"
---
# <a name="mb-packet-context-management"></a>MB 数据包上下文管理


本主题介绍了数据包上下文，它们是一组特定的网络配置参数设置的管理*虚拟线路*或*流*基于物理 MB 连接在第 2 层。 在基于 GSM 的设备，这对应于概念的数据包数据协议 (PDP)。 在基于 CDMA 的设备，这对应于网络配置文件。

在大多数情况下，数据包上下文的详细的设置预配了 Ihv 和/或网络提供商的 MB 设备连接，或者通过网络无线 (OTA) 预配或使用短信。 在任一情况下，最终用户通常不需要提供的大多数设置 （例如，服务质量 (QoS)、 安全代码、 移动 IP，，等等）。 但是，最终用户可能需要提供网络访问字符串、 用户名和密码。 它是构成内容的数据包上下文从 MB 服务的角度来看这些用户可配置设置。

MB 驱动程序模型不提供显式 OID 来设置或关闭 WWAN 的第 2 层连接。 相反，激活设置基础的第 2 层连接授权和停用的最后一个数据包上下文中的第一个数据包上下文结果将有效地拆解基础的第 2 层连接。

MB 驱动程序模型基于这两个有关活动的包上下文的数目限制在任何给定时间按以下方式：

1.  每个数据包上下文可以激活仅一次。

2.  可以在任何给定时间激活仅单个数据包上下文。

它是必需的 MB 驱动程序模型是否符合任何微型端口驱动程序设置**MaxActivatedContexts**的成员[ **WWAN\_设备\_CAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff571204)为 1，在响应时的结构[OID\_WWAN\_设备\_CAPS](https://msdn.microsoft.com/library/windows/hardware/ff569824)查询请求。 即使微型端口驱动程序设置此值是大于 1，则可确保 MB 服务，最多只有一个数据包激活上下文在任何给定时间。

每个数据包上下文可以激活不超过一次，因为静态数据包上下文标识符可以用于标识正在激活后的虚拟线路。 使用此静态标识符是仍然有效，前提是第一个约束仍然成立。

有关数据包上下文管理的详细信息，请参阅[OID\_WWAN\_已预配\_上下文](https://msdn.microsoft.com/library/windows/hardware/ff569831)并[OID\_WWAN\_CONNECT](https://msdn.microsoft.com/library/windows/hardware/ff569823).

 

 





