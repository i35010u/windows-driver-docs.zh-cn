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
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: b4f8e49a6af8cf8da041fb8bb347c93988febf5e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564433"
---
# <a name="tools-for-changing-boot-options-for-driver-testing-and-debugging"></a>用于更改驱动程序测试和调试启动选项的工具

若要测试和调试在 Microsoft Windows 操作系统上的驱动程序，必须启用并配置操作系统加载时建立的功能。 中包含这些功能的设置*启动选项*-用于确定如何启动加载程序加载和配置操作系统和其他可启动的程序和设备的值。

> [!TIP] 
> 如果使用 Windows Driver Kit (WDK) 8，您可以配置用于测试和调试从 Visual Studio 的计算机。 配置测试计算机时，WDK 驱动程序测试框架将自动启用测试计算机进行远程调试，并传输测试二进制文件和支持文件。 有关详细信息，请参阅[预配计算机，以使驱动程序部署和测试 (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)，或[预配计算机，以使驱动程序部署和测试 (WDK 8)](https://msdn.microsoft.com/library/windows/hardware/hh698272)，和[如何测试在驱动程序运行时使用 Visual Studio](https://docs.microsoft.com/windows-hardware/drivers/develop/testing-a-driver-at-runtime)。

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
- [编辑启动选项](editing-boot-options.md)
- [Boot.ini 引导参数引用](https://msdn.microsoft.com/library/windows/hardware/ff542248)
- [引用的 BCD 引导选项](https://msdn.microsoft.com/library/windows/hardware/ff542205)
- [使用引导参数](using-boot-parameters.md)
- [跳过启动选项](bypassing-boot-options.md)

从 Windows Vista 开始，Windows 包括一个新的引导加载程序体系结构、 新的启动选项和新的启动选项编辑器。 有关信息，请参阅[Windows Vista 中的启动选项](boot-options-in-windows-vista-and-later.md)。
