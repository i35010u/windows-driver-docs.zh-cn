---
title: Unidrv 微型驱动程序
description: Unidrv 微型驱动程序
keywords:
- Unidrv、微型驱动程序
- 微型驱动程序 WDK Unidrv
- 基于文本的打印机说明 WDK Unidrv
- 打印机说明 WDK Unidrv
- GPD 文件 WDK Unidrv，Unidrv 功能
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ce54a8ea9cf33049b6fdfc13cc117edabe11614
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796479"
---
# <a name="unidrv-minidrivers"></a>Unidrv 微型驱动程序





Unidrv 微型驱动程序是包含打印机说明的文本文件。 每个微型驱动程序介绍一种制造商提供的打印机类型。 此基于文本的说明称为一般打印机说明 (GPD) ，每个文件称为 GPD 文件。 每个微型驱动程序都包含一个或多个 GPD 文件。

使用 GPD 文件来描述打印机，Unidrv 支持以下功能：

-   大多数打印机上的通用标准 [打印机功能](printer-features.md) 。

-   只有您的打印机提供的独特的自定义打印机功能。

-   可安装 [打印机选项](printer-options.md)，如果安装了选项，则只能选择这些选项。

-   [选项约束](option-constraints.md)，允许您指定不兼容的选项。

-   [条件语句](conditional-statements.md)，可用于指定某些打印机特性依赖于其他特性。

-   可包括大量[标准变量](standard-variables.md)的当前值的[打印机命令](printer-commands.md)的规范。 还可以对这些变量执行算术运算。

-   自定义帮助文件，此外还有 Unidrv 附带的标准帮助文件，用于描述自定义功能。

有关创建 GPD 文件的信息，请参阅 [GPD Files 简介](introduction-to-gpd-files.md)。

Unidrv 微型驱动程序可包含多个 GPD 文件。 有关详细信息，请参阅 [在微型驱动程序中使用多个 GPD 文件](using-multiple-gpd-files-in-a-minidriver.md)。

安装打印机后，Unidrv 的 GPD 分析器将读取打印机的所有 GPD 文件。 GPD 文件中的信息用于为打印机创建临时二进制文件。 [Unidrv 用户界面](unidrv-user-interface.md)和[Unidrv 呈现](unidrv-renderer.md)器都引用此二进制文件。

通常，微型驱动程序必须提供资源，如字体、位图和可本地化的文本字符串。 这些资源位于资源 DLL 中。 有关详细信息，请参阅 [在微型驱动程序中使用资源 dll](using-resource-dlls-in-a-minidriver.md)。

 

 




