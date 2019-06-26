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
- 加载配置 WDK 启动选项
ms.date: 04/19/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6e08f97513d125f2bad0365a6475883e63338afd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360427"
---
# <a name="tools-for-changing-boot-options-for-driver-testing-and-debugging"></a>用于更改驱动程序测试和调试启动选项的工具

若要测试和调试在 Microsoft Windows 操作系统上的驱动程序，必须启用并配置操作系统加载时建立的功能。 中包含这些功能的设置*启动选项*-用于确定如何启动加载程序加载和配置操作系统和其他可启动的程序和设备的值。


本部分介绍如何添加、 删除和更改引导选项以创建新的操作系统的负载配置以及如何使用启动入口参数以自定义负载测试和调试驱动程序的配置。

通过编辑启动选项，你可以：

- 启用并配置调试

- 加载特定内核或硬件抽象层 (HAL) 文件

- 限制可用于 Windows 的物理内存

- 启用、 禁用和配置在 32 位版本的 Windows 上的物理地址扩展 (PAE)

- Reapportion 用户模式和内核模式组件 (3 GB) 若要在非常小的内核模式地址空间中测试驱动程序之间的虚拟地址空间

- 启用并配置数据执行保护 (/ noexecute)

- 指定用于紧急管理服务 (EMS) 控制台重定向无外设的服务器上的端口

- 显示驱动程序的名称，因为它们的加载

本部分包括：

- [介绍启动选项](introduction-to-boot-options.md)
- [在 Windows 选项启动的概述](boot-options-in-windows.md)。
- [启动选项标识符](boot-options-identifiers.md)
- [编辑启动选项](editing-boot-options.md)
- [引用的 BCD 引导选项](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)
- [使用引导参数](using-boot-parameters.md)
- [跳过启动选项](bypassing-boot-options.md)
- [引用的 BCD 引导选项](bcd-boot-options-reference.md)
- [在以前版本的 Windows 的启动选项](boot-options-in-previous-versions-of-windows.md)

