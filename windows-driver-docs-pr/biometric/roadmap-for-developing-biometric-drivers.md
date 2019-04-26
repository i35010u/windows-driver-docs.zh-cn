---
title: 开发生物识别驱动程序的路线图
description: 开发生物识别驱动程序的路线图
ms.assetid: 8ed13c75-86d1-4ac0-9f44-05162521b915
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b021560320ab68f7a1fc7399c150171c712a58a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328375"
---
# <a name="roadmap-for-developing-biometric-drivers"></a>开发生物识别驱动程序的路线图


若要创建的生物识别驱动程序，请执行以下步骤：

-   第 1 步：了解 Windows 体系结构和驱动程序。

    你必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助你做出适当的设计决策，还可以简化开发过程。 有关驱动程序的基本原理的详细信息，请参阅[了解驱动程序和操作系统的基础知识](https://msdn.microsoft.com/library/windows/hardware/ff554731)。

-   步骤 2：了解 Windows 如何支持生物识别驱动程序。

    Windows 7 和更高版本的操作系统版本包括 Windows 生物识别驱动程序接口 (WBDI)。 WBDI 是一个基于 IOCTL 的驱动程序接口，即 Windows 生物识别框架 (WBF) 的一部分。 若要了解有关 WBDI 的详细信息，请参阅[开始使用生物识别驱动程序](getting-started-with-biometric-drivers.md)。

-   步骤 3:查看 WDK 中的生物识别驱动程序示例。

    对于 Windows 7 和更高版本操作系统，驱动程序代码库包含名为的示例[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)。 此示例 WBDI 驱动程序是基于 UMDF 的并使用[USB I/O 目标](https://msdn.microsoft.com/library/windows/hardware/ff561358)。

    有关 WudfBioUsbSample 示例的详细信息，请参阅[示例说明](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics)。

-   步骤 4：选择您的生物识别驱动程序的驱动程序模型。

    Microsoft 建议 WBDI 驱动程序是基于 UMDF 的且使用 USB I/O 目标。 UMDF 有关的信息，请参阅[简介 UMDF](https://msdn.microsoft.com/library/windows/hardware/ff554928)。 有关 USB I/O 目标的信息，请参阅[处理 USB I/O 目标](https://msdn.microsoft.com/library/windows/hardware/ff561358)。

    [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)演示如何实现使用 USB I/O 目标的基于 UMDF WBDI 驱动程序。

    如果使用 UMDF，Microsoft 建议您开发在生物识别驱动程序C++。

-   步骤 5：了解有关 Windows 驱动程序生成、 测试和调试的进程和工具。

    构建一个驱动程序不同于生成在用户模式应用程序。 有关信息请参阅[构建一个驱动程序](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)。 有关如何生成基于 framework 的驱动程序的信息，请参阅[生成和基于 Framework 的驱动程序加载](https://msdn.microsoft.com/library/windows/hardware/ff540730)。

-   步骤 6：做出有关生物识别驱动程序的设计决策。

    有关如何处理 Ioctl 的信息，请参阅[支持生物识别 IOCTL 调用序列](supporting-biometric-ioctl-calling-sequence.md)。 有关如何在 WBDI 驱动程序中使用 USB I/O 目标的信息，请参阅[WBDI 驱动程序中使用 WinUSB](using-winusb-in-a-wbdi-driver.md)。

-   步骤 7：开发、 生成、 测试和调试您的生物识别驱动程序。

    有关如何管理 WBDI 驱动程序中的请求队列的详细信息，请参阅[WBDI 驱动程序中的管理队列](managing-queues-in-a-wbdi-driver.md)。

    有关 Ioctl、 结构和与 WBDI 相关的错误代码的详细信息，请参阅[生物识别设备引用](https://msdn.microsoft.com/library/windows/hardware/ff536410)。

    有关如何测试生物识别驱动程序的信息，请参阅[测试生物识别驱动程序](testing-biometric-drivers.md)。

    有关迭代构建、 测试和调试的信息，请参阅[概述的构建、 调试和测试过程](https://msdn.microsoft.com/windows-drivers/develop/visual_studio_driver_development_environment)。 此过程有助于确保创建的工作的驱动程序。

-   步骤 8：创建您的生物识别驱动程序的驱动程序包。

    有关详细信息，请参阅[提供一个驱动程序包](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_package)。

    有关如何安装生物识别驱动程序的信息，请参阅[安装生物识别驱动程序](installing-a-biometric-driver.md)。

-   步骤 9：签名和分发您的生物识别驱动程序。

    最后一步是签名和分发该驱动程序。 您必须签署您在 32 位和 64 位平台上的引擎适配器。

    如果您的驱动程序符合质量标准，为 Microsoft 硬件认证计划定义，您可以通过 Microsoft Windows Update 计划分发。 有关如何将驱动程序分发的详细信息，请参阅[分发驱动程序](https://msdn.microsoft.com/windows-drivers/develop/distributing_a_driver_package_win8)。

这些是基本步骤。 其他步骤可能有必要在单独的驱动程序的需求。

 

 





