---
title: Unidrv 微型驱动程序
description: Unidrv 微型驱动程序
ms.assetid: ebf12f61-6194-4033-92a2-2bbccc40a6fd
keywords:
- Unidrv，微型驱动程序
- 微型驱动程序 WDK Unidrv
- 基于文本的打印机说明 WDK Unidrv
- 打印机说明 WDK Unidrv
- GPD 文件 WDK Unidrv，Unidrv 功能
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e2b8963ff529bd5e2e6eff2035db22a9ec36232
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373376"
---
# <a name="unidrv-minidrivers"></a>Unidrv 微型驱动程序





Unidrv 微型驱动程序是包含打印机的说明的文本文件。 每个微型驱动程序介绍一个制造商提供的一种打印机类型。 此基于文本的说明称为通用打印机说明 (GPD)，每个文件调用 GPD 文件。 每个微型驱动程序包含一个或多个 GPD 文件。

使用 GPD 文件来描述打印机，Unidrv 支持以下功能：

-   通用的标准[打印机功能](printer-features.md)，大多数打印机上找到。

-   您的打印机提供的唯一的自定义打印机功能。

-   可安装[打印机选项](printer-options.md)，这仅当，才能选择安装选项。

-   [选项约束](option-constraints.md)，这样便可以指定不兼容的选项。

-   [条件语句](conditional-statements.md)，这样便可以指定某些打印机特征都依赖于其他人。

-   规范[打印机命令](printer-commands.md)可以包括从大量可选择的当前值[标准变量](standard-variables.md)。 此外可以执行这些变量的算术运算。

-   自定义的帮助文件，除了标准的帮助文件提供了 Unidrv，用于描述自定义功能。

有关创建 GPD 文件的信息，请参阅[GPD 文件简介](introduction-to-gpd-files.md)。

Unidrv 微型驱动程序可以包含多个 GPD 文件。 有关详细信息，请参阅[微型驱动程序中使用多个 GPD 文件](using-multiple-gpd-files-in-a-minidriver.md)。

安装打印机时，Unidrv 的 GPD 分析器读取所有打印机 GPD 文件中。 GPD 文件中的信息用于创建临时的二进制文件的打印机。 这两个[Unidrv 用户界面](unidrv-user-interface.md)并[Unidrv 呈现器](unidrv-renderer.md)引用此二进制文件。

通常情况下，微型驱动程序必须提供资源，例如字体、 位图和可本地化的文本字符串。 这些资源置于一个资源 DLL 中。 有关详细信息，请参阅[微型驱动程序中使用资源 Dll](using-resource-dlls-in-a-minidriver.md)。

 

 




