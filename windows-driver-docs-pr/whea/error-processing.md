---
title: 错误处理
description: 错误处理
ms.assetid: d9cb2f62-1ccf-4ab6-b547-dc54f6d07820
keywords:
- Windows 硬件错误体系结构 WDK、 错误处理
- WHEA WDK 错误处理
- 硬件错误 WDK WHEA 错误处理
- 错误 WDK WHEA 错误处理
- 已更正的错误 WDK WHEA
- 未更正的错误 WDK WHEA
- 致命硬件错误 WDK WHEA
- 非致命硬件错误 WDK WHEA
- 低级别的硬件错误处理程序 WDK WHEA
- LLHEHs WDK WHEA
- 特定于平台的硬件错误驱动程序 WDK WHEA
- PSHED WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b30a07f2179c525fc9ddcd124f227b3463fe13fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575992"
---
# <a name="error-processing"></a>错误处理


Windows 硬件错误体系结构 (WHEA) 的错误条件的分类根据不同的方式来处理硬件错误。 有关硬件错误的不同分类的详细信息，请参阅[硬件错误和错误源](hardware-errors-and-error-sources.md)。

下面介绍 WHEA 为每个类型的硬件错误条件的响应中所采取的操作序列。 有关这些操作中引用的 WHEA 组件的详细信息，请参阅[Windows 硬件错误体系结构的组件](components-of-the-windows-hardware-error-architecture.md)。

### <a name="corrected-hardware-error"></a>**已更正的硬件错误**

1.  *低级别的硬件错误处理程序*(*LLHEH*) 通知的硬件错误条件是否存在。

2.  LLHEH 验证存在硬件错误。

3.  LLHEH 检索错误源中的硬件错误信息，并使用错误数据来填充硬件错误数据包中。 此数据包的格式设置为[WHEA\_错误\_数据包](https://msdn.microsoft.com/library/windows/hardware/ff560465)结构。

4.  调入 LLHEH*特定于平台的硬件错误驱动程序*(PSHED) 来检索特定于平台的硬件错误的任何信息。 如果 PSHED 插件已安装并且正在注册参与错误信息检索，PSHED 将反过来调入 PSHED 插件，以便它可以进一步扩充 LLHEH 到返回的错误信息。

5.  LLHEH 调用 Windows 操作系统内核，并向其传递错误数据包。

6.  创建 Windows 内核[错误记录](error-records.md)并填充使用 LLHEH 从接收到的错误数据包中的信息，以及有关该错误，例如错误源，错误的严重级别的其他信息和发生了错误的次数。

7.  Windows 内核调用 PSHED 允许 PSHED 将部分添加到的错误记录。 如果 PSHED 插件已安装并且正在注册参与错误信息检索，PSHED 将反过来调入 PSHED 插件，以便它可以进一步扩充错误记录中的信息。

8.  Windows 内核调用 PSHED 以清除错误源的状态寄存器。 如果 PSHED 插件将安装并注册参与错误信息检索，PSHED 会反过来调用插件，以便它可以 PSHED 清除错误源的状态注册。

9.  如果硬件错误条件超过错误源的错误阈值，Windows 内核会生成一个 ETW 事件和系统事件日志中记录错误的信息。

### <a name="nonfatal-uncorrected-hardware-error"></a>**非致命未更正的硬件错误**

1.  LLHEH 通知存在硬件错误条件。

2.  LLHEH 验证存在硬件错误。

3.  LLHEH 检索错误源中的硬件错误信息，并使用错误数据来填充硬件错误数据包中。

4.  若要检索特定于平台的硬件错误的任何信息 PSHED LLHEH 调用。 如果 PSHED 插件已安装并且正在注册参与错误信息检索，PSHED 将反过来调入 PSHED 插件，以便它可以进一步扩充 LLHEH 到返回的错误信息。

5.  LLHEH 调用 Windows 操作系统内核，并向其传递错误数据包。

6.  创建 Windows 内核[错误记录](error-records.md)并填充使用 LLHEH 从接收到的错误数据包中的信息，以及有关该错误，例如错误源，错误的严重级别的其他信息和发生了错误的次数。

7.  Windows 内核调用 PSHED 允许 PSHED 将部分添加到的错误记录。 如果 PSHED 插件已安装并且正在注册参与错误信息检索，PSHED 将反过来调入 PSHED 插件，以便它可以进一步扩充错误记录中的信息。

8.  Windows 内核会尝试从错误中恢复尝试更正硬件错误条件。 Windows 内核然后调入 PSHED 以便为其提供执行任何所需的恢复操作的机会。 如果 PSHED 插件将安装并注册参与错误恢复，PSHED 会反过来调用 PSHED 插件，以便它可以尝试更正错误和/或执行完全所需的任何其他操作从错误中恢复。

9.  如果已成功更正硬件错误，Windows 内核会生成一个 ETW 事件和系统事件日志中记录错误的信息。 如果未更正硬件错误，Windows 内核调用 PSHED 保存错误记录。 如果 PSHED 插件安装，并且将注册为参与错误记录持久性，PSHED 将又调入 PSHED 插件，以便它可以保存错误记录。 保存错误记录后，Windows 内核将生成的 bug 检查。

### <a name="fatal-uncorrected-hardware-error"></a>**严重未更正的硬件错误**

1.  LLHEH 通知存在硬件错误条件。

2.  LLHEH 验证存在硬件错误。

3.  LLHEH 检索错误源中的硬件错误信息，并使用错误数据来填充硬件错误数据包中。

4.  若要检索特定于平台的硬件错误的任何信息 PSHED LLHEH 调用。 如果 PSHED 插件已安装并且正在注册参与错误信息检索，PSHED 将反过来调入 PSHED 插件，以便它可以进一步扩充 LLHEH 到返回的错误信息。

5.  LLHEH 调用 Windows 操作系统内核，并向其传递错误数据包。

6.  创建 Windows 内核[错误记录](error-records.md)并填充使用 LLHEH 从接收到的错误数据包中的信息，以及有关该错误，例如错误源，错误的严重级别的其他信息和发生了错误的次数。

7.  Windows 内核调用 PSHED 保存错误记录。 如果 PSHED 插件安装，并且将注册为参与错误记录持久性，PSHED 将又调入 PSHED 插件，以便它可以保存错误记录。

8.  Windows 内核将生成的 bug 检查。

 

 




