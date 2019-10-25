---
title: 获取有关并行端口的信息
description: 获取有关并行端口的信息
ms.assetid: d8ae2296-05b6-419a-93cc-00fcb12d41fe
keywords:
- 并行端口 WDK，获取信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b762df9f899e1a1d47670d35dbb043cce9f1762f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844498"
---
# <a name="obtaining-information-about-a-parallel-port"></a>获取有关并行端口的信息





在客户端使用并行端口之前，它可以获取有关以下内容的信息：

-   并行端口使用的资源

-   并行端口的硬件功能

-   内核模式驱动程序可以使用的[并行端口回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

客户端使用以下内部设备控制请求来获取上述信息：

[**IOCTL\_内部\_获取\_并行\_端口\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_parallel_port_info)

[**IOCTL\_内部\_获取\_\_并行\_端口\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_more_parallel_port_info)

[**IOCTL\_内部\_获取\_并行\_PNP\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_parallel_pnp_info)

客户端通过使用[**IOCTL\_内部\_版本\_并行\_端口\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_release_parallel_port_info)请求中释放并行端口信息。

 

 




