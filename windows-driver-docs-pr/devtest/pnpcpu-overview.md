---
title: PNPCPU 概述
description: PNPCPU 概述
keywords:
- PNPCPU WDK，关于 PNPCPU
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67b7a58ea9c471e55aa6bb23505222331799db41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841035"
---
# <a name="pnpcpu-overview"></a>PNPCPU 概述


PNPCPU 是一个命令行工具，用于执行以下功能：

-   安装
    -   若要安装该工具，请运行带有 **-install** 选项 Pnpcpu.exe。
    -   Pnpcpu 安装所有相关驱动程序。
    -   Pnpcpu 用适当的参数更新引导配置数据存储。
-   添加
    -   PNPCPU 尝试热添加系统中的所有逻辑处理器，最大为已安装版本的许可证所支持的最大值。
-   删除
    -   若要删除该工具，请用 **-uninstall** 选项运行 Pnpcpu.exe。 这将导致完全撤销 **安装** 所执行的所有步骤。
    -   此选项会保留磁盘上的二进制文件，以便以后重新安装和使用。

 

 





