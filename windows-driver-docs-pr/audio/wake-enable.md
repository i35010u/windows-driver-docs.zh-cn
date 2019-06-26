---
title: 启用唤醒
description: 启用唤醒
ms.assetid: f4a2d4b1-d3a0-449a-ac65-a448d2bcab5c
keywords:
- HD Audio，唤醒启用
- 高清晰度音频 (HD Audio) 唤醒启用
- 唤醒启用 WDK 音频
- 状态更改事件 WDK 音频
- 电源管理 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 670a7ced6bfc9f238d7f4bf05fff3872c81ca594
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364807"
---
# <a name="wake-enable"></a>启用唤醒


之前关闭编解码器，编解码器功能驱动程序通常情况下允许要唤醒系统，如果编解码器处于关闭状态时发生的状态更改事件的编解码器。 有关音频编解码器，这种情况下可以在用户输入插孔中插入即插即用或删除从插孔的即插即用时触发。 对于调制解调器编解码器，电话响铃以指示的传入呼叫时，可以发生的状态更改事件。 有关状态更改事件的详细信息，请参阅*Intel 高定义音频规范*处[Intel HD Audio](https://go.microsoft.com/fwlink/p/?linkid=42508)网站。

若要准备关闭，功能驱动程序首先配置要发出信号 HD Audio 总线控制器的状态更改事件发生时的编解码器。 接下来，功能驱动程序发送[ **IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) HD Audio 总线驱动程序的电源管理 IRP 告诉它要启用从唤醒信号编解码器。 更高版本，如果启用了唤醒信号，并且通过编码解码器的 SDI 行编解码器将传输的状态更改事件，控制器生成到系统唤醒信号和总线驱动程序通知功能驱动程序通过完成 IRP\_MN\_等待\_唤醒 IRP。

以下为总线驱动程序确定哪些编解码器生成唤醒信号并完成任何挂起的 IRP\_MN\_等待\_唤醒 Irp 上该编解码器。 但是，如果编解码器包含音频和调制解调器函数组，例如，总线驱动程序具有无法确定哪些函数组是唤醒信号的源。 在这种情况下，功能驱动程序必须将其自己的查询发送到编解码器来验证唤醒信号源。

 

 




