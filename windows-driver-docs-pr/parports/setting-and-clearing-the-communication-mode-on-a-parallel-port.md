---
title: 设置和清除并行端口上的通信模式
description: 设置和清除并行端口上的通信模式
ms.assetid: a22cdeef-4ae7-49f8-b0b5-a4d68feb4235
keywords:
- 并行端口 WDK，通信模式
- 通信模式 WDK 并行端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97c4604b81457f816a4051ada91ccaa2a322e226
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842321"
---
# <a name="setting-and-clearing-the-communication-mode-on-a-parallel-port"></a>设置和清除并行端口上的通信模式





客户端通过使用以下内部设备控制请求来设置并行端口上的通信模式：

[**IOCTL\_内部\_并行\_集\_芯片\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_set_chip_mode)

[**IOCTL\_内部\_并行\_清晰\_芯片\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_clear_chip_mode)

内核模式驱动程序还可以使用系统提供的、通过 IOCTL 获取的[并行设备回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index) [ **\_内部\_获取\_并行\_PNP\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_parallel_pnp_info)请求。 此请求返回一个[**并行\_PNP\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/ns-parallel-_parallel_pnp_information)结构，其中包括指向系统提供的回调的以下指针：

-   **TrySetChipMode**成员是指向[*PPARALLEL\_集的指针\_芯片\_模式*](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_set_chip_mode)回调，用于设置并行端口的运行模式。

-   **ClearChipMode**成员是指向 PPARALLEL 的指针[ *\_清除\_芯片\_模式*](https://docs.microsoft.com/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_clear_chip_mode)回调，该回调通过将主机芯片集的通信模式重置为 IEEE 1284-兼容性来清除并行端口的操作模式众.

客户端必须先分配一个并行端口，然后才能设置或清除通信模式。

客户端必须先清除通信模式，然后才能设置新的通信模式。 清除通信模式会将主机芯片集返回到 IEEE 1284 兼容模式。

若要确定当前模式，客户端可以使用 IOCTL\_内部\_获取\_并行\_PNP\_INFO 请求，后者返回一个并行\_PNP\_信息结构，该结构包含有关当前通信模式。

 

 




