---
title: INF 文件常规指南
description: INF 文件常规指南
keywords:
- INF 文件 WDK 设备安装，一般指导原则
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50b5c7b7a012e26000841acf39f1d95daf5c58dd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820149"
---
# <a name="general-guidelines-for-inf-files"></a>INF 文件常规指南




INF 文件有许多常见部分，并遵循一组语法规则。 但是，它们也与 Microsoft Windows 支持的各种设备相同。 编写 INF 文件时，请参阅以下信息源：

-   本部分以及 [INF 文件部分和指令](./index.md) 参考材料。

-   设备类别的文档。

    例如，如果设备是打印机，请参阅 [安装和配置打印机驱动程序](../print/installing-and-configuring-printer-drivers.md)。

-   用于 INF 的 WDK 工具文件。

    有关详细信息，请参阅 [用于 INF 文件的工具](../devtest/tools-for-inf-files.md)。 这些工具包含在 WDK 的 \\ tools 子目录中。

-   类似设备的示例 INF 文件和 INF 文件。

    WDK 包含其示例驱动程序的 INF 文件。 查看示例驱动程序，查看设备是否有与设备类似的 INF 文件。

可以通过使用任何文本编辑器来创建或修改 INF 文件，在该编辑器中，可以控制换行符的插入。 如果 INF 中包含非 ASCII 字符，请将该文件保存为 Unicode 文件。

Windows 7 及更早版本的操作系统附带的 INF 文件的文件名必须为 <em>xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx</em>**，其中**"*xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx*" 不能超过八个字符。 与操作系统分开提供的 INF 文件的名称不能超过八个字符。

从 Windows 8 开始，INF 文件名的长度不能超过8个字符，而不管它们是否随操作系统一起提供。

不要以版本控制机制任意修改 INF 文件的时间戳。 INF 文件的版本控制应基于在 [**INF 版本部分**](inf-version-section.md)中指定的日期和版本号。

## <a name="best-practices-for-naming-and-versioning-your-inf-file"></a>对 INF 文件进行命名和版本控制的最佳做法

- INF 名称的命名方式应降低其他供应商与 Inf 发生冲突的可能性。  例如，INF 名称可以包含在其中，可以是前缀或后缀，即公司名称的缩写。
- 如果有两个不同的驱动程序包变体不同（如品牌字符串、设置等），则这两个驱动程序包应该具有唯一的名称。
- 每次更新 inf 或 INF 引用的任何文件时，都应更新 INF 中的日期和版本。
