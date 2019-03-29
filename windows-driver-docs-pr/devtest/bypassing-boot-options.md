---
title: 绕过启动选项
description: 绕过启动选项
ms.assetid: 7991fed3-943e-4d43-acba-e2462f7e9d03
keywords:
- 启动选项 WDK，绕过
- F8 键 （跳过启动选项） WDK
- 跳过启动选项
- 内核调试支持 WDK 启动选项
- 调试模式下 WDK 启动选项
- 正在跳过启动选项
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4ff1cc01db09fdf181e842cbdc01f2f456ac4a02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562664"
---
# <a name="bypassing-boot-options"></a>绕过启动选项

正常情况下，调试程序或 Windows Vista 之前的操作系统上的驱动程序也会创建用于调试的启动选项、 重新启动计算机，并选择调试选项从启动菜单。 但是，有时你不能编辑需要进行调试的计算机上的启动选项。

例如，可能会有之前达到登录屏幕时，遇到的 bug 检查的计算机使您无法编辑通过 Windows Boot.ini 文件。 您可以从软盘，启动 Microsoft MS-DOS，但如果您的硬盘启动分区是 NTFS 格式，您将不能编辑来自 MS-DOS 的 Boot.ini 文件。

如果你不能直接编辑启动选项，重新启动计算机，并等待，直到初始 BIOS 过程都已完成。 此时，如果有多个操作系统安装，您将看到启动菜单。 出现此菜单时，按 F8 键。 如果没有多个启动选项，你将看不到引导菜单中，但您仍可以在前两秒的 Windows 加载期间按 F8 键。 您可能会发现最简单的方法只是开始几乎完全 BIOS 过程时重复按 F8 和持续按它直到菜单显示。

按 f8 键将导致显示该故障排除和高级启动选项菜单。 在此菜单上的选项之一是**调试模式下**。 如果选择此选项，你将能够使用内核调试支持启动 Windows。 内核调试程序连接将活动状态的最高枚举 COM 端口 (例如，COM2 如果有两个端口) 通过 19200 波特率。

从 Windows 8 和 Windows Server 2012 开始，启动加载程序不再响应 F8。 相反，当启动加载器检测到的操作系统是中时遇到问题，例如不能达到的登录屏幕，它自动向你提供相关诊断选项，在其中**调试模式下**可能是找到。 但是，如果可以访问登录屏幕，其中一个可以通过发出重新启动命令的同时按住 Shift 键触发诊断选项在下一次启动期间的显示。

 





