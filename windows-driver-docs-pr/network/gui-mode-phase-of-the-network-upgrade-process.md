---
title: 网络升级过程的 GUI 模式阶段
description: 网络升级过程的 GUI 模式阶段
ms.assetid: 35c382aa-5905-4a22-b9fa-b876d1373b94
keywords:
- 网络组件升级，WDK 阶段
- 升级网络组件 WDK，阶段
- GUI 模式阶段 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9804d7d615b85fadffe04fe01ccd8e998c2f03f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349890"
---
# <a name="gui-mode-phase-of-the-network-upgrade-process"></a>网络升级过程的 GUI 模式阶段





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

在系统上安装 Windows 2000 或更高版本的操作系统之前，NetSetup 读取 Winnt32 阶段期间写入应答文件的特定于网络的信息。

如果网络迁移 DLL 编写[ **InfToRunBeforeInstall** ](https://msdn.microsoft.com/library/windows/hardware/ff559059)到组件的关键*OEM 部分*应答文件，在 NetSetup 查找的 INF 文件和由指定的部分密钥和进程在本部分中的 INF 指令。 本节通常包含**AddReg**， **DelReg**， **AddService**，或者**DelService**指令。

安装了 Windows 2000 或更高版本操作系统后，NetSetup 安装在系统中，检测到每个网络组件使用指定的组件的 Windows 2000 或更高版本的 INF 文件中的组件的默认参数值。 然后，NetSetup 安装应答文件中列出的网络组件。

如果某个网络组件*OEM 部分*应答文件中包含[OemDllToLoad](examining-the-answerfile.md)键，NetSetup 加载网络迁移 DLL 如果 DLL 不是已加载，然后调用 DLL 的[**PostUpgradeInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff562410)函数。 **PostUpgradeInitialize**函数提供的 DLL 使用初始化其自身的信息的 DLL。 NetSetup 然后调用的 DLL [ **DoPostUpgradeProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff545629)函数一次为每个网络组件由 DLL 升级。 **DoPostUpgradeProcessing**可以显示用户界面，允许用户指定的组件的参数值。 **DoPostUpgradeProcessing**向注册表写入任何用户指定的参数值。

如果网络适配器的微型端口驱动程序需要在升级之前，适配器的实例 ID，它可能会要求在升级后，适配器的实例 ID。 网络迁移，可以调用 DLL [ **HrGetInstanceGuidOfPreNT5NetCardInstance** ](https://msdn.microsoft.com/library/windows/hardware/ff546613)从其**DoPostUpgradeProcessing**函数来获取 Windows 2000 或更高版本网络适配器实例的 GUID。

NetSetup 启动已安装的网络协议、 客户端和服务。

NetSetup 处理中的条目**标识**的应答文件，尝试将系统连接到工作组或域中该部分指定的部分。

如果正在升级系统中包含的任何异步适配器，安装程序将调用异步类安装程序，它将升级每个异步适配器，如下所示：

-   Async 类安装程序应答文件中查找异步适配器的 OEM 部分。

-   从异步适配器的 OEM 部分中，异步类安装程序的适配器读取的升级前的参数值。 这些参数值是由网络迁移 DLL 适配器升级 Winnt32 阶段编写的。

-   Async 类安装程序在 Windows 2000 或更高版本的注册表中写入适配器的升级前的参数值。

 

 





