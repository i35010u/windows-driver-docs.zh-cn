---
title: USB 刷写支持的 UEFI 要求
description: Microsoft 提供了多个基于 USB 的闪烁解决方案，可用于工程环境和生产环境。 为了使设备与这些工具一起使用，设备上的 UEFI 环境必须满足本主题中列出的要求。
ms.date: 01/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: fee25c05c9549c2984617fb845ea947ec868cc27
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804097"
---
# <a name="uefi-requirements-for-usb-flashing-support"></a>USB 刷写支持的 UEFI 要求

Microsoft 提供了多个基于 USB 的闪烁解决方案，可用于工程环境和生产环境。 为了使设备与这些工具一起使用，设备上的 UEFI 环境必须满足本主题中列出的要求。

与闪烁相关的这些要求在适用于 windows 10 移动 [版的所有 windows 版本](uefi-requirements-that-apply-to-all-windows-platforms.md) 和 [Uefi 要求](uefi-requirements-specific-to-windows-mobile.md)的 uefi 要求中列出。

## <a name="required-uefi-protocols"></a>必需的 UEFI 协议

| Procotol | 要求详细信息 |
| --- | --- |
| USB 函数协议 | 对于 usb 3.0 上的 USB 闪烁，固件必须实现 UEFI USB function 协议修订版本0x00010002 或更高版本，包括对 [EFI \_ USBFN \_ IO \_PROTOCOL.ConfigureEnableEndpointsEx](efi-usbfn-io-protocol-configureenableendpointsex.md) 函数的支持。 有关详细信息，请参阅 [UEFI USB 函数协议](uefi-usb-function-protocol.md)。 |
| BlockIO | Microsoft 提供的 USB 闪烁解决方案选择第一个返回到非零大小块 i/o 存储设备的指针，以供闪烁。 设备可以是不可移动的或可移动的存储。                                                                                                                                                             |
## <a name="uefi-desync-event-optional"></a>UEFI desync 事件 (可选) 

在闪烁时，尝试在磁盘上读取或写入磁盘的 UEFI 组件必须 \_ \_ \_ \_ 按下表中所述的方式实现对 UEFI desync 事件 (EFI 事件组固件 desync) 的支持。

| 要求 | 说明 |
| --- | --- |
| UEFI 启动服务支持 | UEFI 固件必须支持 UEFI 2.3.1 规范的6.1 节中定义的事件、计时器和任务优先级服务。 |
| 事件组 GUID | Microsoft 定义具有以下 GUID 的 EFI_EVENT_GROUP_FIRMWARE_DESYNC： {24FA5E72-1A82-49A2-970B-3230372662A5} |
| UEFI 固件事件 | 确定需要定期刷新或将其状态同步回存储的所有 UEFI 固件组件。 在上述每个组件中，创建与 EFI_EVENT_GROUP_FIRMWARE_DESYNC 关联的事件，并使用 NotifyFunction ( # A1 来使组件停止刷新/同步到存储。 事件的 NotifyFunction ( # A1 应执行组件转换为 desynchronized 模式所需的任何清理操作。 完成此清理后，组件必须不刷新或将其存储重新同步，直到下一次设备重新启动。 如果事件的 NotifyFunction 失败 ( # A1，则 NotifyFunction ( # A3 不应返回 EFI_SUCCESS。 |

下面的代码示例演示了固件如何创建事件组 GUID 事件：

```cpp
gBS->CreateEventEx (
    EVT_NOTIFY_SIGNAL,
    TPL_CALLBACK,
    FIRMWARE_NOTIFICATION_FUNCTION,          // To be defined by SoC Vendor
    &FIRMWARE_NOTIFICATION_FUNCTION_CONTEXT, // To be defined by SoC Vendor
    &EFI_EVENT_GROUP_FIRMWARE_DESYNC,
    &Event                                   // Event returned by CreateEventEx
);
```

## <a name="related-topics"></a>相关主题

[SoC 平台上的 Windows 的最低 UEFI 要求](minimum-uefi-requirements-for-windows-on-soc-platforms.md)  

[适用于所有 Windows 版本的 UEFI 要求](uefi-requirements-that-apply-to-all-windows-platforms.md)  

[Windows 10 移动版的 UEFI 要求](uefi-requirements-specific-to-windows-mobile.md)  
