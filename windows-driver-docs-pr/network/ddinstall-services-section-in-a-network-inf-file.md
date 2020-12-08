---
title: 网络 INF 文件中的 DDInstall.Services 节
description: 网络 INF 文件中的 DDInstall.Services 节
keywords:
- INF 文件 WDK 网络，DDInstall 部分
- 网络 INF 文件 WDK，DDInstall 部分
- DDInstall 的 "服务" 部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e0a951329dcad42b577ad1cfcf142db66307bd3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814975"
---
# <a name="ddinstallservices-section-in-a-network-inf-file"></a>网络 INF 文件中的 DDInstall.Services 节





*DDInstall*。网络 INF 文件中的 "**服务**" 部分基于 "通用 [**INF DDInstall" 部分**](../install/inf-ddinstall-services-section.md)。

*DDInstall*。**Services** 节包含一个或多个 **AddService** 指令，其中每个指令都引用一个由 INF 编写器定义的 *服务安装部分*，该部分指定如何以及何时加载特定组件驱动程序的服务。

*DDInstall*。在 (适配器) 安装网络组件的 INF 文件中需要 "**服务**" 部分。它在安装 **NetTrans**、 **NetClient** 或 **空间** 组件的 INF 文件中是可选的。

**请注意**，**NetClient** 组件在 Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用。  

 

*DDInstall* 中的 **AddService** 指令。**服务** 部分还可以引用安装组件错误日志的 *错误日志安装*。 对于所有网络组件，错误日志都是可选的。

有关详细信息，请参阅 [**INF AddService 指令**](../install/inf-addservice-directive.md)。

下面是 *DDInstall* 的一个示例。*错误日志-安装-部分* 中的 **AddReg** 指令引用的 **服务** 部分、*服务安装部分*、*错误日志-安装部分* 和 *外接* 程序的部分：

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

**AddService** 指令的 *ServiceName* 参数（在上面的示例中为 **A1** ） (第一个 **AddService** 参数) ，必须与组件的 **Ndi \\ 服务** 值匹配。 有关详细信息，请参阅 [将 Service-Related 值添加到 Ndi 项](adding-service-related-values-to-the-ndi-key.md)。

 

