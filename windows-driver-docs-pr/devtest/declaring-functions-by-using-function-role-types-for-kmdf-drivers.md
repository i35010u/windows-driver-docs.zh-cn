---
title: 使用 KMDF 驱动程序的函数角色类型来声明函数
description: 使用 KMDF 驱动程序的函数角色类型来声明函数
ms.assetid: 73a408ba-0219-4fde-8dad-ca330e4e67c3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9024cd3b17c4b2aa5f43326268468183d248c0b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341167"
---
# <a name="declaring-functions-by-using-function-role-types-for-kmdf-drivers"></a>使用 KMDF 驱动程序的函数角色类型来声明函数


若要启用 SDV 分析 KMDF 驱动程序，您必须声明您使用 KMDF 函数角色类型声明的函数。 Wdf.h 和 Wdf.h 中包含其他 KMDF 标头文件中定义的函数角色类型。 有关函数的角色类型和其相应的事件回调函数的列表，请参阅[静态验证工具 KMDF 驱动程序函数声明](static-driver-verifier-kmdf-function-declarations.md)。

必须通过指定相应的角色类型声明 KMDF 驱动程序中的每个事件回调函数。

例如，下面的代码示例显示的函数角色类型声明[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数。 在此示例中，调用该回调函数*myDriver\_EvtDriverDeviceAdd*。 函数角色类型为 EVT\_WDF\_驱动程序\_设备\_添加。

```
EVT_WDF_DRIVER_DEVICE_ADD myDriver_EvtDriverDeviceAdd;
```

如果回调函数有函数原型声明，必须将函数原型替换函数角色类型声明。

以下列表是从标头文件失败\_Driver6.h。 相关的函数 FailDriver6.c 中声明。

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

使用角色类型声明的回调函数声明您的驱动程序之后，你可以[扫描该驱动程序](scanning-the-driver.md)。 扫描该驱动程序会生成 Sdv map.h 文件，可检查以确定是否已正确识别的入口点。

### <a name="span-idrunningcodeanalysisfordriverstoverifythefunctiondeclarationsspanspan-idrunningcodeanalysisfordriverstoverifythefunctiondeclarationsspan-running-code-analysis-for-drivers-to-verify-the-function-declarations"></a><span id="running_code_analysis_for_drivers_to_verify_the_function_declarations"></span><span id="RUNNING_CODE_ANALYSIS_FOR_DRIVERS_TO_VERIFY_THE_FUNCTION_DECLARATIONS"></span> 运行 Code Analysis for Drivers 验证函数声明

若要帮助您确定是否准备好的源代码，请运行[Code Analysis for Drivers](code-analysis-for-drivers.md)。 代码分析函数角色类型声明的驱动程序检查并且可以帮助标识可能错过的函数声明或函数定义的参数不匹配函数角色类型中时向您发出警告。

### <a name="span-idfunctionparametersandfunctionroletypesspanspan-idfunctionparametersandfunctionroletypesspanfunction-parameters-and-function-role-types"></a><span id="function_parameters_and_function_role_types"></span><span id="FUNCTION_PARAMETERS_AND_FUNCTION_ROLE_TYPES"></span>函数参数和函数的角色类型

根据需要在 C 编程语言中，在函数定义中使用的参数类型必须匹配的函数原型中，参数类型或函数角色在此示例中，键入。 SDV 取决于分析的函数签名，并忽略的函数的签名不匹配。

例如，应声明[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)例程使用 EVT\_WDF\_驱动程序\_设备\_添加函数角色类型。

```
EVT_WDF_DRIVER_DEVICE_ADD myEvtDriverDeviceAdd;
```

当实现函数*myEvtDriverDeviceAdd*，参数类型必须匹配所使用的 EVT\_WDF\_驱动程序\_设备\_添加，即 WDFDRIVER 和 PWDFDEVICE\_INIT (请参阅[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)例程的语法)。

```
NTSTATUS
 myEvtDriverDeviceAdd (
  WDFDRIVER Driver,
 PWDFDEVICE_INIT DeviceInit
 )
{
}
```

 

 





