---
title: 网络升级过程
description: 网络升级过程
ms.assetid: f89cb7c2-8375-4326-94c8-70e2a5e3a1f7
keywords:
- 网络组件升级，WDK 阶段
- 升级网络组件 WDK，阶段
- 应答文件 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b95f7e0208037bed8f67e32057eae9160864fa3d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350817"
---
# <a name="the-network-upgrade-process"></a>网络升级过程





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

网络升级过程分为三个不同的阶段，可以按如下所示简要总结：

-   **Winnt32 阶段**

    Winnt32.exe 调用 NetSetup。 NetSetup 网络的特定于组件的信息写入应答文件，并调用迁移 Dll 的任何供应商提供的网络。 Dll 将特定于组件的信息写入应答文件。 Winnt32.exe 将 Microsoft Windows 2000 或更高版本的文件复制到正在升级系统，并准备在系统上的启动扇区。 然后，系统启动到文本模式。

-   **文本模式阶段**

    安装消息将显示在蓝色、 基于文本的屏幕。 安装程序将执行的基本 Windows 2000 或更高版本的安装。 然后，在系统启动到 GUI 模式。

-   **GUI 模式阶段**

    NetSetup 处理 winnt.sif 文件，也称为应答文件，并安装网络组件。 网络迁移 Dll 可以在其中显示用户界面的用户或系统管理员可以指定网络组件的参数值。 NetSetup 或 DLL 中的网络迁移网络组件的升级前的参数将值写入到 Windows 2000 或更高版本的注册表。

网络升级过程的各个阶段所述的以下主题中的更多详细信息：

[Winnt32 网络升级过程阶段](winnt32-phase-of-the-network-upgrade-process.md)

[网络升级过程的文本模式阶段](text-mode-phase-of-the-network-upgrade-process.md)

[网络升级过程的 GUI 模式阶段](gui-mode-phase-of-the-network-upgrade-process.md)

 

 





