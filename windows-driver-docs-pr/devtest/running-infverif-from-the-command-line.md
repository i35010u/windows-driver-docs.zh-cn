---
title: 从命令行运行 InfVerif
description: 本主题列出了从命令行运行 InfVerif.exe 时可用的选项。
ms.assetid: CC2DB624-FFEE-4049-ACE7-4A24B330BADB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2686122d1c695c1b99b691115c45289947ead84
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568764"
---
# <a name="running-infverif-from-the-command-line"></a>从命令行运行 InfVerif


本主题列出了从命令行运行 InfVerif.exe 时可用的选项。
> [!NOTE]
> InfVerif 要求每个组合的路径和文件名称必须少于 260 个字符。

```
USAGE: InfVerif.exe [/v] [/u | /universal] [/k] [/info] [/stampinf] [/l <path>]
                    [/osver TargetOSVersion>] [/product <ias file>] <files>

/v
        Display verbose file logging details.

/k
        Reports errors for Windows Update submission. (mode)

/u
        Reports errors if INF is not Universal. (mode)

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

<files>
        A space-separated list of INF files to analyze.
        Wildcards (*) may be used.

Only one mode option may be passed at a time.
```

有关的示例*TargetOSVersion*格式设置，请参阅备注部分中的[INF 制造商部分](../install/inf-manufacturer-section.md)。

使用详细选项指定 INF 或不是有效的输出中添加一行。  某些参数标记为模式，其中应传递唯一。

*新建适用于 Windows 10，版本 1703年:* 信息选项是特别有用，若要验证 INF 适用性。  它将报告以及有效的体系结构和最低操作系统版本的每个受支持的硬件 ID。  可用于 /info 和 /osver 一起跨 OS 版本和体系结构验证 INF 的适用性。

