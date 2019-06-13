---
ms.assetid: 2274e848-2a0b-445c-82cd-7bcd9e23078a
title: 调试驱动程序
description: 通常，调试内核模式驱动程序需要两台计算机。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89c126f5a8429d6cff5d6dc50a314fa3def99d48
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63382347"
---
# <a name="debugging-a-driver"></a>调试驱动程序

通常，调试内核模式驱动程序需要两台计算机。 调试程序在主计算机  上运行，所调试的代码在目标计算机  上运行。 目标计算机也称为“测试计算机”  。 你可以在主计算机上或在单独的目标计算机上调试用户模式驱动程序。 你必须先为调试配置目标计算机，然后才能够调试目标计算机上运行的驱动程序。

有关配置目标计算机和设置调试电缆的信息，请参阅[在 Visual Studio 中设置内核模式调试](https://msdn.microsoft.com/windows/hardware/hh439376)和[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](https://msdn.microsoft.com/Library/Windows/Hardware/Dn745909)。

有关使用 Microsoft Visual Studio 调试驱动程序的信息，请参阅[使用 Visual Studio 调试](https://msdn.microsoft.com/Library/Windows/Hardware/Hh406281)。

有关使用 Visual Studio 调试内核模式驱动程序的示例，请参阅[基于模板编写 KMDF 驱动程序](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439654)。

有关 Windows 调试工具的简介，请参阅 [Windows 调试](https://msdn.microsoft.com/Library/Windows/Hardware/Ff551063)。

## <a name="span-idvideodemonstrationspanspan-idvideodemonstrationspanspan-idvideodemonstrationspanvideo-demonstration"></a><span id="Video_Demonstration"></span><span id="video_demonstration"></span><span id="VIDEO_DEMONSTRATION"></span>视频演示


此视频演示如何在 Visual Studio 中直接使用 WinDbg 调试引擎，而不是单独运行 WinDbg。

>[!VIDEO https://www.microsoft.com/videoplayer/embed/57464a96-8900-4194-b806-813eb1dd6ac6]





