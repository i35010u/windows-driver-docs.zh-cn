---
title: Sdv-map.h 文件的格式
description: Sdv-map.h 文件的格式
keywords:
- Sdv-map WDK 静态驱动程序验证程序，格式
- 格式化 WDK 静态驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17ec47bb0aad8118f3a37ab6dc736e0feabd670b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791951"
---
# <a name="format-of-the-sdv-maph-file"></a>Sdv-map.h 文件的格式


Sdv 文件列出了驱动程序中已声明的所有函数角色类型及其关联的回调函数和驱动程序入口点。

下面显示了 KMDF 示例驱动程序的已批准 Sdv-map 文件， \_ Driver3 失败。

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

当 SDV 找到入口点时，它将创建以下格式的 **\# define** 指令：

```
#define fun_Function_RoleType EntryPoint
```

 

 





