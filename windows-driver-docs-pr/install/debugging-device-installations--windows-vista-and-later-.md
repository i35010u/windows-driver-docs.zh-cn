---
title: 调试设备安装
description: 调试设备安装
ms.assetid: bc7105f6-8ba7-49da-8c02-ceda69066daa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 087ddb8305f6c2592ea086d5fda3c32040b07338
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567125"
---
# <a name="debugging-device-installations"></a>调试设备安装


在 Windows Vista 和更高版本的 Windows 上，设备安装的核心阶段始终运行在名为非交互式上下文中*服务器端的安装*。 设备安装的主机进程 (*DrvInst.exe*) 在本地系统帐户的安全上下文下运行。

由于服务器端的安装以非交互方式运行，并且必须完成而无需任何用户输入，它提供给驱动程序的包开发人员想要调试的操作的一些挑战[驱动程序包的](driver-packages.md)安装程序的类和共同安装程序 Dll。 驱动程序包的开发人员，是最通常会在设备的安装过程中调试共同安装程序 DLL 的操作。

本部分包含以下主题，描述用于调试设备安装的核心阶段共同安装程序的技术：

[启用用于调试设备安装的支持](enabling-support-for-debugging-device-installations.md)

[使用用户模式下调试程序调试设备安装](debugging-device-installations-with-a-user-mode-debugger.md)

[使用内核调试器 (KD) 调试设备安装](debugging-device-installations-with-the-kernel-debugger--kd-.md)

有关共同安装程序的详细信息，请参阅[编写共同安装程序](writing-a-co-installer.md)。

 

 





