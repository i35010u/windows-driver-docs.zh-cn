---
title: 测试 WDF 驱动程序（KMDF 或 UMDF）
description: 本主题介绍了用于测试的内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 版本 2 驱动程序的建议。
ms.assetid: 05545488-0114-49f5-bf8a-006a868911e8
keywords:
- 内核模式驱动程序 WDK KMDF，测试
- KMDF WDK，测试驱动程序
- 内核模式驱动程序框架 WDK 测试驱动程序
- 基于框架的驱动程序 WDK KMDF，测试
- 测试驱动程序 WDK，基于框架的驱动程序
- VerifierOn 注册表值 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92d84578cfe5b43c04ea1cbc809a53c9abf83eb7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372313"
---
# <a name="testing-a-wdf-driver-kmdf-or-umdf"></a>测试 WDF 驱动程序（KMDF 或 UMDF）


本主题介绍了用于测试的内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 版本 2 驱动程序的建议。

当测试您的驱动程序，您应该：

-   设置**VerifierOn**注册表值以启用框架的驱动程序验证功能。 有关详细信息**VerifierOn** ，并在调试和测试您的驱动程序时可以使用其他注册表值查看[使用 KMDF Verifier](using-kmdf-verifier.md)和[使用 UMDF Verifier](using-umdf-verifier.md). 有关应用程序，可帮助你使用框架的驱动程序验证功能的信息，请参阅[WDF 验证程序控件应用程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)。

-   对于这两种 UMDF 版本 1 和 2，启用[应用程序验证器 (AppVerif.exe)](https://www.microsoft.com/download/details.aspx?id=20028) Wudfhost.exe 上。 例如：
    ```cpp
    appverif -enable handles locks heaps memory exceptions TLS -for WudfHost.exe
    ```

    会自动打开框架的内置验证。
-   使用此文档中所述的驱动程序验证工具。 有关这些重要的工具的详细信息，请参阅：
    -   [WdfTester:WDF 驱动程序测试工具集](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdftester--wdf-driver-testing-toolset)
    -   [用于验证驱动程序的工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-verifying-drivers)
    -   [用于测试驱动程序的工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/tools-for-testing-drivers)

若要全面测试您的驱动程序，必须使用框架的驱动程序验证功能和驱动程序验证工具。

有关测试您使用 Microsoft Visual Studio 和 Windows Driver Kit (WDK) 的驱动程序的常规信息，请参阅[测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/testing-a-driver)并[测试 WDF 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/testing-a-kmdf-driver)。

 

 





