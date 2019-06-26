---
title: 网络直接内核提供程序接口 (NDKPI) 概述
description: 本部分提供的网络直接内核提供程序接口 (NDKPI) 概述
ms.assetid: D9667238-FD2E-44DE-920F-FA4CF3365D93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 028b126224c08f2fcdf75143de695750ad2e459d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384374"
---
# <a name="overview-of-network-direct-kernel-provider-interface-ndkpi"></a>网络直接内核提供程序接口 (NDKPI) 概述


网络直接内核提供程序接口 (NDKPI) 是允许 Ihv 提供网络适配器 （也称为 RNIC） 中的内核模式远程直接内存访问 (RDMA) 支持的 NDIS 的扩展。 若要显示适配器的 RDMA 功能，IHV 必须实现 NDKPI 接口中定义[NDKPI 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

-   [NDKPI 和 RDMA](#ndkpi-and-rdma)
-   [NDK 提供程序](#the-ndk-provider)
-   [NDK 使用者](#the-ndk-consumer)

### <a name="ndkpi-and-rdma"></a>NDKPI 和 RDMA

NIC 供应商的软件、 固件和硬件组合实现 RDMA。 硬件和固件的部分是提供 NDK/RDMA 功能的网络适配器。 此类型的适配器也称为启用了 RDMA 的 NIC (RNIC)。 软件部分是能够 NDK 微型端口驱动程序，可以实现 NDKPI 接口。

RDMA 的 Windows 实现称为网络直接 (ND)。 内核部分被称为网络直接内核 (NDK)。

NDK 提供程序必须支持通过分配给 NDK 支持微型端口适配器的 IPv4 和 IPv6 地址的网络直接连接。

有关 RDMA 的详细信息，请参阅[背景阅读过有关 RDMA](background-reading-on-rdma.md)。

### <a name="the-ndk-provider"></a>NDK 提供程序

NDK 提供程序是实现 NDKPI 接口的微型端口驱动程序。

NDK 提供程序进行加载和初始化 PnP 管理器。 有关详细信息，请参阅[初始化 NDK 支持的微型端口驱动程序](initializing-an-ndk-capable-miniport-driver.md)并[初始化 NDK 微型端口适配器](initializing-an-ndk-miniport-adapter.md)。

一旦 NDK 提供程序进行加载和初始化，已准备好处理来自 NDK 使用者的请求。 作为对提供程序函数的调用到达这些请求。

在处理来自 NDK 使用者的请求时，该提供程序可以调用使用者的 NDK 回调函数。 这些文档位于[NDKPI 使用者的回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

NDK 提供程序必须实现中所述的 NDKPI 接口中的所有元素[NDKPI 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)，除[NDKPI 使用者的回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

### <a name="the-ndk-consumer"></a>NDK 使用者

NDK 使用者是内核模式 Windows 组件，例如 SMB 服务器和客户端。

**请注意**  本文不讨论如何实现 NDK 使用者。 NDKPI 使用者设备驱动程序接口 (DDI) 是一个专用的 Windows 内部接口。

 

NDK 使用者调用提供程序的*NdkOpenAdapter* ([*打开\_NDK\_适配器\_处理程序*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndisndk/nc-ndisndk-open_ndk_adapter_handler)) 到回调函数创建一个适配器的对象和*NdkCloseAdapter* ([*NDK\_FN\_关闭\_对象*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_close_object)) 以将其关闭。 一旦该提供程序创建的适配器对象，使用者调用其他提供程序回调函数来创建其他 NDK 对象。

使用者实现 NDK [NDKPI 使用者的回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)，由 NDK 提供程序调用。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






