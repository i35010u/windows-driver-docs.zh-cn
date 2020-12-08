---
title: 内核模式转储文件
description: 内核模式转储文件
keywords:
- 转储文件，内核模式
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 976ae59fb76f59389844a1e743c5017b14fb78c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801895"
---
# <a name="kernel-mode-dump-files"></a>内核模式转储文件


## <span id="ddk_kernel_mode_dump_files_dbg"></span><span id="DDK_KERNEL_MODE_DUMP_FILES_DBG"></span>


发生内核模式错误时，Microsoft Windows 的默认行为是显示带有 bug 检查数据的蓝屏。

但是，可以选择以下几种替代行为：

-   可以联系 (的内核调试器，如 WinDbg 或 KD) 。

-   可以写入内存转储文件。

-   系统可以自动重启。

-   可以写入内存转储文件，并且系统可以在以后自动重新启动。

本部分介绍如何创建和分析内核模式内存转储文件。 有三种不同种类的故障转储文件。 但是，应记住，任何转储文件都不能像连接到发生故障的系统的实时内核调试器一样有用。

本节包括：

[内核模式转储文件的种类](varieties-of-kernel-mode-dump-files.md)

[创建内核模式转储文件](creating-a-kernel-mode-dump-file.md)

[分析内核模式转储文件](analyzing-a-kernel-mode-dump-file.md)

 

 





