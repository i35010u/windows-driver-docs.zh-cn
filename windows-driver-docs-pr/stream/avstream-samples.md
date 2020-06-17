---
title: AVStream 示例
description: AVStream 示例
ms.assetid: 18ddd9f1-d8bb-49a7-91bf-a8aeaa9565ad
keywords:
- AVStream WDK，示例
- 示例微型驱动程序 WDK AVStream
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: bb939ed7be8c3d1272fdc53482d26abea2d21120
ms.sourcegitcommit: 97a8d24b1b48602e4ccaa63a113f7c8cdb0c6df5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84812443"
---
# <a name="avstream-samples"></a>AVStream 示例

适用于 AVStream 微型驱动程序的源代码在 GitHub 上的 Windows 驱动程序工具包（WDK）示例中提供：

| 示例 | 说明 |
|--|--|
| [AVStream 以筛选器为中心的模拟捕获驱动程序（Avssamp）](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avstream-filter-centric-simulated-capture-sample-driver-avssamp/) | 模拟硬件模拟块的以 pin 为中心的捕获驱动程序，演示如何通过 AVStream 实现 DMA。 |
| [AVStream 模拟硬件示例驱动程序（AVSHwS）](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/) | 以筛选为中心的捕获驱动程序，该驱动程序不会执行直接内存访问（DMA）。 |

这些示例演示了本文档中所述的许多概念，并为驱动程序开发人员的需求定制了这些示例。
