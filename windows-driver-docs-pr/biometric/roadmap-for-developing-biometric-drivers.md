---
title: 开发生物识别驱动程序的路线图
description: 开发生物识别驱动程序的路线图
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 644b88db4399a7733fc3fa52634a7c4723f9f303
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798619"
---
# <a name="roadmap-for-developing-biometric-drivers"></a>开发生物识别驱动程序的路线图


若要创建生物识别驱动程序，请执行以下步骤：

-   步骤1：了解 Windows 体系结构和驱动程序。

    您必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助您做出适当的设计决策，并使您能够简化开发过程。 有关驱动程序基础的详细信息，请参阅 [了解驱动程序和操作系统基础知识](../gettingstarted/concepts-and-knowledge-for-all-driver-developers.md)。

-   步骤2：了解 Windows 支持生物识别驱动程序的方式。

    Windows 7 及更高版本的操作系统版本包括 Windows 生物识别驱动程序接口 (WBDI) 。 WBDI 是一种基于 IOCTL 的驱动程序接口，它是 Windows Biometric Framework (WBF) 的一部分。 若要了解有关 WBDI 的详细信息，请参阅 [具有生物识别驱动程序的入门](getting-started-with-biometric-drivers.md)。

-   步骤3：查看 WDK 中的生物识别驱动程序示例。

    对于 Windows 7 及更高版本的操作系统，驱动程序代码库包含一个名为 [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)的示例。 此示例 WBDI 驱动程序基于 UMDF，并使用 [USB I/o 目标](../wdf/usb-i-o-targets-in-umdf.md)。

    有关 WudfBioUsbSample 示例的详细信息，请参阅 [示例说明](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics)。

-   步骤4：为生物识别驱动程序选择驱动程序模型。

    Microsoft 建议 WBDI 驱动程序基于 UMDF，并使用 USB i/o 目标。 有关 UMDF 的信息，请参阅 [Umdf 简介](/previous-versions/ff554928(v=vs.85))。 有关 USB i/o 目标的信息，请参阅 [处理 usb I/o 目标](../wdf/usb-i-o-targets-in-umdf.md)。

    [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver) 演示如何实现使用 USB i/o 目标的基于 UMDF 的 WBDI 驱动程序。

    如果你使用 UMDF，Microsoft 建议你使用 c + + 开发生物识别驱动程序。

-   步骤5：了解 Windows 驱动程序的生成、测试和调试过程和工具。

    构建驱动程序不同于构建用户模式应用程序。 有关信息，请参阅 [构建驱动程序](../develop/building-a-driver.md)。 有关如何生成基于框架的驱动程序的信息，请参阅 [生成和加载基于框架的驱动程序](../wdf/building-and-loading-a-kmdf-driver.md)。

-   步骤6：作出有关生物识别驱动程序的设计决策。

    有关如何处理 IOCTLs 的详细信息，请参阅 [支持生物识别 IOCTL 调用序列](supporting-biometric-ioctl-calling-sequence.md)。 有关如何在 WBDI 驱动程序中使用 USB i/o 目标的信息，请参阅在 [WBDI 驱动程序中使用 WinUSB](using-winusb-in-a-wbdi-driver.md)。

-   步骤7：开发、构建、测试和调试生物识别驱动程序。

    有关如何在 WBDI 驱动程序中管理请求队列的详细信息，请参阅 [在 WBDI 驱动程序中管理队列](managing-queues-in-a-wbdi-driver.md)。

    有关与 WBDI 相关的 IOCTLs、结构和错误代码的详细信息，请参阅 [生物识别设备参考](/windows-hardware/drivers/ddi/index)。

    有关如何测试生物识别驱动程序的信息，请参阅 [测试生物识别驱动程序](testing-biometric-drivers.md)。

    有关迭代生成、测试和调试的信息，请参阅 [生成、调试和测试过程的概述](/windows-hardware/drivers)。 此过程有助于确保创建一个可工作的驱动程序。

-   步骤8：创建生物识别驱动程序的驱动程序包。

    有关详细信息，请参阅 [提供驱动程序包](/windows-hardware/drivers)。

    有关如何安装生物识别驱动程序的信息，请参阅 [安装生物识别驱动程序](installing-a-biometric-driver.md)。

-   步骤9：签署和分发生物识别驱动程序。

    最后一步是对驱动程序进行签名和分发。 你必须在32位和64位平台上签署你的引擎适配器。

    如果你的驱动程序满足为 Microsoft 硬件认证计划定义的质量标准，你可以通过 Microsoft Windows 更新计划分发它。 有关如何分发驱动程序的详细信息，请参阅 [分发驱动程序](/windows-hardware/drivers)。

这些是基本步骤。 根据单个驱动程序的需要，可能需要执行其他步骤。

 

