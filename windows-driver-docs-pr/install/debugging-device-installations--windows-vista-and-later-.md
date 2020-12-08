---
title: 调试设备安装
description: 调试设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 388cde9b9a4d4e5102a5aa7f713bc9e2c01127a0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827779"
---
# <a name="debugging-device-installations"></a>调试设备安装


在 Windows Vista 和更高版本的 Windows 上，设备安装的核心阶段始终在非交互式上下文中运行，这种情况称为 *服务器端安装*。 设备安装的主机进程 (*DrvInst.exe*) 在 LocalSystem 帐户的安全上下文中运行。

由于服务器端安装以非交互方式运行，并且必须在无需任何用户输入的情况下完成，因此它为要调试 [驱动程序包的](driver-packages.md) 类安装程序和共同安装程序 dll 的操作的驱动程序包开发人员提供了一些挑战。 对于驱动程序包的开发人员而言，在安装设备的过程中，通常最需要调试共同安装程序 DLL 的操作。

本部分包含以下主题，其中描述了用于在设备安装的核心阶段调试共同安装程序的技术：

[启用对设备安装调试的支持](enabling-support-for-debugging-device-installations.md)

[使用用户模式调试程序调试设备安装](debugging-device-installations-with-a-user-mode-debugger.md)

[使用内核调试程序 (KD) 调试设备安装](debugging-device-installations-with-the-kernel-debugger--kd-.md)

有关共同安装程序的详细信息，请参阅 [编写共同安装程序](writing-a-co-installer.md)。

 

 





