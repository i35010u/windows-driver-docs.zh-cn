---
title: 从命令行运行 InfVerif
description: 本主题列出了从命令行运行 InfVerif.exe 时可用的选项。
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2319a8b1c1c0ea8222e74c0aa124012f23554482
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805711"
---
# <a name="running-infverif-from-the-command-line"></a>从命令行运行 InfVerif

本主题列出了从命令行运行 InfVerif.exe 时可用的选项。

> [!NOTE]
> InfVerif 要求每个组合的路径和文件名必须少于260个字符。

```syntax
USAGE: InfVerif.exe [/v] [/u | /universal] [/w] [/k] [/info] [/stampinf] [/l <path>]
                    [/osver TargetOSVersion>] [/product <ias file>] <files>

/v
        Display verbose file logging details.

/k
        Reports errors for Hardware Dev Center submission. (mode; checks error codes 1100-1299)

/u
        Reports errors if INF is not Universal. (mode)

/w
        Reports Windows Driver compatibility. See below. (mode)

/info
        Displays INF summary information.

/stampinf
        Treat $ARCH$ as a valid architecture, to validate
        pre-stampinf files.

/l <path>
        An inline-annotated HTML version of each INF
        file will be placed in the <path>.

/osver <TargetOsVersion>
        Process the INF for a specific target OS.
        Formatting is the same as a Models section, i.e. NTAMD64.6.0
        Matches the TargetOSVersion you would use in a Models section name (see link below)

/product <ias file>
        Validates all include/needs directives against
        the product definition in the ias file.

/recurse
        Process INF files that match the specified file pattern in the current directory and all subdirectories.

<files>
        A space-separated list of INF files to analyze.
        Wildcards (*) may be used.

Only one mode option may be passed at a time.
```

有关错误代码的信息，请参阅 [INF 验证错误和警告](./inf-validation-errors-and-warnings.md)

Verbose 选项向输出添加一行，用于指定 INF 是否有效。  某些参数被标记为模式，其中只应传递其中一项。

有关 *TargetOSVersion* 格式设置的示例，请参阅 [INF 制造商部分](../install/inf-manufacturer-section.md)的 "备注" 部分。

*适用于 Windows 10 的新版本1703：*  Info 选项对于验证 INF 适用性特别有用。  它会报告每个受支持的硬件 ID 以及有效的体系结构和最低操作系统版本。  可以同时使用/info 和/osver 来验证 INF 在操作系统版本和体系结构方面的适用性。

*适用于 Windows 10 的新版本1809：* 如果要开发 *Windows 驱动程序*，请使用 `infverif /w` (理想使用 `/v`) 来确定与 [DCH 设计原则](../develop/dch-principles-best-practices.md)的 **声明性 (D)** 原则的兼容性。  该 `/w` 标志还会检查 INF 是否符合 [驱动程序包隔离](../develop/driver-isolation.md) 要求 [和 Windows 驱动程序入门](../develop/getting-started-with-windows-drivers.md)。

若要验证多个 INF 文件，请提供多个文件名或使用通配符：

```command
infverif.exe /w test1.inf test2.inf
infverif.exe /w test*.inf
```
