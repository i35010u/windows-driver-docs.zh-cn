---
title: 用于更改驱动程序测试和调试启动选项的工具
description: 用于更改驱动程序测试和调试启动选项的工具
ms.assetid: 4fd58868-7a43-42e3-adf9-5a82593c1675
keywords:
- 工具 WDK，启动选项
- 驱动程序开发工具 WDK，启动选项
- 启动选项 WDK
- 驱动程序测试 WDK 启动选项
- 测试驱动程序 WDK 启动选项
- 调试驱动程序 WDK 启动选项
- 驱动程序调试 WDK 启动选项
- 操作系统启动选项 WDK
- 负载配置 WDK 启动选项
ms.date: 04/19/2019
ms.localizationpriority: medium
ms.openlocfilehash: ea275914a28b606b5e58bacf250db537108829f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840302"
---
# <a name="tools-for-changing-boot-options-for-driver-testing-and-debugging"></a>用于更改驱动程序测试和调试启动选项的工具

若要在 Microsoft Windows 操作系统上测试和调试驱动程序，必须启用并配置在加载操作系统时创建的功能。 这些功能的设置包含在*启动选项*中，这些值用于确定启动加载程序如何加载和配置操作系统以及其他可启动程序和设备。


本部分介绍如何添加、删除和更改启动选项以创建操作系统的新负载配置，以及如何使用启动项参数自定义用于驱动程序测试和调试的负载配置。

通过编辑启动选项，你可以：

- 启用和配置调试

- 加载特定内核或硬件抽象层（HAL）文件

- 限制 Windows 可用的物理内存

- 在32位版本的 Windows 上启用、禁用和配置物理地址扩展（PAE）

- 在用户模式和内核模式组件（3GB）之间 Reapportion 虚拟地址空间，以测试非常小的内核模式地址空间中的驱动程序

- 启用和配置数据执行保护（/noexecute）

- 指定无外设服务器上的紧急管理服务（EMS）控制台重定向端口

- 显示加载的驱动程序的名称

本部分包括：

- [启动选项简介](introduction-to-boot-options.md)
- [Windows 中的启动选项概述](boot-options-in-windows.md)。
- [启动选项标识符](boot-options-identifiers.md)
- [编辑启动选项](editing-boot-options.md)
- [BCD 引导选项参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)
- [使用启动参数](using-boot-parameters.md)
- [跳过启动选项](bypassing-boot-options.md)
- [BCD 引导选项参考](bcd-boot-options-reference.md)
- [Windows 以前版本中的启动选项](boot-options-in-previous-versions-of-windows.md)

