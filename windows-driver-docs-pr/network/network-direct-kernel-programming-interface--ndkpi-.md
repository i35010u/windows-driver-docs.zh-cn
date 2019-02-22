---
title: 网络直接内核提供程序接口 (NDKPI)
description: 本部分提供了一系列主题有关网络直接内核提供程序接口 (NDKPI) 在 NDIS 6.30 和更高版本
ms.assetid: B7E52112-E049-42E2-9BB3-311EB0D1C577
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92bdd378eca7398e7d00e5c9ae6484dc20f400e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526161"
---
# <a name="network-direct-kernel-provider-interface-ndkpi"></a>网络直接内核提供程序接口 (NDKPI)


在 NDIS 6.30 和更高版本 (Windows Server 2012 及更高版本) 中，网络直接内核提供程序接口 (NDKPI) 启用内核模式 Windows 组件，例如 SMB 服务器和客户端，使用提供的远程直接内存访问 (RDMA) 功能独立硬件供应商 (Ihv)。

-   [网络直接内核提供程序接口 (NDKPI) 的概述](overview-of-network-direct-kernel-provider-interface--ndkpi-.md)
-   [NDKPI 术语](ndkpi-terminology.md)
-   [背景阅读过有关 RDMA](background-reading-on-rdma.md)
-   [初始化支持 NDK 微型端口驱动程序](initializing-an-ndk-capable-miniport-driver.md)
-   [初始化 NDK 微型端口适配器](initializing-an-ndk-miniport-adapter.md)
-   [实现 NDKPI 函数](implementing-ndkpi-callback-functions.md)
-   [NDKPI INF 要求](inf-requirements-for-ndkpi.md)
-   [启用和禁用 NDK 功能](enabling-and-disabling-ndk-functionality.md)
-   [NDKPI 对象生存期要求](ndkpi-object-lifetime-requirements.md)
-   [NDKPI 侦听器、 连接器和终结点](ndkpi-listeners--connectors--and-endpoints.md)
-   [NDKPI 完成处理要求](ndkpi-completion-handling-requirements.md)
-   [NDKPI 工作请求发布要求](ndkpi-work-request-posting-requirements.md)
-   [NetworkDirect 断开连接方案](networkdirect-disconnect-scheme.md)
-   [NDKPI 延迟处理方案](ndkpi-deferred-processing-scheme.md)

 

 





