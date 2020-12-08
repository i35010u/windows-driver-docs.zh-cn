---
title: 快速启动与休眠唤醒的区分
description: 从 Windows 8 开始，快速启动模式可用于启动计算机的时间比传统的冷启动通常需要的时间少。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f5ac72edd63cf604bbf47be43e7e4db9079482ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817721"
---
# <a name="distinguishing-fast-startup-from-wake-from-hibernation"></a>快速启动与休眠唤醒的区分


从 Windows 8 开始，快速启动模式可用于启动计算机的时间比传统的冷启动通常需要的时间少。 快速启动是冷启动和从休眠唤醒启动的混合组合。 通常，内核模式设备驱动程序需要将快速启动区别于从休眠状态唤醒，使其设备按照用户的预期运行。 为了进行这种区分，驱动程序可以使用 [系统电源 irp](power-irps-for-the-system.md)中提供的信息。

在冷启动过程中，启动加载程序通过将 Windows 内核文件的部分加载到内存中并链接它们来构造内核内存映像。 接下来，内核配置核心系统功能、枚举连接到计算机的设备，并为其加载驱动程序。

与此相反，快速启动只是将休眠文件 ( # A0) 加载到内存中，以还原以前保存的 Windows 内核和加载的驱动程序映像。 快速启动往往比冷启动要少得多。

为了为快速启动做好准备，Windows 执行了混合关闭序列，该序列将完全关闭序列的元素和准备就绪的序列组合在一起。 首先，与完全关闭一样，Windows 会关闭所有应用程序并记录所有用户会话。 在此阶段，系统状态与刚刚启动的计算机（没有运行任何应用程序，但已加载 Windows 内核并且系统会话正在运行）类似。 接下来，电源管理器会将系统电源 Irp 发送到设备驱动程序，告诉他们准备设备进入休眠状态。 最后，Windows 将 (包含已加载的内核模式驱动程序) 中的内核内存映像保存 Hiberfil.sys 并关闭计算机。

默认情况下，Windows 8 使用快速启动来代替冷启动。 用户通常可以忽略快速启动和冷启动之间的差异，但为了满足用户的期望，快速启动应该与冷启动相同。 特别是，连接到计算机的设备应配置为 "快速启动"，因为它们适用于冷启动。

如果设备的驱动程序以不同的方式配置设备，具体取决于是否发生冷启动或唤醒，此驱动程序应在快速启动后，将设备配置为 "冷启动" (而不是 "唤醒") 出现。 例如，系统提供的 NDIS 驱动程序在快速启动时禁用了微型端口唤醒功能，而不是在从休眠状态唤醒。

若要将快速启动与从唤醒功能唤醒的状态区分开来，驱动程序可以检查系统设置-power ([**irp \_ MN \_ 设置 \_ power**](./irp-mn-set-power.md)) irp 中的信息，通知驱动程序计算机已进入 S0 (正常工作) 状态。 驱动程序的 [i/o 堆栈位置](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location) 此 IRP 包含一个 **power** 成员，该成员是包含与电源相关的信息的结构。 从 Windows Vista 开始， **Power** 成员结构包含一个 **SystemPowerStateContext** 成员，该成员是一个 [**系统 \_ 电源 \_ 状态 \_ 上下文**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_system_power_state_context) 结构，其中包含有关以前系统电源状态的信息。 此信息在 **系统 \_ 电源 \_ 状态 \_ 上下文** 结构的位域中进行编码。

**系统 \_ 电源 \_ 状态 \_ 上下文** 结构中的大多数位域是为系统使用而保留的，对驱动程序是不透明的。 但是，此结构包含两个位字段 **TargetSystemState** 和 **EffectiveSystemState**，驱动程序可以对其进行读取，以确定是否发生了快速启动或从休眠状态唤醒。

**TargetSystemState** 和 **EffectiveSystemState** 位域设置为 [**系统 \_ 电源 \_ 状态**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_system_power_state)枚举值。 如果 **TargetSystemState**  =  **PowerSystemHibernate** 和 **EffectiveSystemState**  =  **PowerSystemHibernate**，则会发生从休眠状态唤醒。

但是，如果 **TargetSystemState**  =  **PowerSystemShutdown** 和 **EffectiveSystemState**  =  **PowerSystemHibernate**，则会快速启动。

**TargetSystemState** 位域指定上次系统电源状态转换，驱动程序将在计算机关闭或进入休眠状态之前接收到系统电源 IRP。 " **EffectiveSystemState** 位" 字段指示该设备的以前的有效先前系统电源状态，如用户所示。 例如，如果驱动程序收到挂起的系统转换到休眠状态的通知，但随后发生了混合关闭，则 **TargetSystemState** 和 **EffectiveSystemState** 值可能不匹配。

有关详细信息，请参阅 [**系统 \_ 电源 \_ 状态 \_ 上下文**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_system_power_state_context)。

 

