---
title: Windows 显示驱动程序模型 (WDDM) 设计指南
description: Windows 显示驱动程序模型（WDDM）从 Windows Vista 开始提供，并从 Windows 8 开始是必需的。 本部分讨论 WDDM 驱动程序的要求、规范和行为。
ms.assetid: d9dc0d48-aea4-4614-a23b-e2449800469f
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
ms.openlocfilehash: 72c22419a18eca7ab8af5e8c70131e7102df1aff
ms.sourcegitcommit: 0d89fc46058efb2ebc6ed9bd8f638c3f8cc1a678
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2020
ms.locfileid: "86459233"
---
# <a name="windows-display-driver-model-wddm-design-guide"></a>Windows 显示驱动程序模型 (WDDM) 设计指南

从 Windows 8 开始，Windows 显示驱动程序模型（WDDM）是必需的。 本指南讨论 WDDM 驱动程序的 WDDM 要求、规范和行为。

> [!NOTE]
>
> Windows [2000 显示器驱动程序模型（XDDM）](windows-2000-display-driver-model-design-guide.md)和 VGA 驱动程序将不会在 windows 8 及更高版本上编译。 如果将显示硬件连接到 Windows 8 计算机，而该计算机上没有一个已认证为支持 WDDM 1.2 或更高版本的驱动程序，则系统默认为运行 Microsoft 基本显示驱动程序。
>
> WDDM 驱动程序不会直接使用 Windows 图形设备接口（GDI）引擎的服务;因此， [GDI](gdi.md)部分与编写 WDDM 驱动程序模型的显示驱动程序并不相关。
