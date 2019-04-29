---
title: SerCx I/O 控制请求
description: SerCx 支持串行 I/O 控制请求的列表。
ms.assetid: 2697096f-73a2-4474-9040-e1cadbb10b1e
keywords:
- SerCx Ioctl
ms.date: 11/30/2017
ms.localizationpriority: medium
ms.openlocfilehash: df64636c9cba08c5927cdd131bb1f096f2716f6f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388020"
---
# <a name="sercx-io-control-requests"></a>SerCx I/O 控制请求

但有少数例外，版本 1 的串行框架扩展 (SerCx) 支持使用 Ntddser.h 标头文件中定义的 IOCTL_SERIAL_XXX I/O 控制代码 (Ioctl) 的 I/O 控制请求。 SerCx 会处理一些这些请求，但 SerCx 必须依赖于串行控制器驱动程序处理许多需要特定于硬件的处理其他请求。 某些由 SerCx 处理的请求还需要特定于硬件的处理。 尽管 SerCx 负责完成这些请求，将卸载 SerCx 众多串行控制器驱动程序对这些请求的处理。

这些 Ioctl 大部分也受系统提供 Serial.sys 驱动程序，它管理的电脑上的命名串行端口。 Serial.sys 是在所有支持的 Windows 版本中可用。 串行 Ioctl 的详细说明，请参阅[串行设备控制请求](serial-device-control-requests2.md)。

SerCx 不支持所有 Ioctl Ntddser.h 标头文件中定义的。 SerCx 不支持已过时 IOCTL_SERIAL_CONFIG_SIZE IOCTL，不能由客户端外围设备驱动程序。 也不支持是 IOCTL_SERIAL_RESET_DEVICE IOCTL，SerCx 始终完成 STATUS_NOT_IMPLEMENTED 错误状态代码。 此外，SerCx 支持无 IOCTL_SERIAL_INTERNAL_XXX Ioctl Ntddser.h 中定义的。

许多 SerCx 支持 Ioctl 用于串行端口上配置硬件设置。 打开串行端口之后, 在客户端应假定串行端口处于未知或未定义状态，而不是已知的默认状态。 客户端将负责配置串行端口，这样就可供使用。

Ioctl SerCx 支持的大多数都由 EvtSerCxControl 回调函数，以实现串行控制器驱动程序处理。 SerCx 处理八个串行 Ioctl 而不会调用 EvtSerCxControl 函数。 但是，若要处理某些这些 Ioctl，SerCx 需要协助以外 EvtSerCxControl 串行控制器驱动程序中的回调函数。 有关详细信息，请参阅 Ioctl SerCx 由处理。

## <a name="ioctls-handled-by-the-evtsercxcontrol-function"></a>Ioctl EvtSerCxControl 函数处理

如果 SerCx 接收的 I/O 控制请求具有 SerCx 不支持 IOCTL，SerCx 调用串行控制器驱动程序的 EvtSerCxControl 回调函数来处理该请求。 在响应中，此函数必须完成的请求。 但是，此函数不可能处理收到的所有 I/O 控制请求。 如果 EvtSerCxControl 函数收到无法识别或支持 IOCTL，它应完成 STATUS_NOT_IMPLEMENTED 错误状态代码的请求。
一些 EvtSerCxControl 函数处理的 I/O 控制请求可能会更改配置或以某种方式的串行控制器的行为。 若要避免错误，外围设备驱动程序应避免发送 I/O 控制请求，以重新配置控制器，而控制器仍在处理挂起的传输或接收操作。 此外，此外围设备驱动程序应避免启动新的传输或接收操作，直到串行控制器驱动程序已完成任何挂起的 I/O 控制请求，可能会更改控制器的配置。

通常情况下，许多 SerCx 发送给 EvtSerCxControl 函数请求可以完成此函数在返回之前。 如果请求需要延迟的处理，该函数可以计划 DPC 例程或辅助线程来完成该请求。 出于性能原因，该函数应避免不必要地计划不需要延迟的处理的操作的 DPC 例程或辅助线程。

SerCx 不会尝试序列化对 EvtSerCxControl 函数的调用。 这些调用可能来自不同线程中并发出现和可能在同一时间运行的 EvtSerCxControl 函数的两个或多个调用。

## <a name="ioctls-handled-by-sercx"></a>Ioctl SerCx 由处理

SerCx 处理，并完成而无需从串行控制器驱动程序，帮助 IOCTL_SERIAL_GET_TIMEOUTS 和 IOCTL_SERIAL_SET_TIMEOUTS 请求但 SerCx 并不将当前的超时参数应用到传输接收操作，该驱动程序执行。 串行控制器驱动程序可以通过调用 SerCxGetReadIntervalTimeout 方法获取当前的读取时间间隔的超时值。 有关超时的详细信息，请参阅 SERIAL_TIMEOUTS。

SerCx 处理，并完成 IOCTL_SERIAL_APPLY_DEFAULT_CONFIGURATION 请求。 此请求的处理，过程 SerCx 调用驱动程序的 EvtSerCxApplyConfig 回调函数来配置串行控制器在请求中使用的默认连接设置。 从硬件平台的 ACPI 固件复制这些设置。

SerCx 处理，并完成 IOCTL_SERIAL_PURGE 请求。 在此类请求的处理，过程 SerCx 可以如有必要，驱动程序的 EvtSerCxPurge 回调函数寻求帮助清除接收或传输串行控制器驱动程序可能具有挂起的操作。 用作当前实现，SerCx 句柄所有支持清除操作而无需从 EvtSerCxPurge 函数的帮助。 但是，将来的实现的 SerCx 可能调用 EvtSerCxPurge 函数来执行清除操作的新类型。

SerCx 处理，并完成 IOCTL_SERIAL_GET_WAIT_MASK、 IOCTL_SERIAL_SET_WAIT_MASK 和 IOCTL_SERIAL_WAIT_ON_MASK 请求。 IOCTL_SERIAL_SET_WAIT_MASK 请求的处理，过程 SerCx 调用驱动程序的 EvtSerCxWaitmask 回调函数来通知等待掩码已更改的串行控制器驱动程序。 此函数将调用 SerCxGetWaitMask 方法以获取新的等待掩码。 更高版本，硬件事件发生时在此等待掩码中指定，串行控制器驱动程序调用 SerCxCompleteWait 方法以通知 SerCx，和 SerCx 完成任何挂起的 IOCTL_SERIAL_WAIT_ON_MASK 请求可能会等待该事件。 如果没有此类请求处于挂起状态，SerCx 将事件存储在预期将来的 IOCTL_SERIAL_WAIT_ON_MASK 请求到其内部事件历史记录中。

等待操作挂起时，SerCx 可以调用 EvtSerCxWaitmask 函数。 若要确定是否启动新的等待操作，该函数将调用 SerCxGetWaitMask。 如果 SerCxGetWaitMask 返回非零等待掩码，此等待掩码替换旧的等待掩码，和一个新的等待操作启动具有更新后的等待掩码。 如果 SerCxGetWaitMask 返回等待掩码为零，则在函数结束等待操作。 该函数在两种情况下调用 SerCxCompleteWait。
