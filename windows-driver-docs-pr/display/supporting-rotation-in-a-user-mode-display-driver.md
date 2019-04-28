---
title: 在用户模式显示驱动程序中支持旋转
description: 在用户模式显示驱动程序中支持旋转
ms.assetid: fb80e875-26d4-4928-9268-2c6b36bb5d20
keywords:
- 用户模式显示驱动程序 WDK Windows Vista 中，旋转
- 旋转 WDK 显示
- 图面上旋转 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da3a606fc565e59588441884cb1e21ccaf8d50a4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350176"
---
# <a name="supporting-rotation-in-a-user-mode-display-driver"></a>在用户模式显示驱动程序中支持旋转


用户模式显示驱动程序支持旋转以不同的方式，具体取决于许多因素。 例如，用户模式显示驱动程序必须的行为不同的全屏幕设备比有窗口的设备。 此外，以不同的方式根据是否正在运行的桌面窗口管理器 (DWM) 创建主图面，图形适配器支持 Microsoft DirectX 9 L 或使用 DirectX 9 L 应用程序会旋转知道。

下面的主题介绍用户模式显示驱动程序如何支持不同的情况下的旋转：

[Windowed-Mode Behavior](windowed-mode-behavior.md)

[全屏幕模式行为](full-screen-mode-behavior.md)

[DirectX 运行时行为](directx-runtime-behavior.md)

 

 





