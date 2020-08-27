---
description: 本主题简要概述了如何使用 ETW 来检查 USB 选择性挂起状态，并使用 Windows PowerCfg 实用工具确定系统能源效率问题。
title: USB ETW 和电源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6429701d3ff790c60fe86ee1c64e6b6cd8b8002
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969238"
---
# <a name="usb-etw-and-power-management"></a>USB ETW 和电源管理


本主题简要概述了如何使用 ETW 来检查 USB 选择性挂起状态，并使用 Windows PowerCfg 实用工具确定系统能源效率问题。

如果 USB 设备驱动程序支持 [Usb 选择性挂起](usb-selective-suspend.md)，则它可以在设备空闲时关闭 usb 设备。 当设备不再处于空闲状态时，系统将唤醒设备并恢复正常操作。 当系统处于空闲状态且所有 USB 设备都处于挂起状态时，无需处理器活动，因此处理器进入低功耗状态。 正确实现选择性挂起会使移动系统的电力节省大幅提高并延长电池寿命。

你可以使用 USB ETW 来检查 USB 设备及其驱动程序，以验证它们是否成功进入选择性挂起状态。 无论你是系统制造商、IT 专业人员还是硬件开发人员，我们都建议你检查 USB 设备和驱动程序，以确保在将设备提供给最终用户之前，它们正确支持选择性挂起。

为了帮助你确定系统能源效率问题，我们在 Windows 7 中增强了 Windows PowerCfg 实用程序。 PowerCfg 是 Windows 附带的一个命令行实用工具，可用于启用电源策略枚举和配置。 通过使用 **-能量** 参数，可以实现为确定能源效率问题而进行的改进。 这些增强功能启用了 PowerCfg 来检查系统是否有常见的能源效率问题，并生成一个 HTML 报告，其中包含发现的任何问题。

PowerCfg 检测各种能源效率问题，其中包括未通过 USB 设备使用选择性挂起的有效使用、处理器利用率过高、计时器分辨率增加、性能低下且电池容量下降。 PowerCfg 确定不同的问题级别，包括服务器问题 (错误) 和小问题 (警告) 。

有关 Windows 电源管理和 PowerCfg 工具的详细信息，请参阅 [Powercfg 命令行选项](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc748940(v=ws.10)) 和 [使用 Powercfg 评估系统能源效率](https://docs.microsoft.com/previous-versions/windows/hardware/download/dn550976(v=vs.85))。

## <a name="related-topics"></a>相关主题
[Windows 的 USB 事件跟踪](usb-event-tracing-for-windows.md)  



