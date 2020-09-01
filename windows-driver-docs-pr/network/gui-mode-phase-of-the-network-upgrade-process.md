---
title: 网络升级过程的 GUI 模式阶段
description: 网络升级过程的 GUI 模式阶段
ms.assetid: 35c382aa-5905-4a22-b9fa-b876d1373b94
keywords:
- 网络组件升级 WDK，阶段
- 升级网络组件 WDK，阶段
- GUI 模式阶段 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: baa8b7fad2e39602bfbefec4484384ae83db34ea
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207591"
---
# <a name="gui-mode-phase-of-the-network-upgrade-process"></a>网络升级过程的 GUI 模式阶段





**注意**   Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

在系统上安装 Windows 2000 或更高版本的操作系统之前，NetSetup 将读取在 Winnt32.exe 阶段写入 AnswerFile 的特定于网络的信息。

如果网络迁移 DLL 在 AnswerFile 中将 [**InfToRunBeforeInstall**](/previous-versions/windows/hardware/network/ff559059(v=vs.85)) 键写入组件的 *OEM 部分* ，则 NetSetup 将查找密钥指定的 inf 文件和部分，并处理本部分中的 inf 指令。 此部分通常包含 **AddReg**、 **DelReg**、 **AddService**或 **DelService** 指令。

安装 Windows 2000 或更高版本的操作系统后，NetSetup 将使用为组件的 Windows 2000 或更高版本 INF 文件中的组件指定的默认参数值安装系统中检测到的每个网络组件。 然后，NetSetup 安装 AnswerFile 中列出的网络组件。

如果 AnswerFile 中的网络组件的 *OEM 部分* 包含 [OemDllToLoad](examining-the-answerfile.md) 键，则 NetSetup 将加载网络迁移 dll （如果尚未加载 dll），然后调用 dll 的 [**PostUpgradeInitialize**](/previous-versions/windows/hardware/network/ff562410(v=vs.85)) 函数。 **PostUpgradeInitialize**函数为 DLL 提供 dll 用来初始化自身的信息。 然后，NetSetup 将为每个要由 DLL 升级的网络组件调用一次 DLL 的 [**DoPostUpgradeProcessing**](/previous-versions/windows/hardware/network/ff545629(v=vs.85)) 函数。 **DoPostUpgradeProcessing** 可以显示一个用户界面，该用户界面允许用户指定组件的参数值。 **DoPostUpgradeProcessing** 将任何用户指定的参数值写入注册表。

如果网络适配器的微型端口驱动程序需要适配器的实例 ID 才能进行升级，则在升级后可能需要适配器的实例 ID。 网络迁移 DLL 可从其**DoPostUpgradeProcessing**函数调用[**HrGetInstanceGuidOfPreNT5NetCardInstance**](/previous-versions/windows/hardware/network/ff546613(v=vs.85)) ，以获取网络适配器的 Windows 2000 或更高版本的实例 GUID。

NetSetup 启动安装的网络协议、客户端和服务。

NetSetup 处理 AnswerFile 的 **标识** 部分中的条目，并尝试将系统连接到该部分中指定的工作组或域。

如果正在升级的系统包含任何异步适配器，则安装程序将调用 Async class 安装程序，该程序将按如下所示升级每个异步适配器：

-   Async 类安装程序将在 AnswerFile 中查找异步适配器的 OEM 部分。

-   在异步适配器的 OEM 部分，异步类安装程序读取适配器的 preupgrade 参数值。 这些参数值是在升级的 Winnt32.exe 阶段，由适配器的网络迁移 DLL 编写的。

-   Async 类安装程序将适配器的 preupgrade 参数值写入 Windows 2000 或更高版本的注册表。

 

