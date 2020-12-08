---
title: 安装 WIA 错误处理驱动程序扩展
description: 安装 WIA 错误处理驱动程序扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3140d2564d1000210450d2749f8fb5301425c57c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793643"
---
# <a name="installing-a-wia-error-handling-driver-extension"></a>安装 WIA 错误处理驱动程序扩展


错误处理扩展插件应该与 WIA 驱动程序一起安装。 若要将驱动程序的错误处理程序与驱动程序一起安装，必须为驱动程序的 INF 文件添加少量的添加操作。

下面的示例演示如何修改现有的驱动程序 INF 文件，使其包含错误处理程序。

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

{UiClassId} 类 ID 是驱动程序为 WIA \_ DIP UI CLSID 属性返回的值 \_ \_ ，而 {ErrorHandlerCLSID} 是错误处理程序的类 id。 在此示例中， *myerrhandler.dll* 包含错误处理程序的实现。

**AddReg** 节中的第一项是将错误处理程序注册为驱动程序的 WIA 扩展。 以下三个项将错误处理程序注册为 COM 组件。

错误处理扩展插件的 *ThreadingModel* 值必须同时为 **两者**。

 

 




