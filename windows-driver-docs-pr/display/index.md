---
title: 显示设备设计指南
description: 显示设备设计指南
ms.assetid: 0cbd75a3-49c3-4805-8f97-ab3551d0c6ee
keywords:
- 显示驱动程序 WDK
- 微型端口驱动程序 WDK 显示
ms.date: 10/10/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 38867a715c9cc4d7e1a4af8e86d80545bbd9cdff
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252385"
---
# <a name="display-devices-design-guide"></a>显示设备设计指南

欢迎使用 Windows 显示驱动程序设计指南。 本部分包括：

- [Windows 显示驱动程序模型 (WDDM) 设计指南](windows-vista-display-driver-model-design-guide.md)

  WDDM 是从 Windows Vista 开始提供的显示/图形驱动程序体系结构。 遵循 WDDM 的驱动程序仅在 Windows Vista 和更高版本上运行。

- [Windows 2000 显示驱动程序模型 (XDDM) 设计指南](windows-2000-display-driver-model-design-guide.md)

  WDDM 是为 Windows 2000 到 Windows Vista 和 Windows 7 提供的显示/图形驱动程序体系结构。 XDDM 和 VGA 驱动程序在 Windows 8 及更高版本上无法编译。 如果将显示硬件连接到 Windows 8 计算机，而该计算机上没有一个已认证为支持 WDDM 1.2 或更高版本的驱动程序，则系统默认为运行 Microsoft 基本显示驱动程序。

- [显示示例](display-samples.md)
