---
title: Boot.ini 文件概述
description: Boot.ini 文件是一个文本文件，其中包含 BIOS 固件运行 Windows Vista 之前基于 NT 的操作系统的计算机的启动选项。 它位于系统分区的根目录下，通常 c:\Boot.ini。
keywords:
- Boot.ini 文件 WDK，关于 Boot.ini 文件
- 启动加载器部分 WDK 启动选项
- 操作系统部分 WDK 启动选项
- 启动条目 WDK
- 命名 WDK 启动选项
- 友好名称 WDK 启动选项
- 启动项参数 WDK
- 启动参数 WDK
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9435d66013b6f2e84807662d3e5ba00e1cd25d0e
ms.sourcegitcommit: 20569e032b1e0963ad295e9c46b7682832af3d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "100648176"
---
# <a name="overview-of-the-bootini-file"></a>Boot.ini 文件概述

> [!IMPORTANT] 
> 本主题介绍 Windows XP 和 Windows Server 2003 中支持的启动选项。 如果要更改 Windows 的新式版本的启动选项，请参阅 [Windows Vista 和更高版本中的启动选项](./boot-options-in-windows.md)。

Boot.ini 文件是一个文本文件，其中包含 BIOS 固件运行 Windows Vista 之前基于 NT 的操作系统的计算机的启动选项。 它位于系统分区的根目录下，通常为 c： \\Boot.ini。 下面的示例显示了典型 Boot.ini 文件的内容。

```
[boot loader]
timeout=30
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional" /fastdetect
C:\CMDCONS\BOOTSECT.DAT="Microsoft Windows Recovery Console" /cmdcons
```

Boot.ini 有两个主要部分：

-   **\[ 启动加载 \]** 器部分包含适用于系统上的所有启动项的选项设置。 选项包括 **超时**、启动菜单超时值 **，以及默认** 操作系统的位置。

    下面的示例演示了 \[ Boot.ini 的启动加载器 \] 部分。

    ```
    [boot loader]
    timeout=30
    default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
    ```

-   **\[ 操作系统 \]** 部分包括计算机上安装的每个操作系统或可启动程序的一个或多个 *启动项*。

    *启动项* 是一组用于定义操作系统或可启动程序的加载配置的选项。 启动项指定操作系统或启动程序以及其文件的位置。 它还可以包含配置操作系统或程序的参数。

    下面的示例显示了在 \[ \] 具有两个操作系统、MICROSOFT windows XP 和 microsoft windows 2000 的计算机上 Boot.ini 的操作系统部分。 它有两个启动项，分别用于每个操作系统。

    ```
    [operating systems]
    multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional" /fastdetect
    multi(0)disk(0)rdisk(0)partition(2)\WINNT="Microsoft Windows 2000 Professional" /fastdetect
    ```

每个启动条目都包含以下元素：

-   操作系统的位置。 Boot.ini 使用高级 RISC 计算 (ARC) 命名约定显示操作系统所在的磁盘分区和目录的路径。 例如：
    ```
    multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
    ```

-   启动项的友好名称。 易记名称表示启动菜单中的启动条目。 友好名称括在引号内，表示启动菜单中的启动项。 例如：
    ```
    "Microsoft Windows XP Professional"
    ```

-   *启动项参数*（也称为 *启动参数* 或 *加载选项* ）启用、禁用和配置操作系统功能。 启动参数类似于命令行参数，每个参数以正斜杠 (/) （如 [**/debug**](https://support.microsoft.com/help/833721/available-switch-options-for-the-windows-xp-and-the-windows-server-200)）开头。 对于每个启动项，可以有零个或多个启动参数。

    有关与驱动程序测试和调试相关的启动参数的列表，请参阅 [Boot.ini 启动参数参考](./boot-options-in-a-boot-ini-file.md)。

对于同一操作系统，可以有多个启动项，每个启动项具有一组不同的启动参数。 Windows 在你安装操作系统时创建一个标准启动条目，你可以通过编辑 Boot.ini 为操作系统创建其他自定义条目。