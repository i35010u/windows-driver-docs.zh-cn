---
title: 测试 WDF 驱动程序（KMDF 或 UMDF）
description: 本主题介绍了有关测试内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 第2版驱动程序的建议。
ms.assetid: 05545488-0114-49f5-bf8a-006a868911e8
keywords:
- 内核模式驱动程序 WDK KMDF、测试
- KMDF WDK，测试驱动程序
- 内核模式驱动程序框架 WDK，测试驱动程序
- 基于框架的驱动程序 WDK KMDF，测试
- 测试驱动程序 WDK，基于框架的驱动程序
- VerifierOn 注册表值 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: caa9affaf177bfddbed94c391494464690bd6faf
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184043"
---
# <a name="testing-a-wdf-driver-kmdf-or-umdf"></a>测试 WDF 驱动程序（KMDF 或 UMDF）


本主题介绍了有关测试内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 第2版驱动程序的建议。

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

有关使用 Microsoft Visual Studio 和 Windows 驱动程序工具包 (WDK) 测试驱动程序的常规信息，请参阅 [测试驱动](../develop/testing-a-driver.md) 程序和 [测试 WDF 驱动程序]()。

 

