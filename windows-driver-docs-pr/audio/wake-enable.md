---
title: 启用唤醒
description: 启用唤醒
keywords:
- HD 音频，启用唤醒
- 高清晰音频 (HD 音频) ，唤醒启用
- 唤醒启用 WDK 音频
- 状态-更改事件 WDK 音频
- 电源管理 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 213ba6f2b194f0a4336a12501d1df5d7115199c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800449"
---
# <a name="wake-enable"></a>启用唤醒


在关闭编解码器之前，编解码器函数驱动程序通常允许编解码器在编码解码器处于关闭状态的情况下唤醒系统。 对于音频编解码器，当用户插入输入插孔或从插孔中删除插头时，可以触发此类事件。 对于调制解调器编解码器，当电话响铃指示传入呼叫时，可能会发生状态更改事件。 有关状态更改事件的详细信息，请参阅 [INTEL HD 音频](https://www.intel.com/content/www/us/en/standards/intel-standards-and-initiatives.html)网站上的 *Intel 高质音频规范*。

若要准备关闭电源，函数驱动程序首先会将编解码器配置为在发生状态更改事件时向 HD 音频总线控制器发出信号。 接下来，函数驱动程序将 [**irp \_ MN \_ 等待 \_ 唤醒**](../kernel/irp-mn-wait-wake.md) 电源管理 irp 发送到 HD 音频总线驱动程序，告诉它从编解码器启用唤醒信号。 稍后，如果启用了唤醒信号，并且编解码器在编解码器的 SDI 行上传输状态更改事件，则控制器将为系统生成唤醒信号，并且总线驱动程序将通过完成 IRP \_ MN \_ 等待唤醒 IRP 来通知函数驱动程序 \_ 。

唤醒事件之后，总线驱动程序将确定哪些编解码器生成了唤醒信号，并 \_ \_ \_ 在该编解码器上完成任何挂起的 IRP MN 等待唤醒 irp。 但是，如果编解码器同时包含音频和调制解调器功能组，则总线驱动程序无法确定哪个函数组是唤醒信号的源。 在这种情况下，函数驱动程序必须将自己的查询发送到编解码器来验证唤醒信号的源。

 

