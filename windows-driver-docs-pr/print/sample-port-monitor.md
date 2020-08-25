---
title: 示例端口监视器
description: 示例端口监视器
ms.assetid: dac754bf-f39d-439c-974b-889436211ef3
keywords:
- 端口监视 WDK 打印，示例
ms.date: 08/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: fbc5837bf6c18592dd823e6bbac6bd6a334d3485
ms.sourcegitcommit: d9a9925f790271f4ca2c8377d551d96e8d1e62c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88850295"
---
# <a name="sample-port-monitor"></a>示例端口监视器

LOCALMON 导出的函数合并到本地打印提供程序 Localspl.dll 中。 端口监视器分为两个 Dll：端口监视器服务器 DLL 和端口监视器用户界面 DLL。

> [!NOTE]
> LOCALMON ( # A0) 先前版本 Windows 的打印监视器示例已存档，如下所述。 LOCALMON ( # A0) 打印监视器示例代码在 Windows 驱动程序工具包中不可用，但在 GitHub 上 (WDK) 10 个示例。

对于以前版本的 Windows，LOCALMON 的示例源代码 ( # A0) 在以下位置提供：

- 对于 Windows 7， [Windows 驱动程序工具包 7.1.0](https://www.microsoft.com/download/details.aspx?id=11800) 安装下载中包含了 Localmon.dll 的示例源代码。 该示例位于** \\ src \\ 打印 \\ 监视器 \\ localmon**子目录 (例如，C:\WinDDK\7600.16385.1\src\print\monitors\localmon) 。

- 对于 Windows 8，Localmon.dll 的示例源代码可在 GitHub 上的 Windows 驱动程序工具包 (WDK) 8.0 示例存档存储库中的 [localmon](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.0%20Samples/%5BC%2B%2B%5D-Windows%20Driver%20Kit%20(WDK)%208.0%20Samples/C%2B%2B/WDK%208.0%20Samples/Print%20Monitors%20Samples/Solution/localmon) 目录中找到。

- 对于 Windows 8.1，Localmon.dll 的示例源代码可在 GitHub 上的 Windows 驱动程序工具包 8.1)  (的 Windows 驱动程序工具包中的 [localmon](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.1%20Samples/%5BC%2B%2B%5D-windows-driver-kit-81-cpp/WDK%208.1%20C%2B%2B%20Samples/Print%20Monitors%20Samples/C%2B%2B/localmon) 目录中找到。
