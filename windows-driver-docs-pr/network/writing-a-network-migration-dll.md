---
title: 编写网络迁移 DLL
description: 编写网络迁移 DLL
keywords:
- 网络迁移 DLL WDK
- 网络组件升级 WDK，网络迁移 DLL
- 升级网络组件 WDK，网络迁移 DLL
- 迁移 DLL WDK 网络
- 正在写入网络迁移 DLL
- Dll WDK 网络迁移
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ea0aed2cc4aa8b4ec7064f7ae820ffb51e0059c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836187"
---
# <a name="writing-a-network-migration-dll"></a>编写网络迁移 DLL





**注意**  Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

网络迁移 DLL 可将一个或多个网络组件的参数值从 Microsoft Windows NT 3.51 或 Windows NT 4.0 迁移到 Windows 2000 或更高版本。

网络迁移 DLL 必须：

-   **在 preupgrade 操作系统下加载 (Windows NT 3.51 或 Windows 4.0)**

    DLL 无法调用特定于 Windows 2000 或更高版本的任何函数或使用特定于 Windows 2000 或更高版本的任何功能。 如果 DLL 在 postupgrade (GUI 模式) 阶段中运行，则它还必须在 Windows 2000 和更高版本的操作系统下加载。

-   **导出** [**PreUpgradeInitialize**](/previous-versions/windows/hardware/network/ff562439(v=vs.85))**和**[**DoPreUpgradeProcessing**](/previous-versions/windows/hardware/network/ff545634(v=vs.85))**函数**

    如果 DLL 在 GUI 模式下运行，则它还必须导出 [**PostUpgradeInitialize**](/previous-versions/windows/hardware/network/ff562410(v=vs.85)) 和 [**DoPostUpgradeProcessing**](/previous-versions/windows/hardware/network/ff545629(v=vs.85)) 函数。

-   **在 Winnt32.exe 阶段不进行任何不可逆更改**

    在此阶段，DLL 不得进行任何不可逆更改，如删除文件或修改注册表项，因为用户可以取消网络组件或操作系统的升级。 但是，DLL 可以修改其临时工作目录中的文件，该文件由 NetSetup 在对 **PreUpgradeInitialize** 的调用中指定。

 

