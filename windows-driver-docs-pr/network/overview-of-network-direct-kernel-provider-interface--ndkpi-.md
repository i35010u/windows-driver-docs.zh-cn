---
title: 网络直接内核提供程序接口 (NDKPI) 概述
description: '本部分概述了网络直接内核提供程序接口 (NDKPI) '
ms.assetid: D9667238-FD2E-44DE-920F-FA4CF3365D93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7d8ab9563ff69f7786bf5c10b640fcf353eab10
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207869"
---
# <a name="overview-of-network-direct-kernel-provider-interface-ndkpi"></a>网络直接内核提供程序接口 (NDKPI) 概述


网络直接内核提供程序接口 (NDKPI) 是 NDIS 的扩展，它允许 Ihv 提供网络适配器中的内核模式远程直接内存访问 (RDMA) 支持 (也称为 RNIC) 。 为了公开适配器的 RDMA 功能，IHV 必须实现 [NDKPI 引用](/windows-hardware/drivers/ddi/_netvista/)中定义的 NDKPI 接口。

-   [NDKPI 和 RDMA](#ndkpi-and-rdma)
-   [NDK 提供程序](#the-ndk-provider)
-   [NDK 使用者](#the-ndk-consumer)

### <a name="ndkpi-and-rdma"></a>NDKPI 和 RDMA

NIC 供应商将 RDMA 实现为软件、固件和硬件的组合。 硬件和固件部分是提供 NDK/RDMA 功能的网络适配器。 这种类型的适配器也称为启用 RDMA 的 NIC (RNIC) 。 软件部分是支持 NDK 的微型端口驱动程序，该驱动程序实现了 NDKPI 接口。

RDMA 的 Windows 实现称为网络直接 (ND) 。 内核部分称为网络直接内核 (NDK) 。

NDK 提供程序必须通过分配给支持 NDK 的微型端口适配器的 IPv4 和 IPv6 地址支持网络直接连接。

有关 RDMA 的详细信息，请参阅 [rdma 上的后台阅读](background-reading-on-rdma.md)。

### <a name="the-ndk-provider"></a>NDK 提供程序

NDK 提供程序是实现 NDKPI 接口的微型端口驱动程序。

NDK 提供程序由 PnP 管理器加载并初始化。 有关详细信息，请参阅 [初始化支持 ndk 的微型端口驱动程序](initializing-an-ndk-capable-miniport-driver.md) 和 [初始化 Ndk 微型端口适配器](initializing-an-ndk-miniport-adapter.md)。

一旦加载并初始化 NDK 提供程序后，就可以处理来自 NDK 使用者的请求。 这些请求作为调用方函数的调用到达。

处理来自 NDK 使用者的请求时，提供程序可以调用使用者的 NDK 回调函数。 它们记录在 [NDKPI 使用者回调函数](/windows-hardware/drivers/ddi/_netvista/)中。

NDK 提供程序必须实现 [NDKPI 引用](/windows-hardware/drivers/ddi/_netvista/)中记录的 NDKPI 接口的所有元素（ [NDKPI 使用者回调函数](/windows-hardware/drivers/ddi/_netvista/)除外）。

### <a name="the-ndk-consumer"></a>NDK 使用者

NDK 使用者是内核模式的 Windows 组件，例如 SMB 服务器和客户端。

**注意**   本文档不讨论如何实现 NDK 使用者。 NDKPI 使用方设备驱动程序接口 (DDI) 是专有的 Windows 内部接口。

 

NDK 使用者调用提供程序的 *NdkOpenAdapter* ([*打开 \_ NDK \_ 适配器 \_ 处理*](/windows-hardware/drivers/ddi/ndisndk/nc-ndisndk-open_ndk_adapter_handler) 程序) 回调函数创建适配器对象，并 *NdkCloseAdapter* ([*NDK \_ FN \_ close \_ 对象*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_close_object)) 关闭它。 在提供程序创建适配器对象之后，使用者将调用其他提供程序回调函数来创建其他 NDK 对象。

NDK 使用者实现了由 NDK 提供程序调用的 [NDKPI 使用者回调函数](/windows-hardware/drivers/ddi/_netvista/)。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)]()

 

