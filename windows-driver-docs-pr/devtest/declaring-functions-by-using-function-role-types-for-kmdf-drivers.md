---
title: 使用 KMDF 驱动程序的函数角色类型来声明函数
description: 使用 KMDF 驱动程序的函数角色类型来声明函数
ms.assetid: 73a408ba-0219-4fde-8dad-ca330e4e67c3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3d91b8b9b079b11090601fdc92024a23a35720b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840284"
---
# <a name="declaring-functions-by-using-function-role-types-for-kmdf-drivers"></a>使用 KMDF 驱动程序的函数角色类型来声明函数


若要使 SDV 能够分析 KMDF 驱动程序，必须使用 KMDF 的函数角色类型声明来声明函数。 函数角色类型在 Wdf 和 KMDF 中包含的其他头文件中定义。 有关函数角色类型及其对应的事件回调函数的列表，请参阅[Static Driver VERIFIER KMDF Function 声明](static-driver-verifier-kmdf-function-declarations.md)。

KMDF 驱动程序中的每个事件回调函数必须通过指定相应的角色类型进行声明。

例如，下面的代码示例演示了[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数的函数角色类型声明。 在此示例中，回调函数称为*myDriver\_EvtDriverDeviceAdd*。 函数 role 类型为 .EVT\_WDF\_DRIVER\_设备\_"添加"。

```
EVT_WDF_DRIVER_DEVICE_ADD myDriver_EvtDriverDeviceAdd;
```

如果回调函数具有函数原型声明，则必须将函数原型替换为函数角色类型声明。

下面列出的是标头文件中的 Driver6 失败\_。 相关函数在 FailDriver6 中声明。

```
/*++

Copyright (C) Microsoft.  All rights reserved.
Module Name:
    fail_driver6.h
Environment:
    Kernel mode
--*/

#include <NTDDK.h>  
#include <wdf.h>

#include "fail_library6.h"

DRIVER_INITIALIZE DriverEntry;
EVT_WDF_DRIVER_DEVICE_ADD EvtDriverDeviceAdd;
EVT_WDF_IO_QUEUE_IO_READ EvtIoRead;
EVT_WDF_IO_QUEUE_IO_WRITE EvtIoWrite;
EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL EvtIoDeviceControl;
EVT_WDF_DEVICE_CONTEXT_CLEANUP DeviceContextCleanUp;
EVT_WDF_DEVICE_CONTEXT_DESTROY DeviceContextDestroy;
EVT_WDF_IO_QUEUE_CONTEXT_CLEANUP_CALLBACK QueueCleanup;
EVT_WDF_IO_QUEUE_CONTEXT_DESTROY_CALLBACK QueueDestroy;
EVT_WDF_FILE_CONTEXT_CLEANUP_CALLBACK FileContextCleanup;
EVT_WDF_FILE_CONTEXT_DESTROY_CALLBACK FileContextDestroy;
```

使用角色类型声明声明驱动程序回调函数后，可以[扫描该驱动程序](scanning-the-driver.md)。 扫描驱动程序会生成 Sdv 文件，您可以检查该文件以确定是否正确确定了入口点。

### <a name="span-idrunning_code_analysis_for_drivers_to_verify_the_function_declarationsspanspan-idrunning_code_analysis_for_drivers_to_verify_the_function_declarationsspan-running-code-analysis-for-drivers-to-verify-the-function-declarations"></a><span id="running_code_analysis_for_drivers_to_verify_the_function_declarations"></span><span id="RUNNING_CODE_ANALYSIS_FOR_DRIVERS_TO_VERIFY_THE_FUNCTION_DECLARATIONS"></span>为驱动程序运行代码分析来验证函数声明

为帮助您确定是否已准备好源代码，请[对驱动程序运行代码分析](code-analysis-for-drivers.md)。 用于驱动程序的代码分析检查函数角色类型声明，并有助于识别可能已丢失的函数声明，或函数定义的参数与函数角色类型中的参数不匹配时发出警告。

### <a name="span-idfunction_parameters_and_function_role_typesspanspan-idfunction_parameters_and_function_role_typesspanfunction-parameters-and-function-role-types"></a><span id="function_parameters_and_function_role_types"></span><span id="FUNCTION_PARAMETERS_AND_FUNCTION_ROLE_TYPES"></span>函数参数和函数角色类型

根据 C 编程语言的要求，在函数定义中使用的参数类型必须与函数原型的参数类型匹配，在本例中为函数角色类型。 SDV 依赖于用于分析的函数签名，并忽略其签名不匹配的函数。

例如，你应该使用 .EVT\_WDF\_DRIVER\_设备\_"添加函数" 角色类型声明一个[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)例程。

```
EVT_WDF_DRIVER_DEVICE_ADD myEvtDriverDeviceAdd;
```

实现函数*myEvtDriverDeviceAdd*时，参数类型必须与由 .EVT\_WDF\_DRIVER\_设备\_ADD，即，WDFDRIVER and PWDFDEVICE\_INIT 一起使用的参数类型相同（请参阅[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)例程的语法）。

```
NTSTATUS
 myEvtDriverDeviceAdd (
  WDFDRIVER Driver,
 PWDFDEVICE_INIT DeviceInit
 )
{
}
```

 

 





