---
title: 静态驱动程序验证程序
description: 静态驱动程序验证程序
ms.assetid: 74feeb16-387c-4796-987a-aff3fb79b556
keywords:
- 验证驱动程序 WDK、 Static Driver Verifier
- 驱动程序验证 WDK、 Static Driver Verifier
- WDK 的 static Driver Verifier
- StaticDV WDK
- SDV WDK
- 路径 WDK SDV
- 编译时静态验证工具 WDK
ms.date: 06/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0b1dd0732b11b435d4956ffca95b1be938482fbe
ms.sourcegitcommit: f520be298d14434610dd8b824adc81218ea68e58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67141833"
---
# <a name="static-driver-verifier"></a>静态驱动程序验证程序

Static Driver Verifier （也称为"StaticDV"或"SDV"） 是一个静态验证工具，系统化地分析 Windows 内核模式驱动程序的源代码。 SDV 是一种编译时工具，能够发现缺陷和驱动程序中的设计问题。 根据一组接口规则和操作系统的模型，SDV 确定驱动程序是否正确交互与 Windows 操作系统内核。

## <a name="installing-static-driver-verifier"></a>安装的 Static Driver Verifier

Static Driver Verifier 可作为的一部分[Windows Driver Kit (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)和独立企业 WDK 中完整的 WDK 体验。  此外，视觉对象C++用于 Visual Studio 可再发行组件包所需的 SDV 来运行。 请参阅以下内容：

* [Visual Studio 2019 重新分发](https://docs.microsoft.com/visualstudio/releases/2019/redistribution)
* [VisualC++用于 Visual Studio 2017 可再发行组件包](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)
* [Visual C++ Visual Studio 2013 可再发行组件包](https://www.microsoft.com/download/details.aspx?id=40784)  

对于版本的 WDK 为 Windows 10，版本 1809年或更早版本中可用的 SDV [VisualC++用于 Visual Studio 2012 可再发行组件包](https://my.visualstudio.com/Downloads?pid=1452)应安装而不是 2017年包。

## <a name="visual-studio-integration"></a>Visual Studio 集成

Static Driver Verifier 集成到 Visual Studio。 在 Visual Studio 驱动程序项目，可以运行静态分析。 可以启动、 配置和控制从 Static Driver Verifier**驱动程序**Visual Studio 菜单中的。

## <a name="static-driver-verifier-documentation"></a>Static Driver Verifier 文档

* [Static Driver Verifier 的已知问题](https://docs.microsoft.com/windows-hardware/drivers/develop/static-driver-verifier-known-issues):Static Driver Verifier 列出了最新的已知的问题
* [使用 Static Driver Verifier 驱动程序中查找缺陷](using-static-driver-verifier-to-find-defects-in-drivers.md):告诉您需要开始分析驱动程序代码在 Visual Studio 环境中。
* [静态 Driver Verifier 命令 (MSBuild)](-static-driver-verifier-commands--msbuild-.md):列出要使用的 Visual Studio 命令提示符窗口中运行 SDV 的 MSBuild 命令。
* [引入的 Static Driver Verifier](introducing-static-driver-verifier.md):提供了静态分析工具的概述。
* [使用 Static Driver Verifier](using-static-driver-verifier.md):提供了有关使用和配置的静态分析工具的详细信息。
* [Static Driver Verifier 报表](static-driver-verifier-report.md):描述的查看器显示的静态代码分析详细的跟踪。
* [Static Driver Verifier 规则](static-driver-verifier-rules.md):规则定义所需的正确驱动程序模型和操作系统的内核接口之间的交互。
* [Static Driver Verifier 引用](static-driver-verifier-reference.md):提供了有关函数的角色类型、 SDV 配置文件、 错误和警告消息的参考信息。

## <a name="finding-bugs-in-windows-driver-code"></a>Windows 驱动程序代码中查找错误

Microsoft 使用 SDV 来测试是 Microsoft Windows 操作系统附带的内核模式驱动程序，并在 WDK 中测试的示例驱动程序。 通过对特定驱动程序模型使用 DDI 符合性规则，SDV 可以验证正确的驱动程序行为。 例如，SDV 可以验证该驱动程序：

* 在正确的 IRQL 调用函数
* 获取和释放锁正确的顺序
* 正确使用函数，用于处理 I/O 请求数据包 (IRP)

SDV 检查通过驱动程序代码的所有可能路径。 它旨在彻底的测试中甚至不太可能会遇到的晦涩路径中查找出现严重的错误。

## <a name="additional-resources"></a>其他资源

SDV 可以验证的驱动程序相关的特定信息，请参阅[支持驱动程序](supported-drivers.md)

有关详细信息和有关使用 Static Driver Verifier 的提示，请参阅以下文章：

* [Windows 硬件认证博客](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)
* [Windows 内核社区站点](https://techcommunity.microsoft.com/t5/Windows-Kernel/ct-p/WindowsKernel)
* [Windows 硬件测试和认证论坛](https://social.msdn.microsoft.com/Forums/home?forum=whck)
