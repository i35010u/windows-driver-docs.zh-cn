---
title: 图形系统概述
description: 图形系统概述
ms.assetid: d120a9df-d8ed-4862-b421-2e7545be1ed0
keywords:
- GDI WDK Windows 2000 显示，相关图形系统信息
- 显示图形驱动程序 WDK Windows 2000，有关图形系统
- 有关图形系统绘制 WDK GDI，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55893ead753a61efcef52ac3eba4b8dd428a4596
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519309"
---
# <a name="graphics-system-overview"></a>图形系统概述


## <span id="ddk_graphics_system_overview_gg"></span><span id="DDK_GRAPHICS_SYSTEM_OVERVIEW_GG"></span>


Microsoft Windows NTâˆ 基于的操作系统提供稳定可靠的图形体系结构中的第三方图形硬件公司可以轻松地集成其视频显示和打印设备。 以下各节提供编写有效的图形驱动程序的设计准则：

-   [**Graphics DDI**](using-the-graphics-ddi.md)

    本部分介绍 Windows 图形设备接口 (GDI) 和图形设备驱动程序接口 (DDI)。 介绍了设计和实现详细信息所共有的显示和打印驱动程序。

-   [**Windows 显示驱动程序模型 (WDDM) 设计指南**](windows-vista-display-driver-model-design-guide.md)

    [**Windows 2000 显示器驱动程序模型 (XDDM) 设计指南**](windows-2000-display-driver-model-design-guide.md)

    下列各节介绍 Windows NTâˆ 中的视频显示环境基于操作系统和显示，微型端口，用于提供设计和实现详细信息，以及监视驱动程序编写人员。 请注意，不能在 Windows 8 和更高版本的计算机上安装驱动程序遵循与 Windows 2000 显示器驱动程序模型。

-   [**打印设备设计指南**](https://msdn.microsoft.com/library/windows/hardware/ff561035)

    本部分介绍驱动程序和打印后台处理程序组成 Windows NTâˆ 中的打印环境的基于操作系统。 Windows 驱动程序工具包 (WDK) 的此部分中的各部分指定如何提供自定义驱动程序和后台处理程序组件，以便可以支持新打印机硬件和网络配置。

 

 





