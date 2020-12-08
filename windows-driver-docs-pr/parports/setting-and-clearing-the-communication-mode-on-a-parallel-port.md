---
title: 设置和清除并行端口上的通信模式
description: 设置和清除并行端口上的通信模式
keywords:
- 并行端口 WDK，通信模式
- 通信模式 WDK 并行端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f680429124d12562d80ee862a39f6eab438718d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812577"
---
# <a name="setting-and-clearing-the-communication-mode-on-a-parallel-port"></a>设置和清除并行端口上的通信模式





客户端通过使用以下内部设备控制请求来设置并行端口上的通信模式：

[**IOCTL \_ 内部 \_ 并行 \_ 设置 \_ 芯片 \_ 模式**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_set_chip_mode)

[**IOCTL \_ 内部 \_ 并行 \_ 清除 \_ 芯片 \_ 模式**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parallel_clear_chip_mode)

内核模式驱动程序还可以使用系统提供的、通过 [**IOCTL \_ 内部 \_ GET \_ 并行 \_ PNP \_ 信息**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_get_parallel_pnp_info)请求获取的 [并行设备回调例程](/windows-hardware/drivers/ddi/index)。 此请求返回 [**并行 \_ PNP \_ 信息**](/windows-hardware/drivers/ddi/parallel/ns-parallel-_parallel_pnp_information) 结构，其中包括指向系统提供的回调的以下指针：

-   **TrySetChipMode** 成员是指向 [*PPARALLEL \_ 集 \_ 芯片 \_ 模式*](/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_set_chip_mode)回调的指针，它可设置并行端口的运行模式。

-   **ClearChipMode** 成员是指向 [*PPARALLEL \_ 清除 \_ 芯片 \_ 模式*](/windows-hardware/drivers/ddi/parallel/nc-parallel-pparallel_clear_chip_mode)回拨的指针，它通过将主机芯片集的通信模式重置为 IEEE 1284 兼容模式，清除并行端口的运行模式。

客户端必须先分配一个并行端口，然后才能设置或清除通信模式。

客户端必须先清除通信模式，然后才能设置新的通信模式。 清除通信模式会将主机芯片集返回到 IEEE 1284 兼容模式。

若要确定当前模式，客户端可以使用 IOCTL \_ 内部 \_ GET \_ PARALLEL \_ PNP \_ INFO 请求，这会返回 \_ \_ 包含当前通信模式相关信息的并行 pnp 信息结构。

 

