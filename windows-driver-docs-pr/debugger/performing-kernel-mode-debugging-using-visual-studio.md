---
title: 在 Visual Studio 中进行内核模式调试
description: 若要执行在 Microsoft Visual Studio 中的内核模式调试
ms.assetid: 6E77843F-4907-4193-B987-92BD0719AE10
keywords:
- 内核模式调试 visual studio
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5f77678509680cb79b1a780bef3580dc210133ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387071"
---
# <a name="span-iddebuggerperformingkernel-modedebuggingusingvisualstudiospankernel-mode-debugging-in-visual-studio"></a><span id="debugger.performing_kernel-mode_debugging_using_visual_studio"></span>内核模式下在 Visual Studio 中调试

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>


若要执行在 Microsoft Visual Studio 中的内核模式调试：

1.  主机计算机上，在 Visual Studio 中，从**工具**菜单中，选择**附加到进程**。
2.  在中**附加到进程**对话框中，将**传输**到**Windows 内核模式调试程序**，并设置**限定符**的名称以前配置的目标计算机。 有关配置目标计算机的信息，请参阅[设置内核模式调试在 Visual Studio](setting-up-kernel-mode-debugging-in-visual-studio.md)或[设置了内核模式调试手动](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)。
3.  单击**附加。**

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[使用 Visual Studio 调试](debugging-using-visual-studio.md)

 

 






