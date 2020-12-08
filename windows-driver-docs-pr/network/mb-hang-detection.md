---
title: MB 挂起检测
description: MB 挂起检测
keywords:
- MB 挂起检测，移动宽带挂起检测，移动宽带微型端口驱动程序挂起检测
ms.date: 08/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9f6eaa12d8c59ce569be06547b94235bde879fde
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795447"
---
# <a name="mb-hang-detection"></a>MB 挂起检测

移动宽带 (MB 或 MBB) 挂起检测是 Windows 10 版本1809及更高版本中的一项技术，可帮助 MBB 客户端驱动程序检测控制路径中的挂起情况并从中恢复。 它是 [基于设备的重置和恢复](mb-device-based-reset-and-recovery.md) 功能的一部分，旨在从 MBB 设备和驱动程序的各种可能的错误情况中恢复。 

本主题中的流程图使用 USB 作为基础总线，但如果 ACPI 和总线堆栈定义此页上描述的接口，则重置机制是不可知的。 

以下流程图一般适用于所有 NDIS 对象标识符 (Oid) 和回微端口驱动程序的回叫。 在某些情况下，如果 NDIS 不完全支持重置恢复，此过程的恢复部分将不起作用。

![高级别挂起检测和重置流](images/mb-self-healing-hang-detection-highlevel.png "高级别挂起检测和重置流。")

此挂起检测和重置流序列包含三个阶段：

1. 挂起检测 
2. 获取用于进一步调试的状态的任何潜在日志记录
3. 重置–意外删除处理

## <a name="hang-detection"></a>挂起检测

服务层为驱动程序提供提示，以便在用户层上检测到错误时启动恢复，因为 `WWANSvc` 有一个状态机管理蜂窝适配器的连接状态。 为了支持这一点，定义了一个专用接口，驱动程序使用该接口来触发重置操作。 在某些情况下，驱动程序会在设备上发出自己的命令，以确保状态机有效。 如果这些命令中的任何一个出现超时，则将从驱动程序本身触发重置/恢复，而无需将操作重新与用户模式通信以启动恢复操作。 

有关 UDE 客户端驱动程序可用于触发重置操作的专用接口的详细信息，请参阅 [MB 基于设备的重置和恢复](mb-device-based-reset-and-recovery.md#reset-recovery-for-ude-devices)。

此示例使用 [OID_WWAN_CONNECT](oid-wwan-connect.md) 作为遍历挂起检测流的示例。 

![OID_WWAN_CONNECT 的重置流](images/mb-self-healing-hang-detection-wwanconnect-flow.png "OID_WWAN_CONNECT 的重置流。")

1. 通过协议驱动程序) 的 NDIS (收到 [OID_WWAN_CONNECT](oid-wwan-connect.md)。
2. NDIS 将 OID_WWAN_CONNECT 向下传递到类驱动程序。
3. 类驱动程序为连接请求构造 MBIM 消息。
4. 类驱动程序通过 USB 总线将 MBIM 消息发送到 MBIM 函数。 
5. 固件命令超时，原因可能是固件挂起或 MBIM 命令需要很长时间才能完成。
6. 类驱动程序将返回不带 NDIS_NOTIFICATION_REQUIRED 的固件完成的 NDIS 命令。 OID_WWAN_CONNECT 的结果将 [NDIS_STATUS_WWAN_CONTEXT_STATE](ndis-status-wwan-context-state.md) 通过从驱动程序中的请求通知返回，并将 **状态** 设置为 **Timeout**，指示基础设备未响应命令。 
7. NDIS 完成对协议驱动程序的 OID 请求。
8. 协议驱动程序将回调返回给服务，这将会看到该命令失败。
9. 服务使用新 OID 接口触发设备上的重置操作。 
10. 在此之后，FDO 会调用总线来意外删除并重新枚举 MBB 设备。 如果基础总线为 USB，则 FDO 将调用相应的函数来重置设备。 
11. 如果在 UEFI 中定义了适当的 ACPI 方法，则会触发 FLDR 或 PLDR。

有关 FLDR 和 PLDR 的详细信息，请参阅 [MB 基于设备的重置和恢复](mb-device-based-reset-and-recovery.md#device-based-resets)。

## <a name="reset-surprise-removal"></a>重置 (惊喜消除) 

重置恢复之后，总线会使即插即用 (PnP) 管理器生成意外删除 IRP，前提是该支持存在于 ACPI/UEFI 级别。 NDIS，接收到意外删除 IRP 后，会回拨入， `WMBCLASS` 以获取意外删除的 PnP 事件回调。 `WMBCLASS` 处理意外删除操作。 此时，必须完成所有命令等，并且必须将数据包成功返回回 NDIS。 否则，意外删除操作将无法完成。 流的其余部分与在总线上真正删除设备（例如 USB）相同。 

1. NDIS 调用 PnP 事件以进行意外删除。
2. `WMBCLASS` 忽略挂起的 MBIM 命令的返回并返回原始 NDIS 命令。 
3. `WMBCLASS` 返回用于意外删除的 NDIS PnP 回调。

## <a name="recovery"></a>恢复

在意外删除后，堆栈中的所有驱动程序都 `WMBCLASS` 必须释放所有资源，以便总线可以删除和重新枚举设备对象。 如果不这样做，将不会重新枚举设备，也不会恢复。

## <a name="related-links"></a>相关链接

[MB 基于设备的重置和恢复](mb-device-based-reset-and-recovery.md)
