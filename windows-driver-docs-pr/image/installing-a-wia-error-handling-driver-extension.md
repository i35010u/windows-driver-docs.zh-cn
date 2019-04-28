---
title: 安装 WIA 错误处理驱动程序扩展
description: 安装 WIA 错误处理驱动程序扩展
ms.assetid: 8a16b0db-25ed-4512-8b45-0256fed6b83e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42239d5ce8c1a6b002e0218e0ad0d14c9592f721
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326075"
---
# <a name="installing-a-wia-error-handling-driver-extension"></a>安装 WIA 错误处理驱动程序扩展


应与 WIA 驱动程序一起安装的错误处理扩展插件。 若要安装该驱动程序以及驱动程序的错误处理程序，必须对驱动程序的 INF 文件完成少量的新增功能。

下面的示例演示如何修改现有的驱动程序 INF 文件以包括错误处理程序。

```INF
MyDriver.AddReg]
...
HKCR,CLSID\{UiClassId}\shellex\ErrorHandler\{ErrorHandlerCLSID}
...
HKCR,CLSID\{ErrorHandlerCLSID },,,"My Error Handler"
HKCR,CLSID\{ErrorHandlerCLSID }\InProcServer32,,,%11%\myerrhandler.dll
HKCR,CLSID\{ErrorHandlerCLSID }\InProcServer32,ThreadingModel,,"Both"
...

[MyDriver.CopyFiles]
...
myerrhandler.dll
...

[SourceDisksFiles.x86]
...
myerrhandler.dll=1
...
```

{UiClassId} 类 ID 为的值，以驱动程序返回的 WIA\_DIP\_UI\_CLSID 属性和 {ErrorHandlerCLSID} 是错误处理程序的类 ID。 在此示例中， *myerrhandler.dll*包含错误处理程序的实现。

中的第一个条目**AddReg**部分是为 WIA 扩展的驱动程序注册错误处理程序。 以下三项注册为 COM 组件的错误处理程序。

*ThreadingModel*值的错误处理扩展插件必须**同时**。

 

 




