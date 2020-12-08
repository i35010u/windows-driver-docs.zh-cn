---
title: 错误处理
description: 错误处理
keywords:
- Windows 硬件错误体系结构 WDK，错误处理
- WHEA WDK，错误处理
- 硬件错误 WDK WHEA，错误处理
- 错误 WDK WHEA，错误处理
- 更正的错误 WDK WHEA
- 未更正的错误 WDK WHEA
- 严重硬件错误 WDK WHEA
- 非致命硬件错误 WDK WHEA
- 低级别硬件错误处理程序 WDK WHEA
- LLHEHs WDK WHEA
- 平台特定硬件错误驱动程序 WDK WHEA
- PSHED WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06b78fc85e6c2c3078501a6017e59278478461cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837603"
---
# <a name="error-processing"></a>错误处理


Windows 硬件错误体系结构 (WHEA) 根据错误情况的分类，以不同方式处理硬件错误。 有关硬件错误的不同分类的详细信息，请参阅 " [硬件错误" 和 "错误源](hardware-errors-and-error-sources.md)"。

下面描述了 WHEA 执行的一系列操作，以响应每种类型的硬件错误条件。 有关这些操作中所引用的 WHEA 组件的详细信息，请参阅 [Windows 硬件错误体系结构的组件](components-of-the-windows-hardware-error-architecture.md)。

### <a name="corrected-hardware-error"></a>**更正的硬件错误**

1.   (*LLHEH*) 的 *低级硬件错误处理程序* 将收到有关硬件错误情况的通知。

2.  LLHEH 验证是否存在硬件错误。

3.  LLHEH 从错误源检索硬件错误信息，并使用错误数据填充硬件错误数据包。 此数据包的格式为 [WHEA \_ 错误 \_ 数据包](/previous-versions/windows/hardware/drivers/ff560465(v=vs.85)) 结构。

4.  LLHEH 调用到特定于 *平台的硬件错误驱动程序* (PSHED) 检索任何特定于平台的硬件错误信息。 如果安装了 PSHED 插件并注册了以参与错误信息检索，则 PSHED 将依次调用 PSHED 插件，以便进一步增加返回到 LLHEH 的错误信息的详细信息。

5.  LLHEH 调用 Windows 操作系统内核，并向其传递错误数据包。

6.  Windows 内核将创建 [错误记录](error-records.md) ，并使用从 LLHEH 收到的错误数据包中的信息填充该记录，并将其填充到有关错误的其他信息（如错误源、错误严重性以及错误发生的次数）。

7.  Windows 内核调入 PSHED，以允许 PSHED 向错误记录中添加部分。 如果安装了 PSHED 插件并注册了以参与错误信息检索，则 PSHED 将转到 PSHED 插件，以便进一步增加错误记录中的信息。

8.  Windows 内核调入 PSHED 以清除错误源的状态寄存器。 如果安装了 PSHED 插件并注册了以参与错误信息检索，则 PSHED 将再次调用 PSHED 插件，以便它能够清除错误源的状态寄存器。

9.  如果硬件错误条件超过错误源的错误阈值，Windows 内核将生成一个 ETW 事件，并在系统事件日志中记录错误消息。

### <a name="nonfatal-uncorrected-hardware-error"></a>**未更正的非致命硬件错误**

1.  系统会通知 LLHEH 出现硬件错误情况。

2.  LLHEH 验证是否存在硬件错误。

3.  LLHEH 从错误源检索硬件错误信息，并使用错误数据填充硬件错误数据包。

4.  LLHEH 调用 PSHED 来检索任何特定于平台的硬件错误信息。 如果安装了 PSHED 插件并注册了以参与错误信息检索，则 PSHED 将依次调用 PSHED 插件，以便进一步增加返回到 LLHEH 的错误信息的详细信息。

5.  LLHEH 调用 Windows 操作系统内核，并向其传递错误数据包。

6.  Windows 内核将创建 [错误记录](error-records.md) ，并使用从 LLHEH 收到的错误数据包中的信息填充该记录，并将其填充到有关错误的其他信息（如错误源、错误严重性以及错误发生的次数）。

7.  Windows 内核调入 PSHED，以允许 PSHED 向错误记录中添加部分。 如果安装了 PSHED 插件并注册了以参与错误信息检索，则 PSHED 将转到 PSHED 插件，以便进一步增加错误记录中的信息。

8.  Windows 内核尝试纠正硬件错误条件，尝试从错误中恢复。 然后，Windows 内核调入 PSHED，为其提供执行任何所需恢复操作的机会。 如果安装了 PSHED 插件并注册了以参与错误恢复，则 PSHED 将转而调入 PSHED 插件，以便它可以尝试更正错误，并/或执行从错误条件完全恢复所需的任何其他操作。

9.  如果已成功纠正硬件错误，Windows 内核将生成一个 ETW 事件，并在系统事件日志中记录错误消息。 如果未纠正硬件错误，Windows 内核将调入 PSHED 以保存错误记录。 如果安装了 PSHED 插件并注册了以参与错误记录持久性，则 PSHED 将转到 PSHED 插件，以便它能够保存错误记录。 保存错误记录后，Windows 内核将生成 bug 检查。

### <a name="fatal-uncorrected-hardware-error"></a>**错误的不更正硬件错误**

1.  系统会通知 LLHEH 出现硬件错误情况。

2.  LLHEH 验证是否存在硬件错误。

3.  LLHEH 从错误源检索硬件错误信息，并使用错误数据填充硬件错误数据包。

4.  LLHEH 调用 PSHED 来检索任何特定于平台的硬件错误信息。 如果安装了 PSHED 插件并注册了以参与错误信息检索，则 PSHED 将依次调用 PSHED 插件，以便进一步增加返回到 LLHEH 的错误信息的详细信息。

5.  LLHEH 调用 Windows 操作系统内核，并向其传递错误数据包。

6.  Windows 内核将创建 [错误记录](error-records.md) ，并使用从 LLHEH 收到的错误数据包中的信息填充该记录，并将其填充到有关错误的其他信息（如错误源、错误严重性以及错误发生的次数）。

7.  Windows 内核调入 PSHED 以保存错误记录。 如果安装了 PSHED 插件并注册了以参与错误记录持久性，则 PSHED 将转到 PSHED 插件，以便它能够保存错误记录。

8.  Windows 内核生成 bug 检查。

 

