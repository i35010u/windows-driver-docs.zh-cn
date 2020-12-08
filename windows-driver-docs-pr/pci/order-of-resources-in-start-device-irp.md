---
title: 启动设备 IRP 中的资源顺序
description: 启动设备 IRP 中的资源顺序
keywords:
- 资源的顺序 WDK PCI
- 启动-设备 IRP WDK PCI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05577c85f6326ff78fb98fdac377e50ad3897344
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812549"
---
# <a name="order-of-resources-in-start-device-irp"></a>启动设备 IRP 中的资源顺序

在 (IRP) 的启动设备 i/o 请求包中报告的资源的顺序应当与 PCI 基址寄存器 (条) 中列出的资源的顺序匹配。 有两种类型的资源列表：原始资源列表和已转换资源列表。 每个资源列表都有资源描述符。 资源列表中的资源描述符按基址寄存器 (条在 PCI 设备上) 的顺序排列。 原始列表和已翻译列表中的资源顺序相同。 在两个连续的资源说明符之间存在设备专用描述符数据。 条形的资源描述符后跟一个或多个描述符，用于扩展的消息-终止中断 (MSI-X) 消息或 MSI 的一个描述符或基于硬件的中断的一个或多个描述符。 在某些情况下，例如使用视频设备，例如，对于旧版视频资源，条的描述符后跟描述符。 保证资源列表中的条描述符顺序与所有硬件平台上 PCI 设备上的条的顺序相匹配。
