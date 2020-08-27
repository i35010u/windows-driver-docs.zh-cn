---
description: 处理设备控制和文件创建
title: 处理设备控制和文件创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 387a931ae049f25d30249b4ee69e517fde3aa2c6
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968802"
---
# <a name="handling-device-control-and-file-creation"></a>处理设备控制和文件创建


每次基于 Windows 的应用程序调用 **DeviceIoControl** Win32 函数时，用户模式驱动程序框架 (UMDF) 通过调用 **IQueueCallbackDeviceIlControl** 接口中的方法之一通知驱动程序。 每次基于 Windows 的应用程序调用 **CreateFile** Win32 函数时，UMDF 会通过调用 **IQueueCallbackCreate** 接口中的方法来通知驱动程序。 此功能位于示例驱动程序的 *queue* 和 *queue* 模块中。

下表介绍了这些模块中的方法。

| 方法                                               | 说明                                                                                                   |
|------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| **IObjectCleanup::OnCleanup**                        | 释放对由 **OnCreateFile** 分配给 WDF file 对象的客户端上下文映射的引用。 |
| **IQueueCallbackCreate::OnCreateFile**               | 作为调用 Win32 **CreateFile** 函数的应用程序的结果打开设备。                  |
| **IQueueCallbackDeviceIoControl::OnDeviceIoControl** | 在调用 **DeviceIOControl** 函数的应用程序的结果中执行设备操作。        |

 

有关每个接口及其方法的说明，请参阅 [UMDF](https://go.microsoft.com/fwlink/p/?linkid=153678) 文档。

 

 




