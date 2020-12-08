---
title: TList
description: Tlist.exe (任务列表查看器) ，Tlist.exe 显示在本地计算机上运行的进程以及有关每个进程的有用信息。
keywords: Tlist.exe、任务列表查看器任务列表查看器，请参阅 Tlist.exe
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c796f1136e7f33b6c5e83694c6da7d1b7c9a7ac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801873"
---
# <a name="tlist"></a>TList


## <span id="ddk_tlist_dtools"></span><span id="DDK_TLIST_DTOOLS"></span>


Tlist.exe (任务列表查看器) ，Tlist.exe 是一个命令行工具，它显示在本地计算机上运行的进程以及有关每个进程的有用信息。

Tlist.exe 显示：

-   计算机上运行的所有进程及其进程 Id (Pid) 。

-   显示创建每个进程的进程的树。

-   进程的详细信息，包括其虚拟内存使用情况和启动进程的命令。

-   每个进程中运行的线程，包括它们的线程 Id、入口点、上次报告的错误和线程状态。

-   每个进程中运行的模块，包括模块的版本号、特性和虚拟地址。

您可以使用 Tlist.exe 按名称或 PID 搜索进程，或者查找已加载指定模块的所有进程。

在 Windows XP 和更高版本的 Windows 中，Tlist.exe 已替换为 TaskList ( # A0) ，这些系统的 "帮助和支持" 中对此进行了介绍。 Tlist.exe 包含在 Windows 调试工具中，以支持无权访问 TaskList 的用户。

本节包括：

[**TList 命令**](tlist-commands.md)

[TList 示例](tlist-examples.md)

 

 





