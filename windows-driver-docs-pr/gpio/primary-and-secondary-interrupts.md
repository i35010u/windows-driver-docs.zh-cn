---
title: 主要和次要中断
description: GPIO 中断处理本质上是一个两阶段过程。
ms.assetid: 731B0E36-4480-4B69-931E-1F7B40B18911
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00b906a6232ee9912c58c5c0c819e43f110c5044
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326120"
---
# <a name="primary-and-secondary-interrupts"></a>主要和次要中断


GPIO 中断处理本质上是一个两阶段过程。 调用从常规用途的 I/O (GPIO) 控制器，它将导致 GPIO framework 扩展 (GpioClx) 中断服务例程 (ISR) 运行，中断*主中断*。 此 ISR 将中断的 GPIO 插针映射到的全球系统中断 (GSI)，并将此 GSI 传递给硬件抽象层 (HAL)。 生成 HAL*辅助中断*运行之间存在逻辑连接到的 GPIO 插针此 GSI 通过第二个 ISR。 此过程在关系图中所示[GPIO 驱动程序支持概述](https://msdn.microsoft.com/library/windows/hardware/hh439512#gpio-block-diagram)。

GpioClx 实现 ISR GPIO 控制器配置为中断输入的 GPIO 插针通过收到的服务中断请求。 当外围设备断言的 GPIO 插针，中断并中断已启用，且未掩码 GPIO 控制器中时，GPIO 控制器硬件断言处理器中断。 在此中断响应，ISR GpioClx 查询中的 GPIO 控制器来确定生成中断，，然后确定哪些 GSI 的 GPIO 插针分配给此 pin。 GpioClx ISR 传递到 HAL 和 HAL 此 GSI 调用以逻辑方式连接到 GSI ISR。

通常情况下，此第二个 ISR 属于断言的 GPIO 插针中断外围设备的驱动程序。 有关如何将外围设备驱动程序以逻辑方式连接其 ISR GPIO 中断 pin 信息，请参阅[GPIO-Based 中断资源](https://msdn.microsoft.com/library/windows/hardware/hh698246)。

 

 




