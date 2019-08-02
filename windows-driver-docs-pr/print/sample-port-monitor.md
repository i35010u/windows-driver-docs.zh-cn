---
title: 示例端口监视器
description: 示例端口监视器
ms.assetid: dac754bf-f39d-439c-974b-889436211ef3
keywords:
- 端口监视 WDK 打印, 示例
ms.date: 08/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 36f4d2e1634d9eac0e43465ef1f72a0b7a9a0693
ms.sourcegitcommit: b444e3a948c4aae2ca1196167844d694c83c8869
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68720044"
---
# <a name="sample-port-monitor"></a>示例端口监视器

> [!NOTE]
> LOCALMON 打印监视器示例已存档, 在 GitHub 上的[Windows 驱动程序工具包 (WDK) 10 示例](https://github.com/microsoft/Windows-driver-samples)存储库中不可用。

[Windows 驱动程序工具包 (wdk) 8.0 示例](https://go.microsoft.com/fwlink/p/?LinkId=616509)存档和[Windows 驱动程序工具包 (wdk) 8.1 示例](https://go.microsoft.com/fwlink/p/?LinkId=618052)存档中包含 LOCALMON (LOCALMON) 的源代码 (支持本地 LPT 和 COM 端口的端口监视器)。

LOCALMON 导出的函数合并为本地打印提供程序 Localspl。 端口监视器分为两个 Dll: 端口监视器服务器 DLL 和端口监视器用户界面 DLL。

这些 dll 的\\源代码位于打印监视器示例\\C++\\localmon 和\\打印监视器示例C++\\\\localui 子目录的WDK 示例上列出的存档。
