---
title: MB 挂起检测
description: MB 挂起检测
ms.assetid: D3D222F7-96BE-48F7-8074-8820E43E3C7B
keywords:
- MB 挂起检测，移动宽带挂起检测，移动宽带的微型端口驱动程序挂起检测
ms.date: 08/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0a3d735b1c176b9f8d07e94c481bbbb427bd3dc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343395"
---
# <a name="mb-hang-detection"></a>MB 挂起检测

移动宽带 （MB 或 MBB） 挂起检测是 Windows 10，版本 1809年及更高版本中一项技术，可帮助 MBB 客户端驱动程序检测的控制路径和从这些恢复挂起状态。 是的一部分[基于设备的重置和恢复](mb-device-based-reset-and-recovery.md)旨在从各种 MBB 设备和驱动程序的错误情况中恢复的功能。 

本主题中的流关系图作为基础总线，使用 USB 尽管重置机制与总线无关，如果在 ACPI 和总线堆栈定义此页所述的接口。 

以下流程图以一般方式适用于所有 NDIS 对象标识符 (Oid) 和到微型端口驱动程序的回调。 可能情况下的恢复在此过程不如果 NDIS 不完全支持重置恢复无法工作。

![高级挂起检测和重置流](images/mb-self-healing-hang-detection-highlevel.png "高级挂起检测和重置流。")

此挂起检测和重置流序列包含三个阶段：

1. 挂起检测 
2. 若要获取状态，以便进行进一步调试任何潜在的日志记录
3. 重置-意外删除处理

## <a name="hang-detection"></a>挂起检测

服务层提供了对驱动程序以启动恢复时错误因为在用户层上，检测到的内容的提示`WWANSvc`有管理的移动电话网络适配器连接状态的状态机。 若要支持此功能，专用接口被定义驱动程序用于触发重置操作。 有少数情况下，驱动程序在哪里产生自己设备的命令，以确保状态机有效。 如果任何这些命令的超时时间，然后从驱动程序本身无需进行通信的操作返回到用户模式，才能启动恢复操作触发重置/恢复。 

有关 UDE 客户端驱动程序可用于触发重置操作的专用接口的详细信息，请参阅[基于 MB 设备的重置和恢复](mb-device-based-reset-and-recovery.md#reset-recovery-for-ude-devices)。

此示例使用[OID_WWAN_CONNECT](oid-wwan-connect.md)作为一个示例，用于该挂起检测工作流中的每个步骤。 

![重置流的 OID_WWAN_CONNECT](images/mb-self-healing-hang-detection-wwanconnect-flow.png "重置 OID_WWAN_CONNECT 的流。")

1. 接收 （通过协议驱动程序） 的 NDIS [OID_WWAN_CONNECT](oid-wwan-connect.md)。
2. NDIS 将 OID_WWAN_CONNECT 传递到类驱动程序。
3. 在类驱动程序构造的连接请求的 MBIM 消息。
4. 在类驱动程序将 MBIM 消息发送到通过 USB 总线 MBIM 函数。 
5. 固件命令将会超时，这可能是因为固件挂起或 MBIM 命令需要很长时间才能完成。
6. 在类驱动程序返回 NDIS 命令而无需使用 NDIS_NOTIFICATION_REQUIRED 固件完成。 从驱动程序通过 OID_WWAN_CONNECT 结果返回经请求的通知[NDIS_STATUS_WWAN_CONTEXT_STATE](ndis-status-wwan-context-state.md)与**状态**设置为**超时**，该值指示基础设备没有响应命令。 
7. NDIS 完成 OID 请求到协议驱动程序。
8. 协议驱动程序返回回服务，会看到该命令失败的调用。
9. 该服务会触发重置操作使用新的 OID 接口在设备上。 
10. 此点之后，FDO 调用总线意外删除和重新枚举 MBB 设备。 如果基础总线，USB FDO 将调用适当的函数以将设备重置。 
11. 如果在 UEFI 中定义了适当的 ACPI 方法，则将触发文件夹数或 PLDR。

有关文件夹数和 PLDR 的详细信息，请参阅[基于 MB 设备的重置和恢复](mb-device-based-reset-and-recovery.md#device-based-resets)。

## <a name="reset-surprise-removal"></a>重置 （意外删除）

后重置恢复可以继续，总线原因要生成意外删除 IRP，提供了支持的插即用 (PnP) 管理器已在 ACPI/UEFI 级别。 NDIS，在接收到意外删除 IRP，调用返回到`WMBCLASS`意外删除即插即用事件回调。 `WMBCLASS` 处理意外删除操作。 此时，必须完成所有命令，等等，必须返回到 NDIS 成功返回的数据包。 否则，在意外删除操作将完成。 流的余下部分等同于在总线上，例如 USB 真实的设备，意外的删除。 

1. NDIS 调用意外删除的即插即用事件。
2. `WMBCLASS` 忽略挂起 MBIM 命令的返回值，并返回原始的 NDIS 命令。 
3. `WMBCLASS` 返回在意外删除的 NDIS 即插即用回调。

## <a name="recovery"></a>恢复

意外删除，在堆栈包括的所有驱动程序后`WMBCLASS`必须释放所有资源，以便可以删除并重新枚举的总线的设备对象。 如果不这样做，设备将不会重新枚举并不会被恢复。

## <a name="related-links"></a>相关链接

[MB 基于设备的重置和恢复](mb-device-based-reset-and-recovery.md)
