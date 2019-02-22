---
title: V4 打印机驱动程序配置体系结构
description: V4 打印机驱动程序模型支持大大简化了的配置层。
ms.assetid: E797CB4A-C28E-4442-89E6-97B589900BD6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73f581861a41a02141560b8aed3221d2941d5500
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543547"
---
# <a name="v4-printer-driver-configuration-architecture"></a>V4 打印机驱动程序配置体系结构


V4 打印机驱动程序模型支持大大简化了的配置层。

与使用 v3 打印机驱动程序，其中用户界面紧密耦合与驱动程序配置，这种情况不同 v4 打印机驱动程序关注于提供 PrintTicket 和 PrintCapabilities，约束的功能。 常见的配置模块 PrintConfig.dll，封装了以前在 UnidrvUI 和 PS5UI 核心驱动程序中提供的功能。

V4 打印机驱动程序模型不会利用配置插件，因此应 GPD 或 PPD 文件中表示的大多数设备配置。 此外，v4 打印机驱动程序可能会提供支持高级约束处理，以及 PrintTicket 和 PrintCapabilities 支持的 JavaScript 文件。

**配置文件格式**

泛型打印机说明 (GPD) 和 PostScript 打印机说明 (PPD) 文件格式保持不变与 v4 打印机驱动程序。 现有 GPD 和 PPD 文件相兼容，但是，所有 v4 打印机驱动程序必须另外都指定以下指令在其 GPD 或 PPD 文件中。 这些指令阻止 XPSDrv，如每张多本机不支持的功能的表达式。

| 文件类型 | 所需的指令 | 所需的值 |
|-----------|--------------------|----------------|
| GPD       | \*包括          | msxpsinc.gpd   |
| PPD       | \*MSIsXPSDriver    | True           |

 

**请注意**  PPD 基于驱动程序不能指定\*Include: msxpsinc.ppd 指令，因为这已知会引起与某些应用程序兼容性问题。

 

**映射到 PrintSchema**

映射功能和选项划分 PrintSchema 的命名空间是在许多情况下必需的。 映射将导致由驱动程序以进行更符合标准的打印用户界面和应用程序生成的 PrintCapabilities 文档。

某些功能和选项被视为标准，并将自动映射到 PrintSchema 的命名空间。 这些功能和选项是特定的不应使用被重新映射\*PrintSchemaKeywordMap。 如果未列出，必须使用驱动程序\*PrintSchemaKeywordMap 指令上基于 GPD 的驱动程序，或\*MSPrintSchemaKeywordMap 指令上基于 PPD 的驱动程序。

 

 




