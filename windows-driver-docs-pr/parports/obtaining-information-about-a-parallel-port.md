---
title: 获取有关并行端口的信息
description: 获取有关并行端口的信息
ms.assetid: d8ae2296-05b6-419a-93cc-00fcb12d41fe
keywords:
- 并行端口 WDK，获取信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dffbfd5980341de13063fd178f12b6affc456299
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358510"
---
# <a name="obtaining-information-about-a-parallel-port"></a>获取有关并行端口的信息





客户端使用的并行端口之前，它可以获取有关以下信息：

-   并行端口使用的资源

-   硬件功能的并行端口

-   [并行端口回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)，可以使用的内核模式驱动程序

客户端使用以下内置设备控制请求获取上面的信息：

[**IOCTL\_INTERNAL\_GET\_PARALLEL\_PORT\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_get_parallel_port_info)

[**IOCTL\_内部\_获取\_详细\_并行\_端口\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_get_more_parallel_port_info)

[**IOCTL\_INTERNAL\_GET\_PARALLEL\_PNP\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_get_parallel_pnp_info)

客户端通过使用版本并行端口的信息[ **IOCTL\_内部\_发行\_并行\_端口\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/parallel/ni-parallel-ioctl_internal_release_parallel_port_info)请求。

 

 




