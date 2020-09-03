---
title: 在并行设备上设置属性
description: 在并行设备上设置属性
ms.assetid: 10df9a1b-99ec-46b1-b515-10fb20fe2aed
keywords:
- 并行设备 WDK，特性
- 属性 WDK 并行设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6025c9482df60d800aef24bb7ef5484ea4453e3
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384727"
---
# <a name="setting-attributes-on-a-parallel-device"></a>在并行设备上设置属性





客户端使用下列设备控制请求来设置并行设备的指示操作：

-   [**IOCTL \_PAR \_ 集 \_ 信息**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_set_information) 初始化并行设备。

-   [**IOCTL \_串行 \_ 设置 \_ 超时**](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts) 设置并行设备的超时时间。

-   [**IOCTL \_PAR \_ 设置 " \_ 读取 \_ 地址**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_set_read_address) " 为并行设备 (通道) 设置 ECP 或 EPP 读取地址。

-   [**IOCTL \_PAR \_ 设置 \_ 写入 \_ 地址**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_set_write_address) 为并行设备 (通道) 设置 ECP 或 EPP 写入地址。

 

