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
ms.openlocfilehash: e65c49140ce838f65983ecba3334f59189ae3522
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350654"
---
# <a name="testing-a-wdf-driver-kmdf-or-umdf"></a>测试 WDF 驱动程序（KMDF 或 UMDF）


本主题介绍了用于测试的内核模式驱动程序框架 (KMDF) 或用户模式驱动程序框架 (UMDF) 版本 2 驱动程序的建议。

当测试您的驱动程序，您应该：

-   设置**VerifierOn**注册表值以启用框架的驱动程序验证功能。 有关详细信息**VerifierOn** ，并在调试和测试您的驱动程序时可以使用其他注册表值查看[使用 KMDF Verifier](using-kmdf-verifier.md)和[使用 UMDF Verifier](using-umdf-verifier.md). 有关应用程序，可帮助你使用框架的驱动程序验证功能的信息，请参阅[WDF 验证程序控件应用程序](https://msdn.microsoft.com/library/windows/hardware/ff556129)。

-   对于这两种 UMDF 版本 1 和 2，启用[应用程序验证器 (AppVerif.exe)](http://www.microsoft.com/download/details.aspx?id=20028) Wudfhost.exe 上。 例如：
    ```cpp
    appverif -enable handles locks heaps memory exceptions TLS -for WudfHost.exe
    ```

    会自动打开框架的内置验证。
-   使用此文档中所述的驱动程序验证工具。 有关这些重要的工具的详细信息，请参阅：
    -   [WdfTester:WDF 驱动程序测试工具集](https://msdn.microsoft.com/library/windows/hardware/ff556110)
    -   [用于验证驱动程序的工具](https://msdn.microsoft.com/library/windows/hardware/ff552969)
    -   [用于测试驱动程序的工具](https://msdn.microsoft.com/library/windows/hardware/ff552966)

若要全面测试您的驱动程序，必须使用框架的驱动程序验证功能和驱动程序验证工具。

有关测试您使用 Microsoft Visual Studio 和 Windows Driver Kit (WDK) 的驱动程序的常规信息，请参阅[测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/testing-a-driver)并[测试 WDF 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/wdf/testing-a-kmdf-driver)。

 

 





