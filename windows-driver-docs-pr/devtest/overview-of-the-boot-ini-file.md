---
title: Boot.ini 文件概述
description: Boot.ini 文件是文本文件，其中包含使用运行 Windows Vista 之前基于 NT 的操作系统的 BIOS 固件的计算机的启动选项。 它是系统分区，通常 c:\Boot.ini 根目录。
ms.assetid: bc9bb063-4caa-42fe-bb3d-dc588fbbb8d9
keywords:
- Boot.ini 文件 WDK，有关 Boot.ini 文件
- 启动加载程序部分 WDK 的启动选项
- 操作系统部分 WDK 的启动选项
- 启动项 WDK
- 名称 WDK 启动选项
- 友好名称 WDK 启动选项
- 启动入口参数 WDK
- 引导参数 WDK
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7d0193b302f5a4101775cbfef2050c3b12e48e5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356333"
---
# <a name="overview-of-the-bootini-file"></a>Boot.ini 文件概述

> [!IMPORTANT] 
> 本主题介绍支持 Windows XP 和 Windows Server 2003 中的启动选项。 如果要更改的最新版本的 Windows 启动选项，请参阅[Windows Vista 和更高版本中的启动选项](boot-options-in-windows-vista-and-later.md)。

Boot.ini 文件是文本文件，其中包含使用运行 Windows Vista 之前基于 NT 的操作系统的 BIOS 固件的计算机的启动选项。 它所处的系统分区，通常为 c： 根目录\\Boot.ini。 下面的示例显示了典型的 Boot.ini 文件的内容。

```
[boot loader]
timeout=30
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional" /fastdetect
C:\CMDCONS\BOOTSECT.DAT="Microsoft Windows Recovery Console" /cmdcons
```

Boot.ini 具有两个主要部分：

-   **\[启动加载器\]** 部分包含适用于在系统上的所有启动项的选项设置。 选项包括**超时**，引导菜单超时值，并**默认**的默认操作系统的位置。

    下面的示例演示\[启动加载器\]Boot.ini 的部分。

    ```
    [boot loader]
    timeout=30
    default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
    ```

-   **\[操作系统\]** 部分组成的一个或多个*引导条目*为每个操作系统或可启动的计算机上安装的程序。

    一个*引导条目*是一组定义的操作系统或可启动的程序的负载配置的选项。 启动项指定操作系统或可启动的程序和其文件的位置。 它还可以包含配置操作系统或程序的参数。

    下面的示例演示\[操作系统\]Boot.ini 部分使用两种操作系统，Microsoft Windows XP 和 Microsoft Windows 2000 的计算机上。 它具有两个启动项目，一个用于每个操作系统。

    ```
    [operating systems]
    multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional" /fastdetect
    multi(0)disk(0)rdisk(0)partition(2)\WINNT="Microsoft Windows 2000 Professional" /fastdetect
    ```

每个启动项目包括以下元素：

-   操作系统的位置。 Boot.ini 使用高级 RISC 计算 (ARC) 命名约定来显示磁盘分区和目录路径操作系统所在的位置。 例如：
    ```
    multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
    ```

-   启动条目的友好名称。 友好名称表示引导菜单中的启动项目。 友好名称用引号引起来，表示在启动菜单中的启动项目。 例如：
    ```
    "Microsoft Windows XP Professional"
    ```

-   *启动入口参数*，也称为*引导参数*或*负载选项*启用、 禁用和配置操作系统功能。 引导参数类似于命令行参数，每个以正斜杠 （/） 开头，如[ **/debug**](https://msdn.microsoft.com/library/windows/hardware/ff556253)。 在每个启动项目，可以有零个或多个启动参数。

    与测试和调试驱动程序的启动参数的列表，请参阅[Boot.ini 引导参数引用](https://msdn.microsoft.com/library/windows/hardware/ff542248)。

可以具有相同的操作系统，每个都有一组不同的引导参数的多个启动项。 Windows 创建标准引导条目在安装操作系统，并且可以创建其他，通过编辑 Boot.ini 自定义的操作系统条目。
