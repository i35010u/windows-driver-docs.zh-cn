---
title: 示例设备和驱动程序配置
description: 示例设备和驱动程序配置
keywords:
- WDM 驱动程序 WDK 内核，配置
- WDM 驱动程序 WDK 内核，分层驱动程序
- 分层驱动程序 WDK 内核
- 驱动程序层 WDK WDM
- 键盘 WDK 内核
- 鼠标 WDK 内核
- 硬件配置 WDK 内核
- 中间驱动程序 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec5a7746433a79f8c55dfb1d0c0f378bde2b3ad5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838865"
---
# <a name="sample-device-and-driver-configuration"></a>示例设备和驱动程序配置





本部分说明硬件和驱动程序配置之间的关系，使用键盘和鼠标设备作为示例。 配置不同于其他设备。 有关任何设备配置的完整信息，请参阅 Windows 驱动程序工具包中的特定于设备的文档 (WDK) 。

### <a href="" id="keyboard-and-mouse-hardware-configurations"></a>

下图显示了键盘和鼠标设备的两个可能的硬件配置：

-   每个直接连接到系统总线上的某个位置

-   均通过键盘和辅助设备控制器进行连接

![阐释键盘和鼠标硬件配置的示意图](images/2kbdmuhw.png)

### <a href="" id="keyboard-and-mouse-driver-layers"></a>

下图显示了上图中所示设备上 i/o 操作的相应分层驱动程序。

![键盘和鼠标驱动程序层](images/2samplyr.png)

请注意，不管硬件配置如何，键盘和鼠标设备的驱动程序都可以使用系统的键盘类和鼠标类驱动程序来处理与硬件无关的操作。 这些 *驱动程序称为类驱动程序* ，因为每个提供系统所需的系统要求，但对特定类设备的硬件独立支持。

相应的 *端口驱动程序* 实现了特定于设备的支持，以在每个物理设备上执行所需的 i/o 操作。 系统的 (i8042) 键盘和辅助设备端口驱动程序，适用于基于 x86 的平台，用于管理鼠标和键盘的设备特定操作。 在每个设备单独连接的硬件配置中，如说明键盘和鼠标硬件配置的图中所示，每个系统类驱动程序都可以分层为单独的特定于设备的端口驱动程序，或者每个设备的单个驱动程序可以作为单独的单一 (最低级别) 驱动程序来实现。

可以将新的中间驱动程序（如 PnP 筛选器驱动程序）添加到演示键盘和鼠标驱动程序层的图中的配置中。 例如，在键盘类驱动程序上面添加的筛选器驱动程序可能会以平台特定的方式筛选键盘输入，然后再将其传递到请求它的子系统。 此类筛选器驱动程序必须识别与键盘类驱动程序相同的 Irp 和 IOCTLs。

 

 




