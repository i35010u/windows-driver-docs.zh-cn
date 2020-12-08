---
title: AVStream 示例
description: AVStream 示例
keywords:
- AVStream WDK，示例
- 示例微型驱动程序 WDK AVStream
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 08ff3b67d7894e3879d8e1ab4b331228aeb92963
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815839"
---
# <a name="avstream-samples"></a>AVStream 示例

示例 AVStream 微型驱动程序的源代码在 GitHub 上的 Windows 驱动程序工具包 (WDK) 示例中提供：

| 示例 | 说明 |
|--|--|
| [AVStream Filter-Centric 模拟捕获驱动程序 (Avssamp) ](/samples/microsoft/windows-driver-samples/avstream-filter-centric-simulated-capture-sample-driver-avssamp/) | 模拟硬件模拟块的以 pin 为中心的捕获驱动程序，演示如何通过 AVStream 实现 DMA。 |
| [AVStream 模拟硬件示例驱动程序 (AVSHwS) ](/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws/) | 以筛选为中心的捕获驱动程序，不 (DMA) 执行直接内存访问。 |

这些示例演示了本文档中所述的许多概念，并为驱动程序开发人员的需求定制了这些示例。
