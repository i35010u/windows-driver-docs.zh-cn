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
ms.openlocfilehash: 3cc3990b9110cce2edb554f9659d256407ac5fc9
ms.sourcegitcommit: 3464f10ffa0727e38fbe225cfab52bb8c2bb1747
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2020
ms.locfileid: "93352984"
---
# <a name="tools-for-changing-boot-options-for-driver-testing-and-debugging"></a>用于更改驱动程序测试和调试启动选项的工具

若要在 Microsoft Windows 操作系统上测试和调试驱动程序，必须启用并配置在加载操作系统时创建的功能。 这些功能的设置包含在 *启动选项* 中，这些值用于确定启动加载程序如何加载和配置操作系统以及其他可启动程序和设备。


本部分介绍如何添加、删除和更改启动选项以创建操作系统的新负载配置，以及如何使用启动项参数自定义用于驱动程序测试和调试的负载配置。

通过编辑启动选项，你可以：

- 启用和配置调试

-  (HAL) 文件加载特定内核或硬件抽象层

- 限制 Windows 可用的物理内存

- 在32位版本的 Windows 上启用、禁用和配置物理地址扩展 (PAE) 

- 在用户模式和内核模式组件之间 Reapportion 虚拟地址空间 (3GB) 来测试非常小的内核模式地址空间中的驱动程序

- 启用和配置数据执行保护 (/noexecute) 

- 在无外设服务器上为紧急管理服务 (EMS) 控制台重定向指定端口

- 显示加载的驱动程序的名称

本节包括：

- [Windows 中的启动选项概述](boot-options-in-windows.md)。
- [启动选项标识符](boot-options-identifiers.md)
- [编辑启动选项](editing-boot-options.md)
- [BCD 引导选项参考](/windows-hardware/drivers/ddi/index)
- [使用启动参数](using-boot-parameters.md)
- [BCD 引导选项参考](bcd-boot-options-reference.md)
- [以前 Windows 版本中的启动选项](boot-options-in-previous-versions-of-windows.md)