---
title: 在并行设备上设置属性
description: 在并行设备上设置属性
ms.assetid: 10df9a1b-99ec-46b1-b515-10fb20fe2aed
keywords:
- 并行设备 WDK，属性
- 属性 WDK 并行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6c7669bc15f4dda5d7c9f02e18995b5f390b192
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353592"
---
# <a name="setting-attributes-on-a-parallel-device"></a>在并行设备上设置属性





客户端使用以下设备控制请求设置并行的设备的指示的操作：

-   [**IOCTL\_PAR\_设置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_set_information)初始化并行设备。

-   [**IOCTL\_串行\_设置\_超时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ni-ntddser-ioctl_serial_set_timeouts)设置并行的设备的超时。

-   [**IOCTL\_PAR\_设置\_读取\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_set_read_address)设置 ECP 或 EPP 读取并行设备地址 （通道）。

-   [**IOCTL\_PAR\_设置\_编写\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddpar/ni-ntddpar-ioctl_par_set_write_address)设置 ECP 或 EPP 写地址 （通道） 并行设备。

 

 




