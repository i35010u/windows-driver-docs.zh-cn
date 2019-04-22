---
title: Windows 显示驱动程序模型 (WDDM) 设计指南
description: Windows 显示器驱动程序模型 (WDDM) 是从 Windows Vista 开始提供，并且需要从 Windows 8 开始。 本部分讨论要求、 规范和 WDDM 驱动程序的行为。
ms.assetid: d9dc0d48-aea4-4614-a23b-e2449800469f
keywords:
- WDDM 设计指南 WDK
- 显示器驱动程序模型 WDK Windows Vista
- Windows Vista 显示器驱动程序模型 WDK
- 显示设备 WDK
- 显示驱动程序 WDK，Windows Vista
- 有关显示驱动程序模型的显示器驱动程序模型 WDK Windows Vista
- Windows Vista 显示器驱动程序模型 WDK，有关显示器驱动程序模型
- 微型端口驱动程序 WDK 显示
- 显示微型端口驱动程序 WDK 请参阅微型端口驱动程序 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03dbe538a843370d5fe33e1392f273918ff5f0c3
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59362910"
---
# <a name="windows-display-driver-model-wddm-design-guide"></a>Windows 显示驱动程序模型 (WDDM) 设计指南


Windows 显示器驱动程序模型 (WDDM) 是从 Windows Vista 开始提供，并且需要从 Windows 8 开始。 本部分讨论要求、 规范和 WDDM 驱动程序的行为。

## <span id="wddm_id"></span><span id="WDDM_ID"></span>


**请注意**  [Windows 2000 显示驱动程序模型 (XDDM)](windows-2000-display-driver-model-design-guide.md)和 VGA 驱动程序不会在 Windows 8 和更高版本上进行编译。 如果显示硬件附加到没有认证支持 WDDM 1.2 或更高版本的驱动程序的 Windows 8 计算机，则系统会默认到正在运行的 Microsoft 基本显示驱动程序。

 

以下部分介绍 Windows 显示器驱动程序模型 (WDDM):

[What's new for Windows 10 显示器驱动程序 (WDDM 2.0)](what-s-new-for-windows-threshold-display-drivers--wddm-2-0-.md)

[What's new for Windows 8.1 显示器驱动程序 (WDDM 1.3)](what-s-new-for-windows-8-1-display-drivers--wddm-1-3-.md)

[什么是 Windows 8 显示器驱动程序 (WDDM 1.2) 的新增功能](what-s-new-for-windows-8-display-drivers.md)

[什么是 Windows 7 的显示器驱动程序 (WDDM 1.1) 的新增功能](what-s-new-for-windows-7-display-drivers--wddm-1-1-.md)

[WDDM 2.0 和 Windows 10](wddm-2-0-and-windows-10.md)

[WDDM 1.2 和 Windows 8](wddm-in-windows-8.md)

[Windows 显示器驱动程序模型 (WDDM) 简介](introduction-to-the-windows-vista-and-later-display-driver-model.md)

[显示微型端口和用户模式显示驱动程序的安装要求](installing-display-miniport-and-user-mode-display-drivers.md)

[优化 Windows 7 及更高版本的显示器驱动程序的安装要求](installing-display-drivers-optimized-for-windows-7-and-later.md)

[初始化显示微型端口和用户模式显示驱动程序](initializing-display-miniport-and-user-mode-display-drivers.md)

[Windows Vista 显示驱动程序线程和同步模型](windows-vista-display-driver-threading-and-synchronization-model.md)

[视频内存管理和 GPU 计划](video-memory-management-and-gpu-scheduling.md)

[用户模式显示驱动程序](user-mode-display-drivers.md)

[显示器驱动程序](monitor-drivers.md)

[多个监视器和视频存在网络](multiple-monitors-and-video-present-networks.md)

[Windows 显示器驱动程序模型 (WDDM) 中的任务](tasks-in-the-windows-vista-display-driver-model.md)

[Windows 显示器驱动程序模型 (WDDM) 的调试提示](debugging-tips-for-the-windows-vista-display-driver-model.md)

[实现技巧和 Windows 显示器驱动程序模型 (WDDM) 的要求](implementation-tips-and-requirements-for-the-windows-vista-display-dri.md)

[显示示例](display-samples.md)

[容器支持非 DX Api](container-non-dx.md)

**请注意**  WDDM 驱动程序不直接使用 Windows 图形设备接口 (GDI) 引擎的服务; 因此， [GDI](gdi.md)部分与编写显示器驱动程序为 WDDM 驱动程序模型无关。

 

 

 





