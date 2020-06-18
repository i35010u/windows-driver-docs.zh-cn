---
title: 示例端口监视器
description: 示例端口监视器
ms.assetid: dac754bf-f39d-439c-974b-889436211ef3
keywords:
- 端口监视 WDK 打印，示例
ms.date: 06/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 84457f81c4c88898c854e8121e4873cdb0e82773
ms.sourcegitcommit: f4f861a9f833ef1389ff5c08e2b9de0d3df81bef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84974151"
---
# <a name="sample-port-monitor"></a>示例端口监视器

LOCALMON 导出的函数合并到本地打印提供程序 Localspl.dll 中。 端口监视器分为两个 Dll：端口监视器服务器 DLL 和端口监视器用户界面 DLL。

> [!NOTE]
> LOCALMON （Localmon.dll）以前版本的 Windows 的打印监视器示例已存档，如下所述。 LOCALMON （Localmon.dll）打印监视器示例代码在 GitHub 上的 Windows 驱动程序工具包（WDK）10示例中不可用。

对于以前版本的 Windows，LOCALMON 的示例源代码（Localmon.dll）在以下位置提供：

- 对于 Windows 7， [Windows 驱动程序工具包 7.1.0](https://www.microsoft.com/en-us/download/details.aspx?id=11800)安装下载中包含了 Localmon.dll 的示例源代码。 该示例位于** \\ src \\ print \\ monitor \\ localmon**子目录中（例如，C:\WinDDK\7600.16385.1\src\print\monitors\localmon）。

- 对于 Windows 8，Localmon.dll 的示例源代码可在 GitHub 上的 Windows 驱动程序工具包（WDK）8.0 示例存档存储库中的[localmon](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.0%20Samples/%5BC%2B%2B%5D-Windows%20Driver%20Kit%20(WDK)%208.0%20Samples/C%2B%2B/WDK%208.0%20Samples/Print%20Monitors%20Samples/Solution/localmon)目录中找到。

- Windows 8.1，Windows 驱动程序工具包（WDK）8.1 示例 GitHub 上的[localmon](https://github.com/microsoftarchive/msdn-code-gallery-microsoft/tree/master/Official%20Windows%20Driver%20Kit%20Sample/Windows%20Driver%20Kit%20(WDK)%208.1%20Samples/%5BC%2B%2B%5D-windows-driver-kit-81-cpp/WDK%208.1%20C%2B%2B%20Samples/Print%20Monitors%20Samples/C%2B%2B/localmon)目录中提供了 Localmon.dll 的示例源代码。
