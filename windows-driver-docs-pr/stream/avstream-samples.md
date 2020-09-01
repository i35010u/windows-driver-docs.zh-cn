---
title: AVStream 示例
description: AVStream 示例
ms.assetid: 18ddd9f1-d8bb-49a7-91bf-a8aeaa9565ad
keywords:
- AVStream WDK，示例
- 示例微型驱动程序 WDK AVStream
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: f85be5db225d9160b2852cdfdd9be87d1462d599
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192017"
---
# <a name="avstream-samples"></a>AVStream 示例

示例 AVStream 微型驱动程序的源代码在 GitHub 上的 Windows 驱动程序工具包 (WDK) 示例中提供：

| 示例 | 说明 |
|--|--|
| [AVStream) 的以筛选器为中心的模拟捕获驱动程序 (Avssamp ](/samples/microsoft/windows-driver-samples/avstream-filter-centric-simulated-capture-sample-driver-avssamp/) | 模拟硬件模拟块的以 pin 为中心的捕获驱动程序，演示如何通过 AVStream 实现 DMA。 |
| [AVStream 模拟硬件示例驱动程序 (AVSHwS) ](/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/) | 以筛选为中心的捕获驱动程序，不 (DMA) 执行直接内存访问。 |

这些示例演示了本文档中所述的许多概念，并为驱动程序开发人员的需求定制了这些示例。