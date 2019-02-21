---
title: 其他标准驱动程序例程
description: 其他标准驱动程序例程
ms.assetid: 3dada9cc-7239-47de-8940-bc4cef8be4ca
keywords:
- 驱动程序 WDK 内核对象
- 标准驱动程序例程 WDK 内核，驱动程序对象
- 驱动程序例程 WDK 内核，驱动程序对象
- 例程 WDK 内核，驱动程序对象
- 对象 WDK 驱动程序对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55176b65ea228ee474a8057cef082b8e10fdea1a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520885"
---
# <a name="other-standard-driver-routines"></a>其他标准驱动程序例程





作为[驱动程序对象图](introduction-to-driver-objects.md#driver-object-illustration)所示，内核模式驱动程序有其他标准例程以及它们设置入口点在其各自的驱动程序对象中。 大多数标准驱动程序例程以及他们使用的配置相关对象的一些由 I/O 管理器定义。 ISR *SynchCritSection*例程和那些名称中包含的单词"自定义"定义由 NT 内核驱动程序对象图中所示。

大多数驱动程序使用[设备扩展](device-extensions.md)的每个设备对象它们创建保持有关它们的 I/O 操作的特定于设备的状态并将其存储到它们必须以具有其他标准分配任何系统资源的指针例程。 例如， **DDCustomTimerDpc**驱动程序对象图中所示的例程需要驱动程序提供的内核定义计时器和 DPC 对象存储。

在左侧显示的最低级别驱动程序的标准驱动程序例程的一[驱动程序对象图](introduction-to-driver-objects.md#driver-object-illustration)一定不同于更高级别的驱动程序集。 此图中所示的例程的一些是依赖于设备的或依赖于配置的要求。 有些则是可选： 你可以选择对驱动程序的设计实现具体的特性或驱动程序的设备的配置取决于此类的例程和驱动程序上的位置的链中分层驱动程序。

 

 




