---
title: 内核模式转储文件
description: 内核模式转储文件
ms.assetid: f04dc580-0e14-41aa-88a2-e04f4406add8
keywords:
- 转储文件中，内核模式
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38e361b55eb404124d5370632dfc416d124d612b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520009"
---
# <a name="kernel-mode-dump-files"></a>内核模式转储文件


## <span id="ddk_kernel_mode_dump_files_dbg"></span><span id="DDK_KERNEL_MODE_DUMP_FILES_DBG"></span>


出现内核模式错误时，Microsoft Windows 的默认行为是显示蓝屏和 bug 检查数据。

但是，有几种可选择的替代行为：

-   可以联系内核调试程序 （如 WinDbg 或 KD）。

-   可以写入内存转储文件。

-   系统可以自动重新启动。

-   可以写入内存转储文件，和的系统可以自动启动之后。

本部分介绍如何创建和分析的内核模式内存转储文件。 有三个不同类型的故障转储文件。 但是，应记住无转储文件可能曾经是为有用且通用实时内核调试程序附加到系统出现故障。

本部分包括：

[类型的内核模式转储文件](varieties-of-kernel-mode-dump-files.md)

[正在创建内核模式转储文件](creating-a-kernel-mode-dump-file.md)

[分析内核模式转储文件](analyzing-a-kernel-mode-dump-file.md)

 

 





