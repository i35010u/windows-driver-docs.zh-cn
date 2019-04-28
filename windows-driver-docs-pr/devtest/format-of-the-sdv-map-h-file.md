---
title: Sdv-map.h 文件的格式
description: Sdv-map.h 文件的格式
ms.assetid: 1b9e2b8d-04b8-4288-9d63-e7d84d75a9c6
keywords:
- Sdv map.h WDK Static Driver Verifier 格式
- 格式 WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f3bc99f130f1cddf240003f6b26234ba732fa39
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329684"
---
# <a name="format-of-the-sdv-maph-file"></a>Sdv-map.h 文件的格式


Sdv map.h 文件列出了所有驱动程序及其相关联的回调函数和驱动程序入口点中声明了函数角色类型。

下面显示了对于 KMDF 示例驱动程序，已批准的 Sdv map.h 文件失败\_Driver3。

```
//Approved=true
#define fun_WDF_DRIVER_DEVICE_ADD EvtDriverDeviceAdd
#define fun_WDF_IO_QUEUE_IO_READ EvtIoRead
#define fun_WDF_IO_QUEUE_IO_STOP EvtIoStop
#define fun_WDF_TIMER_1 EvtTimerFunc
#define fun_WDF_DRIVER_UNLOAD EvtDriverUnload
#define fun_WDF_REQUEST_CANCEL_1 EvtRequestCancel
#define fun_DriverEntry DriverEntry
#define fun_WDF_DEVICE_D0_ENTRY DeviceD0Entry
#define fun_WDF_IO_QUEUE_IO_WRITE EvtIoWrite
#define fun_WDF_IO_QUEUE_IO_DEVICE_CONTROL EvtIoDeviceControl
```

当 SDV 找到入口点时，它会创建**\#定义**指令采用以下格式：

```
#define fun_Function_RoleType EntryPoint
```

 

 





