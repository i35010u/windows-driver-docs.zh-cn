---
title: 启用到 D3cold 的转换
description: 所有版本的 Windows 都允许设备处于 D3cold 状态，而计算机 (进入系统低功耗状态，即 S1 到 S4) 。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c6a126346cb6918379aaba63921ae9f8b4c788a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819453"
---
# <a name="enabling-transitions-to-d3cold"></a>启用到 D3cold 的转换


所有版本的 Windows 都允许设备处于 D3cold 状态，而计算机 (进入系统低功耗状态，即 S1 到 S4) 。 在计算机退出 S0 之前，函数驱动程序、总线驱动程序和筛选器驱动程序协同工作以将设备移至 D3hot。 当计算机进入低功耗 Sx 状态时，此转换的副作用是将设备从 D3hot 移动到 D3cold。

从 Windows 8 开始，设备可以进入并退出 D3cold，而计算机仍在 S0 中。 作为设备的电源策略所有者 (PPO) 的驱动程序可以启用和禁用这些到 D3cold 的转换。 驱动程序不应使其设备进入 D3cold，除非设备可以（如果需要）从 D3cold 唤醒，然后在转换为 D0 后恢复正常操作。

设备进入 D3 后，最初进入 d3 的 D3hot 子情况。 在 D3hot 中，设备可以输入 D0 或 D3cold。 对于唤醒事件或 i/o 请求，设备从 D3hot 进入 D0。 否则，该设备可能会保留在 D3hot 中，也可能从 D3hot 移动到 D3cold。 有关这些转换的详细信息，请参阅设备电源状态图中的 [设备电源](device-power-states.md)状态。

该驱动程序不启动设备从 D3hot 到 D3cold 的转换。 相反，当与此设备共享公共电源的所有其他设备处于 D3hot 并准备好进入 D3cold 时，将发生此转换。 当这些设备中的最后一个进入 D3hot 时，基础总线驱动程序和系统固件会删除电源，并且设备会一起进入 D3cold。

设备的 PPO 驱动程序告诉操作系统是否允许设备从 D3hot 转换为 D3cold。 驱动程序可在安装设备的 INF 文件中提供此信息，或驱动程序可在运行时调用 [*SetD3ColdSupport*](/windows-hardware/drivers/ddi/wdm/nc-wdm-set_d3cold_support) 例程以动态启用或禁用设备到 D3cold 的转换。 有关详细信息，请参阅 [使用 GUID \_ D3COLD \_ 支持 \_ 接口驱动程序接口](using-guid-d3cold-support-interface.md)。

通过使设备进入 D3cold，驱动程序可保证以下行为：

-   当计算机停留在 S0 中时，设备可以容忍从 D3hot 到 D3cold 的转换。
-   当设备从 D3cold 返回到 D0 时，它将正常工作。

输入 D3cold 后，无法满足任一要求的设备可能会在计算机重新启动或进入睡眠状态之后才可用。 如果设备必须能够从其输入的任何低功耗 Dx 状态向唤醒事件发出信号，则除非驱动程序确定设备的唤醒信号在 D3cold 中起作用，否则不能启用条目进入 D3cold。

在 D3cold 中放置设备并不一定意味着已删除设备的所有电源源;这意味着，仅允许通过总线与设备进行通信的电源源丢失。 设备仍可以通过足够的功率来向处理器发出唤醒事件信号。 例如，以太网网络接口卡 (NIC) ，其主电源被删除可能会消耗以太网电缆的电源。

由于 D3cold 是一个不能用于与设备进行通信的状态，因此驱动程序无法直接将其设备置于 D3cold 中。 相反，驱动程序首先调用 [**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp) 例程来请求一个 D3 power IRP ([**irp \_ MN \_ 设置 \_**](./irp-mn-set-power.md) 具有 target state = **PowerDeviceD3**) 的 Power 请求，将设备从 D0 移到 D3hot。 输入 D3hot 后，设备可能会也可能不会从 D3hot 移动到 D3cold。 仅当删除总线时，设备才会进入 D3cold，如果父总线驱动程序关闭总线或系统固件关闭了硬件平台的某个部分，则会发生这种情况。

 

