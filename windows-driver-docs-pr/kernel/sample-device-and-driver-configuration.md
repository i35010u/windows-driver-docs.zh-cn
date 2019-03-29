---
title: 示例设备和驱动程序配置
description: 示例设备和驱动程序配置
ms.assetid: 803262b2-0882-46d0-9c4f-63e59eb4beaa
keywords:
- WDM 驱动程序 WDK 内核配置
- WDM 驱动程序 WDK 内核，分层驱动程序
- 分层驱动程序 WDK 内核
- 驱动程序层 WDK WDM
- 键盘 WDK 内核
- 鼠标 WDK 内核
- 硬件配置 WDK 内核
- 中间驱动程序 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3c17c4cd31ffddec2b44aad9c177fb2268b8547
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566619"
---
# <a name="sample-device-and-driver-configuration"></a>示例设备和驱动程序配置





本部分说明的硬件和驱动程序的配置，例如使用键盘和鼠标设备之间的关系。 配置不同的其他设备。 有关任何设备配置的完整信息，请参阅 Windows Driver Kit (WDK) 中的特定于设备的文档。

### <a href="" id="keyboard-and-mouse-hardware-configurations"></a>

下图显示了适用于键盘和鼠标设备的两个可能的硬件配置：

-   每个系统总线上连接直接在某处

-   同时通过键盘和辅助设备控制器连接

![关系图演示的键盘和鼠标的硬件配置](images/2kbdmuhw.png)

### <a href="" id="keyboard-and-mouse-driver-layers"></a>

下图说明了在上图中所示的设备上的 I/O 操作的相应分层驱动程序。

![键盘和鼠标的驱动程序层](images/2samplyr.png)

请注意，驱动程序的键盘和鼠标设备、 任何硬件配置，可以使用系统的键盘类和鼠标类驱动程序来处理独立于硬件的操作。 这些被称为*类的驱动程序*因为每个提供了对设备的特定类的系统要求，但独立于硬件的支持。

相应*端口驱动程序*实现所需的 I/O 操作，每个物理设备上执行的特定于设备的支持。 系统的 (i8042) 键盘和 auxiliary 基于 x86 的平台的设备端口驱动程序管理有关鼠标和键盘的特定于设备的操作。 在硬件配置中，会单独连接每个设备，说明键盘和鼠标硬件配置，图中所示每个系统类驱动程序可以进行分层通过单独的特定于设备的端口驱动程序或为单个驱动程序可作为单独的、 整体化 （最低级别） 驱动程序实现的每个设备。

新中间驱动程序，如即插即用的筛选器驱动程序，无法添加到图中阐释的键盘和鼠标的驱动程序层中的配置。 例如，前面在键盘类驱动程序添加的筛选器驱动程序可能会将其传递通过 I/O 服务到子系统，它在请求之前以特定于平台的方式中筛选键盘输入。 这样的筛选器驱动程序必须将相同的 Irp 和 Ioctl 识别为键盘类驱动程序。

 

 




