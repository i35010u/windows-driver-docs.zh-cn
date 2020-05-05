---
title: 启动设备 IRP 中的资源顺序
description: 启动设备 IRP 中的资源顺序
ms.assetid: df55105e-3da3-40cc-9f57-05632cb2d043
keywords:
- 资源的顺序 WDK PCI
- 启动-设备 IRP WDK PCI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fba7bee0e267206fa246f8b3bdf35a1618aae21
ms.sourcegitcommit: 49d7f27a24360559456063092ac35b2ba1aba7b1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82742615"
---
# <a name="order-of-resources-in-start-device-irp"></a>启动设备 IRP 中的资源顺序

在启动设备 i/o 请求数据包（IRP）中报告的资源的顺序应与 PCI 基址寄存器（条）中列出的资源顺序相匹配。 有两种类型的资源列表：原始资源列表和已转换资源列表。 每个资源列表都有资源描述符。 资源列表中的资源描述符按 PCI 设备上基址寄存器（条）的顺序排列。 原始列表和已翻译列表中的资源顺序相同。 在两个连续的资源说明符之间存在设备专用描述符数据。 条形的资源说明符后跟一个或多个用于扩展消息-已发出信号的中断（MSI-X）消息或一个用于 MSI 的描述符，或者一个或多个描述符用于基于硬件的中断。 在某些情况下，例如使用视频设备，例如，对于旧版视频资源，条的描述符后跟描述符。 保证资源列表中的条描述符顺序与所有硬件平台上 PCI 设备上的条的顺序相匹配。
