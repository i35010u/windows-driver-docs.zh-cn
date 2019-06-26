---
title: 网络 INF 文件中的 DDInstall.Services 节
description: 网络 INF 文件中的 DDInstall.Services 节
ms.assetid: 5d5cc0ac-fbe2-4791-9c74-fdf9906faff6
keywords:
- INF 文件 WDK 网络，DDInstall.Services 部分
- 可使用网络 INF 文件 WDK，DDInstall.Services 部分
- DDInstall.Services 部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fcd4f1039b3698db0430704d21dcd90017f4c20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354616"
---
# <a name="ddinstallservices-section-in-a-network-inf-file"></a>网络 INF 文件中的 DDInstall.Services 节





一个*DDInstall*。**服务**网络 INF 文件中的部分基于泛型[ **INF DDInstall.Services 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-services-section)。

一个*DDInstall*。**服务**部分包含一个或多个**AddService**指令，其中每个引用 INF 编写器的定义*服务安装部分*，它指定如何以及何时服务的特定组件驱动程序已被加载。

一个*DDInstall*。**服务**部分所需的网络组件 （适配器） 安装的 INF 文件中; 在安装的 INF 文件中是可选**NetTrans**， **NetClient**，或**NetService**组件。

**请注意**  **NetClient**组件在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。

 

**AddService**指令*DDInstall*。**服务**部分中还可以引用*错误日志-安装部分*用于安装组件的错误日志。 错误日志是可选的所有网络组件。

有关详细信息，请参阅[ **INF AddService 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)。

以下是一种*DDInstall*。**服务**部分中，*服务安装部分*，则*错误日志-安装部分*，和一个*添加注册表部分*引用**AddReg**指令*错误日志-安装部分*:

```cpp
[a1.ndi.NT.Services]
AddService = a1, 2, a1.AddService, a1.AddEventLog
 
[a1.AddService]
DisplayName = %Adapter1.DispName%
ServiceType = 1 ;SERVICE_KERNEL_DRIVER
StartType = 2 ;SERVICE_AUTO_START
ErrorControl = 1 ;SERVICE_ERROR_NORMAL
ServiceBinary = %12%\a1.sys
LoadOrderGroup = NDIS
 
[a1.AddEventLog]
AddReg = a1.AddEventLog.reg
 
[a1.AddEventLog.reg]
HKR,,EventMessageFile,0x00020000,"%%SystemRoot%%\System32\netevent.dll"
HKR,,TypesSupported,0x00010001,7
```

*ServiceName*的参数**AddService**指令，它在上面的示例中为**a1**(第一个**AddService**参数)，必须匹配的组件**Ndi\\服务**值。 有关详细信息，请参阅[Adding Service-Related 值到 Ndi 密钥](adding-service-related-values-to-the-ndi-key.md)。

 

 





