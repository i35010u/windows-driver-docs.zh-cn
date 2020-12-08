---
title: 在 Visual Studio 中进行内核模式调试
description: 在 Microsoft Visual Studio 中执行内核模式调试
keywords:
- visual studio 的内核模式调试
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: ff868b7d79aa199a56fe6b337ba612cf9ac46af9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838365"
---
# <a name="span-iddebuggerperforming_kernel-mode_debugging_using_visual_studiospankernel-mode-debugging-in-visual-studio"></a><span id="debugger.performing_kernel-mode_debugging_using_visual_studio"></span>在 Visual Studio 中进行内核模式调试

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>


若要在 Microsoft Visual Studio 执行内核模式调试：

1.  在主计算机上，在 Visual Studio 的 " **工具** " 菜单中，选择 " **附加到进程**"。
2.  在 " **附加到进程** " 对话框中，将 " **传输** 到 **Windows 内核模式调试程序**" **设置为先前** 配置的目标计算机的名称。 有关配置目标计算机的信息，请参阅 [在 Visual Studio 中设置 Kernel-Mode 调试](setting-up-kernel-mode-debugging-in-visual-studio.md) 或 [手动设置 Kernel-Mode 调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)。
3.  单击 " **附加"。**

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用 Visual Studio 进行调试](debugging-using-visual-studio.md)

 

 






