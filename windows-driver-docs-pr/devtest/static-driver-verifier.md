---
title: 静态驱动程序验证程序
description: 静态驱动程序验证程序
ms.assetid: 74feeb16-387c-4796-987a-aff3fb79b556
keywords:
- 验证驱动程序 WDK，静态驱动程序验证程序
- 驱动程序验证 WDK，静态驱动程序验证程序
- 静态驱动程序验证程序 WDK
- StaticDV WDK
- SDV WDK
- 路径 WDK SDV
- 编译时静态验证工具 WDK
ms.date: 06/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 09a4c0b0199670fc7720e274ff9b22865b2d313a
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383875"
---
# <a name="static-driver-verifier"></a>静态驱动程序验证程序

静态驱动程序验证程序 (也称为 "StaticDV" 或 "SDV" ) 是一个静态验证工具，可系统地分析 Windows 内核模式驱动程序的源代码。 SDV 是一种编译时工具，能够发现驱动程序中的缺陷和设计问题。 根据一组接口规则和操作系统模型，SDV 确定驱动程序是否与 Windows 操作系统内核正确交互。

## <a name="installing-static-driver-verifier"></a>安装静态驱动程序验证程序

静态驱动程序验证程序作为 [Windows 驱动程序工具包 ](../download-the-wdk.md) 的一部分提供， (wdk 在整个 wdk 体验和独立企业 WDK 中均) 。  此外，SDV 要运行的是 Visual Studio 的 Visual C++ 可再发行组件包。 参阅以下内容：

* [Visual Studio 2019 再分发](/visualstudio/releases/2019/redistribution)
* [适用于 Visual Studio 2017 的 Visual C++ 可再发行组件包](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)
* [适用于 Visual Studio 2013 的 Visual C++ 可再发行组件包](https://www.microsoft.com/download/details.aspx?id=40784)  

对于 Windows 10 版本1809或更早版本中可用的 SDV 版本，应安装 [适用于 Visual Studio 2012 的 Visual C++ 可再发行组件包](https://my.visualstudio.com/Downloads?pid=1452) ，而不是2017包。

## <a name="visual-studio-integration"></a>Visual Studio 集成

静态驱动程序验证程序已集成到 Visual Studio 中。 你可以在 Visual Studio 驱动程序项目上运行静态分析。 可以通过 Visual Studio 中的 " **驱动程序** " 菜单启动、配置和控制静态驱动程序验证程序。

## <a name="static-driver-verifier-documentation"></a>静态驱动程序验证程序文档

* [静态驱动程序验证程序的已知问题](../develop/static-driver-verifier-known-issues.md)：列出了静态驱动程序验证程序的最新已知问题
* [使用静态驱动程序验证器查找驱动程序中的缺陷](using-static-driver-verifier-to-find-defects-in-drivers.md)：说明在 Visual Studio 环境中开始分析驱动程序代码所需的内容。
* [静态驱动程序验证器命令 (MSBuild) ](-static-driver-verifier-commands--msbuild-.md)：列出用于在 Visual Studio 命令提示符窗口中运行 SDV 的 MSBuild 命令。
* [静态驱动程序验证程序简介](introducing-static-driver-verifier.md)：提供静态分析工具的概述。
* [使用静态驱动程序验证程序](using-static-driver-verifier.md)：提供有关使用和配置静态分析工具的详细信息。
* [静态驱动程序验证程序报表](static-driver-verifier-report.md)：介绍显示静态代码分析的详细跟踪的查看器。
* [静态驱动程序验证程序规则](static-driver-verifier-rules.md)：规则定义驱动程序模型和操作系统内核接口之间适当交互的要求。
* [静态驱动程序验证程序参考](static-driver-verifier-reference.md)：提供有关函数角色类型、SDV 配置文件、错误和警告消息的参考信息。

## <a name="finding-bugs-in-windows-driver-code"></a>在 Windows 驱动程序代码中查找 Bug

Microsoft 使用 SDV 来测试 Microsoft Windows 操作系统附带的内核模式驱动程序，并在 WDK 中测试示例驱动程序。 使用特定驱动程序模型的 DDI 符合性规则，SDV 可以验证驱动程序的正确行为。 例如，SDV 可以验证驱动程序：

* 以正确的 IRQL 调用函数
* 获取并释放正确序列中的锁
* 正确使用处理 i/o 请求数据包 (IRP 的函数) 

SDV 检查通过驱动程序代码的所有可能的路径。 它旨在查找不太可能在彻底测试中也不会遇到的隐匿路径中的严重错误。

## <a name="additional-resources"></a>其他资源

有关 SDV 可以验证的驱动程序的特定信息，请参阅 [支持的驱动程序](supported-drivers.md)

有关使用静态驱动程序验证程序的详细信息和提示，请参阅以下内容：

* [Windows 硬件认证博客](https://techcommunity.microsoft.com/t5/Windows-Hardware-Certification/bg-p/WindowsHardwareCertification)
* [Windows 内核社区网站](https://techcommunity.microsoft.com/t5/Windows-Kernel/ct-p/WindowsKernel)
* [Windows 硬件测试和认证论坛](https://social.msdn.microsoft.com/Forums/home?forum=whck)