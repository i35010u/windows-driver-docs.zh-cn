---
title: 在用户模式显示驱动程序中支持旋转
description: 在用户模式显示驱动程序中支持旋转
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，旋转
- 旋转 WDK 显示
- surface 轮换 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e918bc54f4aa4a0cfe7942c2a3640e5a62aa53a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839577"
---
# <a name="supporting-rotation-in-a-user-mode-display-driver"></a>在用户模式显示驱动程序中支持旋转


用户模式显示驱动程序支持旋转的方式不同，具体取决于许多因素。 例如，对于全屏设备，用户模式显示驱动程序的行为方式必须与用于开窗设备的方式不同。 此外，根据桌面窗口管理器 (DWM) 是否正在运行，图形适配器是否支持 Microsoft DirectX 9L，或者 DirectX 9L 应用程序是否能够识别旋转，主要表面的创建方式有所不同。

以下主题介绍用户模式显示驱动程序如何支持在不同情况下旋转：

[窗口模式行为](windowed-mode-behavior.md)

[全屏模式行为](full-screen-mode-behavior.md)

[DirectX 运行时行为](directx-runtime-behavior.md)

 

 





