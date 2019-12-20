---
title: 对 RDMA 进行后台读取
description: RDMA 是一种网络技术，可提供高吞吐量、低延迟的通信，可最大程度地降低 CPU 使用率。
ms.assetid: 583A806D-B7E8-40F5-9CEB-406FAEE8B6C6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efdec7929e1af40f2918c750a72ab22b137ce373
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210861"
---
# <a name="background-reading-on-rdma"></a>对 RDMA 进行后台读取


RDMA 是一种网络技术，可提供高吞吐量、低延迟的通信，可最大程度地降低 CPU 使用率。 NDK 当前支持以下 RDMA 技术：

-   无限（IB）
-   Internet 广域 RDMA 协议（iWARP）
-   跨聚合以太网的 RDMA （RoCE）

有关 RDMA、iWARP 和 RoCE 的详细信息，请参阅以下资源：

-   [RFC 5040：远程直接内存访问协议规范](https://tools.ietf.org/html/rfc5040)
-   [RFC 5041：直接数据放置在可靠传输上](https://tools.ietf.org/html/rfc5041)
-   [RFC 5042：直接数据放置协议（DDP）/远程直接内存访问协议（RDMAP）安全性](https://tools.ietf.org/html/rfc5042)
-   [RFC 5043：流控制传输协议（SCTP）直接数据放置（DDP）](https://tools.ietf.org/html/rfc5043)
-   [RFC 5044： TCP 规范的标记 PDU 对齐组帧](https://tools.ietf.org/html/rfc5044)
-   [RDMA 联盟](https://www.rdmaconsortium.org/)
-   [Internet 草稿： RDMA 协议谓词规范](https://tools.ietf.org/html/draft-hilland-rddp-verbs-00)
-   [不 RoCE 的贸易协会（适用于适用于无限和的可下载规范）](https://www.infinibandta.org/)

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口（NDKPI）](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






