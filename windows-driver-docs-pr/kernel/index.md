---
title: 内核模式驱动程序体系结构设计指南
description: 内核模式驱动程序体系结构设计指南
ms.assetid: 21c199f3-abc3-4607-a674-eb84b6c3c25a
keywords:
- 内核模式驱动程序 WDK，体系结构
- 内核模式驱动程序 WDK
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 52ace0933e55268e11cb82acccd1e4b06bcc20f1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56465612"
---
# <a name="kernel-mode-driver-architecture-design-guide"></a>内核模式驱动程序体系结构设计指南





本部分提供了一般概念来帮助你了解内核模式编程，并介绍了内核编程的特定技术。 本部分细分为四个部分：

-   [Windows 驱动程序简介](introduction-to-windows-drivers.md)提供了 Windows 组件的一般概述，列出了 Windows 中使用的设备驱动程序的类型，讨论了 Windows 设备驱动程序的目标，并讨论了工具包中包括的泛型示例设备驱动程序。

-   [内核模式管理器和库](kernel-mode-managers-and-libraries.md)列出了 Windows 操作系统的主要内核模式组件。

-   [编写 WDM 驱动程序](writing-wdm-drivers.md)提供了使用 Windows 驱动模型 (WDM) 编写驱动程序时所需的信息。

-   [驱动程序编程技术](driver-programming-techniques.md)介绍了可用于为 Windows 内核模式设备驱动程序进行编程的技术。

    **注意**  有关你的驱动程序可以实现或调用的编程接口的详细信息，请参阅[内核模式驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/ff553217)。

     

 

 




