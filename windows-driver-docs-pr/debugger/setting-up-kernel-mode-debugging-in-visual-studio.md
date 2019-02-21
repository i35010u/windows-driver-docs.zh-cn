---
title: 在 Visual Studio 中设置内核模式调试
description: 可以使用 Microsoft Visual Studio 设置和执行的 Windows 内核模式调试。
ms.assetid: 38E57F45-71D9-4467-BECF-42769563751E
keywords:
- 内核模式调试，Visual Studio
- 内核模式调试，Visual Studio 设置
ms.date: 04/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7880050e1712a5daaa245dc8b0ae77b9cd2dcbc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520680"
---
# <a name="span-iddebuggersettingupkernel-modedebugginginvisualstudiospansetting-up-kernel-mode-debugging-in-visual-studio"></a><span id="debugger.setting_up_kernel-mode_debugging_in_visual_studio"></span>设置 Visual Studio 中的内核模式调试

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>


可以使用 Microsoft Visual Studio 设置和执行的 Windows 内核模式调试。 若要使用内核模式调试的 Visual Studio，必须具有 Windows Driver Kit (WDK) 与 Visual Studio 集成。 有关如何安装集成的环境的信息，请参阅[Windows 驱动程序开发](https://go.microsoft.com/fwlink/p?linkid=301383)。
 

作为使用 Visual Studio 设置内核模式调试的替代方法，你还可以手动完成设置。 有关详细信息，请参阅[设置了内核模式调试手动](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)。

内核模式调试通常需要两台计算机。 在运行调试程序*主机计算机*和代码正在上调试运行*目标计算机*。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>在本部分中


-   [设置通过网络电缆在 Visual Studio 中的内核模式调试](setting-up-a-network-debugging-connection-in-visual-studio.md)
-   [设置通过在 Visual Studio 中的 1394年电缆的内核模式调试](setting-up-a-1394-cable-connection-in-visual-studio.md)
-   [设置内核模式下通过 USB 3.0 电缆在 Visual Studio 中调试](setting-up-a-usb-3-0-cable-connection-in-visual-studio.md)
-   [设置内核模式下通过 USB 2.0 电缆在 Visual Studio 中调试](setting-up-a-usb-2-0-cable-connection-in-visual-studio.md)
-   [设置通过在 Visual Studio 中的串行电缆内核模式调试](setting-up-a-null-modem-cable-connection-in-visual-studio.md)
-   [设置内核模式调试使用通过 Visual Studio 中的 USB 串行](setting-up-kernel-mode-debugging-using-serial-over-usb-in-visual-studio.md)
-   [设置内核模式调试的 Visual Studio 中的虚拟机](setting-up-a-connection-to-a-virtual-machine-in-visual-studio.md)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[设置调试 （内核模式和用户模式下）](getting-set-up-for-debugging.md)

[内核模式调试手动设置](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






