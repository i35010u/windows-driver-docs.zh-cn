---
title: 基于硬件的 DVD 解码
description: 基于硬件的 DVD 解码
ms.assetid: 73a32be7-f740-47e8-8177-f204e432c5a6
keywords:
- DVD 解码器微型驱动程序 WDK，基于硬件的 DVD 解码
- 解码器微型驱动程序 WDK DVD，基于硬件的 DVD 解码
- 基于硬件的 DVD 解码 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b69934b2ad6ce257048e084fd40495799832f81
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521915"
---
# <a name="hardware-based-dvd-decoding"></a>基于硬件的 DVD 解码





下图演示了一个基于硬件的 DVD 解码解决方案和如何适应 Windows 驱动程序模型 (WDM) 体系结构。 它显示了与 Microsoft Windows XP 下的现有 DVD 技术的硬件解码器的完整支持。

白色框表示由 Microsoft 提供的软件和阴影的框表示由硬件供应商提供的组件。 椭圆代表由 Ihv 和 Oem 提供的硬件。

使用 Microsoft DVD 的计算机支持这两个 DVD 存储并且如果正确解码硬件或软件存在、 DVD 解码和播放。

![说明硬件 dvd 解码解决方案的关系图](images/hwdvddec.png)

 

 




