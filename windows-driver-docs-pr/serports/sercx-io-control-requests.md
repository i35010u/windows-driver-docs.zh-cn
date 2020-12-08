---
title: SerCx I/O 控制请求
description: SerCx 支持的串行 i/o 控制请求的列表。
keywords:
- SerCx IOCTLs
ms.date: 11/30/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee603e33242c6f740de605d9253568da439f0b38
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811969"
---
# <a name="sercx-io-control-requests"></a>SerCx I/O 控制请求

除了一些例外情况， (SerCx) 的串行 framework 扩展的版本1支持使用 Ntddser 头文件中定义的 IOCTL_SERIAL_XXX i/o 控制代码 (IOCTLs) 的 i/o 控制请求。 SerCx 处理其中一些请求，但 SerCx 必须依赖串行控制器驱动程序来处理需要特定于硬件的处理的多个其他请求。 SerCx 处理的某些请求还需要特定于硬件的处理。 尽管 SerCx 负责完成这些请求，但 SerCx 会将对这些请求的大量处理工作发送到串行控制器驱动程序。

系统提供的 Serial.sys 驱动程序也支持其中的大多数 IOCTLs，该驱动程序管理 Pc 上的命名串行端口。 所有受支持的 Windows 版本都提供 Serial.sys。 有关串行 IOCTLs 的详细说明，请参阅 [串行设备控制请求](serial-device-control-requests2.md)。

SerCx 不支持 Ntddser 头文件中定义的所有 IOCTLs。 SerCx 不支持客户端外设驱动程序不应使用的过时 IOCTL_SERIAL_CONFIG_SIZE IOCTL。 此外，不支持的是 IOCTL_SERIAL_RESET_DEVICE IOCTL，SerCx 始终以 STATUS_NOT_IMPLEMENTED 错误状态代码完成。 此外，SerCx 不支持 Ntddser 中定义的任何 IOCTL_SERIAL_INTERNAL_XXX IOCTLs。

SerCx 支持的许多 IOCTLs 用于配置串行端口上的硬件设置。 打开串行端口之后，客户端应假设串行端口处于未知或未定义状态，而不是处于已知默认状态。 客户端负责配置串行端口，使其可供使用。

SerCx 支持的大多数 IOCTLs 由串行控制器驱动程序实现的 EvtSerCxControl 回调函数进行处理。 SerCx 处理8个串行 IOCTLs，而不调用 EvtSerCxControl 函数。 但是，若要处理其中一些 IOCTLs，SerCx 需要在除 EvtSerCxControl 之外的串行控制器驱动程序中获得回调函数的帮助。 有关详细信息，请参阅 IOCTLs 由 SerCx 处理。

## <a name="ioctls-handled-by-the-evtsercxcontrol-function"></a>IOCTLs 由 EvtSerCxControl 函数处理

如果 SerCx 收到包含 SerCx 不支持的 IOCTL 的 i/o 控制请求，则 SerCx 将调用串行控制器驱动程序的 EvtSerCxControl 回调函数来处理该请求。 在响应中，此函数必须完成该请求。 但是，此函数可能不会处理它收到的所有 i/o 控制请求。 如果 EvtSerCxControl 函数收到它无法识别或支持的 IOCTL，则应使用 STATUS_NOT_IMPLEMENTED 错误状态代码来完成请求。
EvtSerCxControl 函数处理的某些 i/o 控制请求可能会以某种方式更改串行控制器的配置或行为。 若要避免错误，外围设备驱动程序应避免发送 i/o 控制请求来重新配置控制器，而控制器仍在处理挂起的传输或接收操作。 此外，在串行控制器驱动程序完成任何可能更改控制器配置的挂起 i/o 控制请求之前，此外围设备驱动程序应避免启动新的传输或接收操作。

通常，SerCx 发送到 EvtSerCxControl 函数的许多请求在返回之前可通过此函数完成。 如果请求需要延迟处理，则该函数可以计划一个 DPC 例程或工作线程来完成请求。 出于性能原因，此函数应避免不必要地为不需要延迟处理的操作安排 DPC 例程或工作线程。

SerCx 不会尝试序列化对 EvtSerCxControl 函数的调用。 这些调用可能会同时从不同的线程发生，并且可能同时运行两个或多个 EvtSerCxControl 函数的调用。

## <a name="ioctls-handled-by-sercx"></a>IOCTLs 由 SerCx 处理

SerCx 处理并完成 IOCTL_SERIAL_GET_TIMEOUTS 和 IOCTL_SERIAL_SET_TIMEOUTS 请求，无需串行控制器驱动程序的帮助，但 SerCx 会将当前的超时参数应用到驱动程序执行的传输和接收操作。 串行控制器驱动程序可以通过调用 SerCxGetReadIntervalTimeout 方法来获取当前的读取间隔超时值。 有关超时的详细信息，请参阅 SERIAL_TIMEOUTS。

SerCx 处理并完成 IOCTL_SERIAL_APPLY_DEFAULT_CONFIGURATION 的请求。 在处理此请求的过程中，SerCx 将调用驱动程序的 EvtSerCxApplyConfig 回调函数以将串行控制器配置为使用请求中的默认连接设置。 将从硬件平台的 ACPI 固件复制这些设置。

SerCx 处理并完成 IOCTL_SERIAL_PURGE 的请求。 在此类请求的处理过程中，SerCx 可能会在必要时调用驱动程序的 EvtSerCxPurge 回调函数，以便在清除串行控制器驱动程序可能已挂起的接收或传输操作时获得帮助。 当前实现时，SerCx 会处理所有支持的清除操作，而无需 EvtSerCxPurge 函数的帮助。 但是，SerCx 的未来实现可能会调用 EvtSerCxPurge 函数来执行新类型的清除操作。

SerCx 处理并完成 IOCTL_SERIAL_GET_WAIT_MASK、IOCTL_SERIAL_SET_WAIT_MASK 和 IOCTL_SERIAL_WAIT_ON_MASK 请求。 在处理 IOCTL_SERIAL_SET_WAIT_MASK 请求的过程中，SerCx 将调用驱动程序的 EvtSerCxWaitmask 回调函数，通知串行控制器驱动程序等待掩码已更改。 此函数调用 SerCxGetWaitMask 方法来获取新的等待掩码。 稍后，当在此等待掩码中指定的硬件事件发生时，串行控制器驱动程序将调用 SerCxCompleteWait 方法以通知 SerCx，而 SerCx 将完成可能正在等待事件的任何挂起的 IOCTL_SERIAL_WAIT_ON_MASK 请求。 如果没有此类请求处于挂起状态，则 SerCx 会在其内部事件历史记录中存储事件，以预测未来 IOCTL_SERIAL_WAIT_ON_MASK 请求。

等待操作挂起时，SerCx 可以调用 EvtSerCxWaitmask 函数。 若要确定是否要启动新的等待操作，该函数将调用 SerCxGetWaitMask。 如果 SerCxGetWaitMask 返回非零等待掩码，此等待掩码将替换旧的等待掩码，并以更新的等待掩码开始新的等待操作。 如果 SerCxGetWaitMask 返回的等待掩码为零，则该函数将结束等待操作。 在这两种情况下，函数都调用 SerCxCompleteWait。
