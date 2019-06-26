---
Description: 本主题提供了一条简短大致了解使用 ETW 来检查 USB 选择性挂起状态和使用 Windows PowerCfg 实用程序确定系统能源效率问题。
title: USB ETW 和电源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7344397f386329b57b44b134df13a776a40d2f7f
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391767"
---
# <a name="usb-etw-and-power-management"></a>USB ETW 和电源管理


本主题提供了一条简短大致了解使用 ETW 来检查 USB 选择性挂起状态和使用 Windows PowerCfg 实用程序确定系统能源效率问题。

如果 USB 设备驱动程序支持[USB 选择性挂起](usb-selective-suspend.md)，它可以关闭 USB 设备时在设备处于空闲状态。 当设备不再处于空闲状态时，系统唤醒设备，并恢复正常操作。 当系统处于空闲状态，且所有 USB 设备将被都挂起时，没有处理器活动是必需的因此处理器进入低功耗状态。 正确实现选择性挂起可能会导致重大节能和适用于移动系统延长的电池寿命。

您可以使用 USB ETW 检查 USB 设备和其驱动程序以验证是否成功投入选择性挂起。 无论您是系统制造商、 IT 专业人员或硬件开发人员，我们建议您检查自己的 USB 设备和驱动程序，以确保它们正确支持选择性挂起之前向最终用户提供的设备。

为了帮助您识别系统的能源效率问题，我们增强了 Windows 7 中的 Windows PowerCfg 实用程序。 PowerCfg 是使电源策略枚举和配置的 Windows 附带的命令行实用工具。 PowerCfg 确定能源效率的增强功能执行使用 **-能源**参数。 这些增强功能使 PowerCfg 来检查系统的能源效率的常见问题并生成 HTML 报表，其中包含它发现的任何问题。

PowerCfg 检测到通过 USB 设备、 过多的处理器利用率、 增加了的计时器分辨率、 电源效率低下策略设置和电池容量下降的问题，包括无法做到有效利用选择性挂起的各种能源效率。 PowerCfg 标识不同级别的问题，包括服务器问题 （错误） 以及一些小问题 （警告）。

Windows 电源管理和 PowerCfg 工具的详细信息，请参阅[Powercfg 命令行选项](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-vista/cc748940(v=ws.10))并[使用 PowerCfg 评估系统能效](https://docs.microsoft.com/previous-versions/windows/hardware/download/dn550976(v=vs.85))。

## <a name="related-topics"></a>相关主题
[USB Windows 事件跟踪](usb-event-tracing-for-windows.md)  



