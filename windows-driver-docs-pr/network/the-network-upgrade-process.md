---
title: 网络升级过程
description: 网络升级过程
keywords:
- 网络组件升级 WDK，阶段
- 升级网络组件 WDK，阶段
- AnswerFile WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1db6508c8e71fb3c4c2c0dfbbbb891261a2a0075
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840601"
---
# <a name="the-network-upgrade-process"></a>网络升级过程





**注意**  Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

网络升级过程分为三个不同的阶段，可以按如下所示简单总结：

-   **Winnt32.exe 阶段**

    Winnt32.exe 调用 NetSetup。 NetSetup 将网络组件特定的信息写入 AnswerFile，并调用任何供应商提供的网络迁移 Dll。 Dll 将组件特定的信息写入 AnswerFile。 Winnt32.exe 将 Microsoft Windows 2000 或更高版本的文件复制到正在升级的系统，并准备系统上的启动扇区。 然后，系统将启动到文本模式。

-   **文本模式阶段**

    安装消息显示在基于文本的蓝色屏幕上。 安装程序执行基本的 Windows 2000 或更高版本安装。 然后，系统将启动到 GUI 模式。

-   **GUI 模式阶段**

    NetSetup 处理 winnt .sif 文件（也称为 AnswerFile）并安装网络组件。 网络迁移 Dll 可以显示一个用户界面，用户或系统管理员可以在其中指定网络组件的参数值。 NetSetup 或网络迁移 DLL 会将网络组件的 preupgrade 参数值写入 Windows 2000 或更高版本的注册表。

以下主题更详细地介绍了网络升级过程的各个阶段：

[网络升级过程的 Winnt32 阶段](winnt32-phase-of-the-network-upgrade-process.md)

[网络升级过程的文本模式阶段](text-mode-phase-of-the-network-upgrade-process.md)

[网络升级过程的 GUI 模式阶段](gui-mode-phase-of-the-network-upgrade-process.md)

 

 





