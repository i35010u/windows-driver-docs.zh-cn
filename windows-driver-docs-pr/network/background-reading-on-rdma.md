---
title: 对 RDMA 进行后台读取
description: RDMA 是一种网络技术，可提供高吞吐量、低延迟的通信，可最大程度地降低 CPU 使用率。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0f7c75fe9c48826cbc44373666d810f9d7e87c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813007"
---
# <a name="background-reading-on-rdma"></a>对 RDMA 进行后台读取


RDMA 是一种网络技术，可提供高吞吐量、低延迟的通信，可最大程度地降低 CPU 使用率。 NDK 当前支持以下 RDMA 技术：

-   未 (IB) 
-   Internet 广域 RDMA 协议 (iWARP) 
-   基于聚合以太网的 RDMA (RoCE) 

有关 RDMA、iWARP 和 RoCE 的详细信息，请参阅以下资源：

-   [RFC 5040：远程直接内存访问协议规范](https://tools.ietf.org/html/rfc5040)
-   [RFC 5041：直接数据放置在可靠传输上](https://tools.ietf.org/html/rfc5041)
-   [RFC 5042：直接数据放置协议 (DDP) /远程直接内存访问协议 (RDMAP) 安全性](https://tools.ietf.org/html/rfc5042)
-   [RFC 5043：流控制传输协议 (SCTP) 直接数据放置 (DDP) 适配](https://tools.ietf.org/html/rfc5043)
-   [RFC 5044： TCP 规范的标记 PDU 对齐组帧](https://tools.ietf.org/html/rfc5044)
-   [RDMA 联盟](http://www.rdmaconsortium.org/)
-   [Internet 草稿： RDMA 协议谓词规范](https://tools.ietf.org/html/draft-hilland-rddp-verbs-00)
-   [不 RoCE 的贸易协会 (以获取用于应对不平衡和的可下载规范) ](https://www.infinibandta.org/)

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](./overview-of-network-direct-kernel-provider-interface--ndkpi-.md)

 

