---
title: 使用 BDA 筛选器测试 BDA 驱动程序
description: 使用 BDA 筛选器测试 BDA 驱动程序
keywords:
- 广播驱动程序体系结构 WDK AVStream，测试驱动程序
- BDA WDK AVStream，测试驱动程序
- 测试驱动程序 WDK，BDA
- DirectShow 筛选器 WDK AVStream
- 图形编辑器 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd69aff84a34115c9508a2fd82dcae41f0786905
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840483"
---
# <a name="testing-bda-drivers-using-bda-filters"></a>使用 BDA 筛选器测试 BDA 驱动程序





您可以使用 "DirectShow 筛选器图形编辑器" (*Graphedt.exe*) 在筛选器图中插入 BDA 组件的 DirectShow 筛选器实例，以便可以测试组件。 你可以从 Microsoft Windows 驱动程序工具包 (WDK) 获取图形编辑器。

您可以使用图形编辑器执行 BDA 组件的基本测试，如将组件的筛选器实例公开的 pin 连接到图形中的筛选器类型的其他针脚。

若要使用图形编辑器来全面测试您的 BDA 组件的功能，您必须构建一个以 BDA 网络提供程序筛选器开头的筛选器关系图，其中包含 BDA 组件的筛选器实例，并且至少通过一个信号量筛选器（ (数据包标识符 (PID) filter) 传输到传输信息筛选器 (.TIF) 。 使用图形编辑器时，最大的问题是：没有专用应用程序可通过网络提供程序筛选器实现的 **ITuner** 接口提交请求。 但是，网络提供程序筛选器具有相关的属性页，它们提供一些执行 **ITuner** 接口的有限功能。

 

 




