---
title: WdfFiTester 概述
description: WdfFiTester 概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14bc1da7a42b14708d717563324d8c734243f197
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823314"
---
# <a name="wdffitester-overview"></a>WdfFiTester 概述


你可以将 WdfFiTester 配置为使返回 NTSTATUS 代码的任何 KMDF 设备驱动程序接口 (DDI) 函数调用。 KMDF 版本1.11 中提供了190个系统提供的函数，用于返回 NTSTATUS 代码。 有关这些函数的列表，请参阅 [KMDF 函数，返回 NSTATUS 代码](wdftester-functions-that-return-nstatus-codes.md)。

处理 KMDF 函数调用的代码通常具有下面的代码示例中所示的模式：

```
//
// Create the device object.
//
status = WdfDeviceCreate(
                         &DeviceInit,
                         &attributes,
                         &device
                         );
if (!NT_SUCCESS(status)) {
 return status;
    }
```

KMDF 函数返回一个 NTSTATUS 代码，驱动程序在继续之前会检查返回代码。 但是，由于缺少返回代码或检查是否有错误，因此会出现许多驱动程序问题。 这些错误可能导致驱动程序中出现意外的行为，或可能导致 bug 检查。

例如，如果某个函数具有在函数退出时应有效的 (**\_ \_ out**) 指针参数，但却为 **NULL**，则可能会发生 bug 检查。 如果驱动程序使用参数，并且驱动程序未正确检查函数调用的返回状态，则可能会发生 bug 检查。

对于已针对错误注入配置的每个 DDI，WdfFiTester 工具将返回状态为 "不成功" 的 NTSTATUS 代码 \_ 。 驱动程序应该会处理失败。

由于该工具使用 WMI 接口，因此你可以从脚本 (vbscript 或 jscript) 或 (C、c + + 或 c # ) 中可调用 WMI 的任何其他用户模式应用程序运行该工具。

除了其他操作，使用该工具的 WMI 接口，还可以获取由特定 KMDF 驱动程序调用的 DDIs 的列表，并等待在每次成功完成 DDI 错误时引发的 WMI 事件。

 

 





