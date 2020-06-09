---
title: 在 Visual Studio 中设置内核模式调试
description: 您可以使用 Microsoft Visual Studio 设置和执行 Windows 的内核模式调试。
ms.assetid: 38E57F45-71D9-4467-BECF-42769563751E
keywords:
- 内核模式调试，Visual Studio
- 设置内核模式调试，Visual Studio
ms.date: 04/10/2017
ms.localizationpriority: medium
ms.openlocfilehash: 205321c0957b89983fc63a53be876d6d44482982
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534760"
---
# <a name="span-iddebuggersetting_up_kernel-mode_debugging_in_visual_studiospansetting-up-kernel-mode-debugging-in-visual-studio"></a><span id="debugger.setting_up_kernel-mode_debugging_in_visual_studio"></span>在 Visual Studio 中设置内核模式调试

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>


您可以使用 Microsoft Visual Studio 设置和执行 Windows 的内核模式调试。 若要将 Visual Studio 用于内核模式调试，必须将 Windows 驱动程序工具包（WDK）与 Visual Studio 集成。 有关如何安装集成环境的信息，请参阅[使用 Visual Studio 进行调试](debugging-using-visual-studio.md)。
 

作为使用 Visual Studio 设置内核模式调试的替代方法，你还可以手动完成设置。 有关详细信息，请参阅[手动设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)。

内核模式调试通常需要两台计算机。 调试器在*主计算机*上运行，要调试的代码在*目标计算机*上运行。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


-   [在 Visual Studio 中设置通过网线进行的内核模式调试](setting-up-a-network-debugging-connection-in-visual-studio.md)
-   [在 Visual Studio 中设置通过 1394 线缆进行的内核模式调试](setting-up-a-1394-cable-connection-in-visual-studio.md)
-   [在 Visual Studio 中设置通过 USB 3.0 线缆进行的内核模式调试](setting-up-a-usb-3-0-cable-connection-in-visual-studio.md)
-   [在 Visual Studio 中设置通过 USB 2.0 线缆进行的内核模式调试](setting-up-a-usb-2-0-cable-connection-in-visual-studio.md)
-   [在 Visual Studio 中设置通过串行线缆进行的内核模式调试](setting-up-a-null-modem-cable-connection-in-visual-studio.md)
-   [在 Visual Studio 中设置使用串行端口通过 USB 进行的内核模式调试](setting-up-kernel-mode-debugging-using-serial-over-usb-in-visual-studio.md)
-   [在 Visual Studio 中设置虚拟机的内核模式调试](setting-up-a-connection-to-a-virtual-machine-in-visual-studio.md)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[设置调试（内核模式和用户模式）](getting-set-up-for-debugging.md)

[手动设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)

 

 






