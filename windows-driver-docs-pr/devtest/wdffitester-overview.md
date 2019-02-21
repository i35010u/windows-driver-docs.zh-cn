---
title: WdfFiTester 概述
description: WdfFiTester 概述
ms.assetid: 87acefcd-8db3-4b1e-972a-13fba629d52d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77e944cccb0c5abbcf3f88f3fffb2e33f3e8e1a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533672"
---
# <a name="wdffitester-overview"></a>WdfFiTester 概述


你可以配置 WdfFiTester 失败返回 NTSTATUS 代码任何 KMDF 设备驱动程序接口 (DDI) 函数调用。 有 190 系统提供 KMDF 1.11 版中的函数返回 NTSTATUS 代码。 有关这些函数的列表，请参阅[KMDF 函数的返回 NSTATUS 代码](wdftester-functions-that-return-nstatus-codes.md)。

通常处理 KMDF 函数调用的代码已在下面的代码示例所示的模式：

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

KMDF 函数返回的返回代码然后再继续检查 NTSTATUS 代码和驱动程序。 但是，由于缺少或不正确的返回代码检查会出现许多驱动程序问题。 这些错误可能会导致意外的行为驱动程序中，或可能导致的 bug 检查。

例如，可能出现的 bug 检查，如果函数具有 (**\_\_out**) 应在函数退出时有效的指针参数但，而是**NULL**。 如果驱动程序使用的参数和驱动程序不会检查函数调用返回的状态正确，可能出现的 bug 检查。

对于每个已配置为故障注入的 DDI，WdfFiTester 工具返回状态的 NTSTATUS 代码\_未成功。 该驱动程序应处理失败。

由于该工具使用 WMI 接口，你可以从脚本 （vbscript 或 jscript） 或任何其他用户模式应用程序运行它 (C、 c + +，或C#)，可以调用 WMI。

除了其他操作，与该工具的 WMI 接口即可的 DDIs 的函数调用的特定 KMDF 驱动程序，并正在等待 WMI 事件激发每次 DDI 故障注入成功完成的列表。

 

 





