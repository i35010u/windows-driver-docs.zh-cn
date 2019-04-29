---
title: 启动设备 IRP 中的资源顺序
description: 启动设备 IRP 中的资源顺序
ms.assetid: df55105e-3da3-40cc-9f57-05632cb2d043
keywords:
- 资源 WDK PCI 的顺序
- 启动设备 IRP WDK PCI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95d42a0e70ca1fd6db46c0b73b8a78f413dbdd9a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380545"
---
# <a name="order-of-resources-in-start-device-irp"></a>启动设备 IRP 中的资源顺序


报告开始设备 I/O 请求数据包 (IRP) 中的资源的顺序应与 PCI 基址寄存器 （条形图） 中列出的资源的顺序匹配。 有两种类型的资源的列表，原始和已翻译。 每个资源的列表包含资源描述符。 资源的列表中的资源描述符是按 PCI 设备上的基址寄存器 （条形图） 的顺序。 原始和已翻译列表中的资源的顺序是相同的。 两个连续资源描述符之间没有设备专用描述符数据。 条资源描述符后跟一个或多个描述符的扩展的消息信号中断 (MSI X) 消息，或一个描述符 MSI 或基于硬件的中断的一个或多个描述符。 在某些情况下，如使用视频设备，例如，图条的说明符后跟描述符的旧视频资源。 排序描述符的图条的资源列表中保证要匹配的 PCI 设备所有硬件平台上条。

 

 




