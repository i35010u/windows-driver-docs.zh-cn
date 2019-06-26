---
title: 快速启动与休眠唤醒的区分
description: 从 Windows 8 开始，快速启动模式，可在更少的时间比通常需要传统，冷启动中启动计算机。
ms.assetid: 1768F739-619A-441F-B270-029DD1F72953
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6e336c2915898fc5d72abfffd9a8a515273a8674
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384965"
---
# <a name="distinguishing-fast-startup-from-wake-from-hibernation"></a>快速启动与休眠唤醒的区分


从 Windows 8 开始，快速启动模式，可在更少的时间比通常需要传统，冷启动中启动计算机。 快速启动是混合组合的冷启动和唤醒从休眠状态启动。 通常情况下，需要将快速初创企业与唤醒从休眠区分开来，使其设备的行为像预期的用户内核模式设备驱动程序。 若要弄清楚这一点，驱动程序可以使用信息现已推出[系统电源 Irp](power-irps-for-the-system.md)。

在冷启动的启动加载器构造内核内存图像，方法是加载到内存中的 Windows 内核文件的部分并将它们链接。 接下来，内核配置核心系统功能、 枚举的设备连接到计算机，并为其加载驱动程序。

与此相反，快速启动只需将休眠文件 (Hiberfil.sys) 加载到内存来还原以前保存的图像的 Windows 内核和加载的驱动程序。 快速启动往往会比冷启动时间大大减少。

若要准备快速启动，Windows 会执行将完全关闭序列的元素组合的混合关闭序列和准备的休眠序列。 首先，如下所示完全关机，Windows 将关闭所有应用程序，并注销所有用户会话。 在此阶段，系统状态是类似于只需启动的计算机 — 任何应用程序正在运行，但加载 Windows 内核和系统会话正在运行。 接下来，电源管理器将发送系统电源 Irp 到设备驱动程序，让他们准备自己的设备进入休眠状态。 最后，Windows 将内核内存映像 （包括加载的内核模式驱动程序） 保存在 Hiberfil.sys 并关闭计算机。

默认情况下，Windows 8 使用代替冷启动快速启动。 用户通常可以忽略快速和冷初创企业之间的差异，但为了满足用户的期望，快速创业公司应行为冷启动相同。 具体而言，应连接到计算机的设备配置相同的快速启动，而会为冷启动。

如果设备驱动程序配置以不同的方式取决于是否冷启动或唤醒从休眠发生设备，此驱动程序应，快速启动后, 配置设备像是冷启动 （而不是唤醒-从-休眠状态）出现。 例如，系统提供的 NDIS 驱动程序禁用快速启动，但不是用于唤醒从休眠的微型端口唤醒功能。

若要从唤醒从休眠中区分快速启动，驱动程序可以检查系统集电源中的信息 ([**IRP\_MN\_设置\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)) IRP告知驱动程序在计算机已进入 S0 （工作） 状态。 在驱动程序[I/O 堆栈位置](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)在此 IRP 包含**Power**成员，它是一个结构，包含与电源相关的信息。 从 Windows Vista 开始**电源**成员结构包含**SystemPowerStateContext**成员，即[**系统\_POWER\_状态\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_system_power_state_context)结构，其中包含之前的系统电源状态有关的信息。 此信息采用位域进行编码**系统\_电源\_状态\_上下文**结构。

中的位字段的大多数**系统\_电源\_状态\_上下文**结构仅供系统使用，是不透明的驱动程序。 但是，此结构包含两个位域**TargetSystemState**并**EffectiveSystemState**，可以读取由驱动程序以确定是否有快速启动或唤醒从休眠发生。

**TargetSystemState**并**EffectiveSystemState**位域设置为[**系统\_POWER\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_system_power_state)枚举值。 如果**TargetSystemState** = **PowerSystemHibernate**并**EffectiveSystemState** = **PowerSystemHibernate**，唤醒从休眠发生。 但是，如果**TargetSystemState** = **PowerSystemHibernate**并**EffectiveSystemState**  =  **PowerSystemShutdown**，快速启动。

**TargetSystemState**位域指定为其驱动程序收到系统电源 IRP，计算机关闭或进入休眠状态前的最后一个系统电源状态转换。 **EffectiveSystemState**位字段指示有效的上一系统电源状态的设备，所识别的用户。 **TargetSystemState**并**EffectiveSystemState**如果，例如，驱动程序收到通知正在等待系统转换为休眠状态，但混合的值可能不匹配关闭随后发生。

有关详细信息，请参阅[**系统\_POWER\_状态\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_system_power_state_context)。

 

 




