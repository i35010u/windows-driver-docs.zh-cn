---
title: 获取有关并行端口的信息
description: 获取有关并行端口的信息
keywords:
- 并行端口 WDK，获取信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9dbdeb5414817671e522db789d7b9eaedb84e10f
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97090892"
---
# <a name="obtaining-information-about-a-parallel-port"></a>获取有关并行端口的信息





在客户端使用并行端口之前，它可以获取有关以下内容的信息：

-   并行端口使用的资源

-   并行端口的硬件功能

-   内核模式驱动程序可以使用的[并行端口回调例程](/windows-hardware/drivers/ddi/_parports/)

客户端使用以下内部设备控制请求来获取上述信息：

[**IOCTL \_ 内部 \_ 获取 \_ 并行 \_ 端口 \_ 信息**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_parallel_port_info)

[**IOCTL \_ 内部 \_ 获取 \_ 更多 \_ 并行 \_ 端口 \_ 信息**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_more_parallel_port_info)

[**IOCTL \_ 内部 \_ 获取 \_ 并行 \_ PNP \_ 信息**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_parallel_pnp_info)

客户端通过使用 [**IOCTL \_ 内部 \_ 发布 \_ 并行 \_ 端口 \_**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_release_parallel_port_info) 信息请求来释放并行端口信息。

 

