---
title: USB 刷写支持的 UEFI 要求
description: Microsoft 提供用于在设计和制造环境中使用多个基于 USB 的闪烁的解决方案。 按顺序，使设备能够与这些工具一起使用，在设备上的 UEFI 环境必须满足本主题中列出的要求。
ms.assetid: 8979173C-DCBC-4544-9978-BB069FF35914
ms.date: 01/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 088b3b8c2ea0c30c1b3cf9bae9676bbb60614d7c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337372"
---
# <a name="uefi-requirements-for-usb-flashing-support"></a>USB 刷写支持的 UEFI 要求

Microsoft 提供用于在设计和制造环境中使用多个基于 USB 的闪烁的解决方案。 按顺序，使设备能够与这些工具一起使用，在设备上的 UEFI 环境必须满足本主题中列出的要求。

中列出的 UEFI 要求上展开这些要求与相关的闪烁[适用于所有 Windows 版本的 UEFI 要求](uefi-requirements-that-apply-to-all-windows-platforms.md)并[适用于 Windows 10 移动设备的 UEFI 要求](uefi-requirements-specific-to-windows-mobile.md)。

## <a name="required-uefi-protocols"></a>所需的 UEFI 协议

| 协议 | 要求详细信息 |
| --- | --- |
| USB 函数协议 | 对于 USB 闪烁通过 USB 3.0，必须实现固件，UEFI USB 函数協定修訂 0x00010002 或更高版本，其中包括支持[EFI\_USBFN\_IO\_协议。ConfigureEnableEndpointsEx](efi-usbfn-io-protocol-configureenableendpointsex.md)函数。 有关详细信息，请参阅[UEFI USB 函数协议](uefi-usb-function-protocol.md)。 |
| BlockIO | Microsoft 提供的 USB 闪烁解决方案选择第一个闪烁的非零大小的块 I/O 存储设备上返回的指针。 设备可以是固定或可移动存储。                                                                                                                                                             |
## <a name="uefi-desync-event-optional"></a>UEFI desync 事件 （可选）

尝试读取或写入磁盘闪烁的 UEFI 组件必须实现的支持，为 UEFI desync 事件 (EFI\_事件\_组\_固件\_DESYNC) 下表中所述。

| 要求 | 描述 |
| --- | --- |
| UEFI 启动服务的支持 | UEFI 固件必须支持事件，计时器，和任务优先级服务中定义部分 6.1 UEFI 2.3.1 规范。 |
| 事件组 GUID | Microsoft 定义了带下列 GUID EFI_EVENT_GROUP_FIRMWARE_DESYNC: {24FA5E72-1A82-49A2-970B-3230372662A5} |
| UEFI 固件事件 | 识别需要刷新或同步回定期存储其状态的所有 UEFI 固件组件。 在每个组件，创建与 EFI_EVENT_GROUP_FIRMWARE_DESYNC 和导致组件停止刷新/同步回存储 NotifyFunction() 关联的事件。 事件的 NotifyFunction() 应执行任何清理操作对转换为 desynchronized 模式所需的组件。 完成该清理后该组件不必须刷新或直到下一步设备重新启动同步其存储回与立刻正式投入工作。 如果事件的 NotifyFunction fails()，NotifyFunction() 不应返回 EFI_SUCCESS。 |

下面的代码示例演示了如何固件可以创建事件组的 GUID:

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

[最小的 Windows 在 SoC 平台上的 UEFI 要求](minimum-uefi-requirements-for-windows-on-soc-platforms.md)  

[适用于所有 Windows 版本的 UEFI 要求](uefi-requirements-that-apply-to-all-windows-platforms.md)  

[Windows 10 移动版的 UEFI 要求](uefi-requirements-specific-to-windows-mobile.md)  
