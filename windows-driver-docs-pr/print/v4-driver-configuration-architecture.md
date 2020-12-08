---
title: V4 打印机驱动程序配置体系结构
description: V4 打印机驱动程序模型支持的配置层非常简单。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc8d98cfc1c3837dee489b891273577f1409bff5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785953"
---
# <a name="v4-printer-driver-configuration-architecture"></a>V4 打印机驱动程序配置体系结构


V4 打印机驱动程序模型支持的配置层非常简单。

与 v3 打印机驱动程序不同的是，用户界面与驱动程序配置的结合非常结合，v4 打印机驱动程序专注于提供 PrintTicket、PrintCapabilities 和约束功能。 PrintConfig.dll 的常见配置模块封装了以前在 UnidrvUI 和 PS5UI 核心驱动程序中可用的功能。

V4 打印机驱动程序模型不使用配置插件，因此，大多数设备配置应以 GPD 或 PPD 文件表示。 此外，v4 打印机驱动程序还可以提供支持高级约束处理以及 PrintTicket 和 PrintCapabilities 支持的 JavaScript 文件。

**配置文件格式**

一般打印机说明 (GPD) 和 PostScript 打印机说明 (PPD) 文件格式在 v4 打印机驱动程序中保持不变。 现有的 GPD 和 PPD 文件是兼容的，但是，所有 v4 打印机驱动程序还必须在其 GPD 或 PPD 文件中指定以下指令。 这些指令可防止 XPSDrv 不支持的功能的表达式，如 "N"。

| 文件类型 | 必需的指令 | 所需的值 |
|-----------|--------------------|----------------|
| GPD       | \*包括          | msxpsinc.gpd   |
| 信息库       | \*MSIsXPSDriver    | 正确           |

 

**注意**  基于 PPD 的驱动程序不得指定 \* Include： msxpsinc 指令，因为已知这会导致某些应用程序的兼容性问题。

 

**映射到 PrintSchema**

在许多情况下，将功能和选项映射到 PrintSchema 的命名空间是必需的。 映射会导致驱动程序生成的 PrintCapabilities 文档与标准打印 UI 和应用程序更兼容。

某些功能和选项被视为标准，并自动映射到 PrintSchema 的命名空间中。 这些功能和选项是特定的，不应使用 PrintSchemaKeywordMap 重新映射 \* 。 如果未另行列出，驱动程序必须 \* 在基于 GPD 的驱动程序上使用 PrintSchemaKeywordMap 指令，或 \* 在基于 PPD 的驱动程序上使用 MSPrintSchemaKeywordMap 指令。

 

 




