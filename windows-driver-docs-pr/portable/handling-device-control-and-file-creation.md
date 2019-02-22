---
Description: Handling Device Control and File Creation
title: 处理设备控制和文件创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa6dc7786e023435495483e88e004742c9c27144
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555473"
---
# <a name="handling-device-control-and-file-creation"></a>处理设备控制和文件创建


每次基于 Windows 的应用程序调用**DeviceIoControl** Win32 函数，用户模式驱动程序框架 (UMDF) 通知驱动程序通过调用中的方法之一**IQueueCallbackDeviceIlControl**接口。 每次基于 Windows 的应用程序调用**CreateFile** Win32 函数 UMDF 驱动程序会通过通知调用方法**IQueueCallbackCreate**接口。 此功能的示例驱动程序中找到*Queue.cpp*并*Queue.h*模块。

下表介绍这些模块中找到的方法。

| 方法                                               | 描述                                                                                                   |
|------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| **IObjectCleanup::OnCleanup**                        | 释放由分配的客户端上下文映射到引用**OnCreateFile** WDF 文件对象。 |
| **IQueueCallbackCreate::OnCreateFile**               | 打开调用 Win32 的应用程序由于设备**CreateFile**函数。                  |
| **IQueueCallbackDeviceIoControl::OnDeviceIoControl** | 执行调用的应用程序由于设备操作**DeviceIOControl**函数。        |

 

请参阅[UMDF](https://go.microsoft.com/fwlink/p/?linkid=153678)文档，以说明的每个接口和其方法。

 

 




