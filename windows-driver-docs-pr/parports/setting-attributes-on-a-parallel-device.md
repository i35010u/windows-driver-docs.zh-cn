---
title: 在并行设备上设置属性
description: 在并行设备上设置属性
ms.assetid: 10df9a1b-99ec-46b1-b515-10fb20fe2aed
keywords:
- 并行设备 WDK，特性
- 属性 WDK 并行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 007e60936f79a7df1f037d780019d165d7cce148
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842318"
---
# <a name="setting-attributes-on-a-parallel-device"></a>在并行设备上设置属性





客户端使用下列设备控制请求来设置并行设备的指示操作：

-   [**IOCTL\_PAR\_集\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_set_information)初始化并行设备。

-   [**IOCTL\_串行\_集\_超时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts)设置并行设备的超时时间。

-   [**IOCTL\_PAR\_集\_读取\_地址**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_set_read_address)为并行设备设置 ECP 或 EPP 读取地址（通道）。

-   [**IOCTL\_PAR\_集\_写入\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_set_write_address)为并行设备设置 ECP 或 EPP 写入地址（通道）。

 

 




