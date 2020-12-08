---
title: Windows 显示驱动程序模型 (WDDM) 设计指南
description: Windows 显示驱动程序模型 (WDDM) 从 Windows Vista 开始提供，并从 Windows 8 开始使用。 本部分讨论 WDDM 驱动程序的要求、规范和行为。
keywords:
- WDDM 设计指南 WDK
- 显示驱动程序模型 WDK Windows Vista
- Windows Vista 显示器驱动程序模型 WDK
- 显示设备 WDK
- 显示驱动程序 WDK，Windows Vista
- 显示驱动程序模型 WDK Windows Vista，关于显示器驱动程序模型
- Windows Vista 显示器驱动程序模型 WDK，关于显示器驱动程序模型
- 微型端口驱动程序 WDK 显示
- 显示微型端口驱动程序 WDK，请参阅微型端口驱动程序 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2bf1f6ec2bb731c95bf2b67991525f4900162a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818521"
---
# <a name="windows-display-driver-model-wddm-design-guide"></a>Windows 显示驱动程序模型 (WDDM) 设计指南

从 Windows 8 开始，需要 Windows 显示驱动程序模型 (WDDM) 。 本指南讨论 WDDM 驱动程序的 WDDM 要求、规范和行为。

> [!NOTE]
>
> [Windows 2000 显示器驱动程序型号 (XDDM) ](windows-2000-display-driver-model-design-guide.md)和 VGA 驱动程序将不会在 Windows 8 及更高版本上编译。 如果将显示硬件连接到 Windows 8 计算机，而该计算机上没有一个已认证为支持 WDDM 1.2 或更高版本的驱动程序，则系统默认为运行 Microsoft 基本显示驱动程序。
>
> WDDM 驱动程序不会直接使用 Windows 图形设备接口的服务 (GDI) 引擎;因此， [GDI](gdi.md) 部分与编写 WDDM 驱动程序模型的显示驱动程序并不相关。
