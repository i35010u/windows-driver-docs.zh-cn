---
title: 测试 WDF 驱动程序（KMDF 或 UMDF）
description: 本主题介绍了有关测试 Kernel-Mode Driver Framework (KMDF) 或 User-Mode Driver Framework (UMDF) 版本2驱动程序的建议。
keywords:
- 内核模式驱动程序 WDK KMDF、测试
- KMDF WDK，测试驱动程序
- Kernel-Mode Driver Framework WDK，测试驱动程序
- 基于框架的驱动程序 WDK KMDF，测试
- 测试驱动程序 WDK，基于框架的驱动程序
- VerifierOn 注册表值 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4099c0a7b17bb3757b334fd42cc02f8a4df8acd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815545"
---
# <a name="testing-a-wdf-driver-kmdf-or-umdf"></a>测试 WDF 驱动程序（KMDF 或 UMDF）


本主题介绍了有关测试 Kernel-Mode Driver Framework (KMDF) 或 User-Mode Driver Framework (UMDF) 版本2驱动程序的建议。

测试驱动程序时，应执行以下操作：

-   设置 **VerifierOn** 注册表值以启用框架的驱动程序验证功能。 有关调试和测试驱动程序时可使用的 **VerifierOn** 和其他注册表值的详细信息，请参阅 [使用 KMDF VERIFIER](using-kmdf-verifier.md) 和 [使用 UMDF 验证](using-umdf-verifier.md)程序。 有关可帮助你使用框架的驱动程序验证功能的应用程序的信息，请参阅 [WDF 验证程序控件应用程序](../devtest/wdf-verifier-control-application.md)。

-   对于 UMDF 版本1和2，请在 Wudfhost.exe 上启用 [应用程序验证工具 ( # A0) ]。 下载 [适用于 Windows 的调试工具](../debugger/debugger-download-tools.md)的过程中，你可以下载 AppVerif 工具。  例如：
    ```cpp
    appverif -enable handles locks heaps memory exceptions TLS -for WudfHost.exe
    ```

    这样做会自动启用框架的内置验证。
-   使用本文档中描述的驱动程序验证工具。 有关这些重要工具的详细信息，请参阅：
    -   [WdfTester：WDF 驱动程序测试工具集](../devtest/wdftester--wdf-driver-testing-toolset.md)
    -   [用于验证驱动程序的工具](../devtest/tools-for-verifying-drivers.md)
    -   [用于测试驱动程序的工具](../devtest/tools-for-testing-drivers.md)

若要全面测试您的驱动程序，您必须使用框架的驱动程序验证功能和驱动程序验证工具。 
