---
title: 包含 NetworkProvider 节
description: 包含 NetworkProvider 节
keywords:
- INF 文件 WDK network，NetworkProvider 部分
- 网络 INF 文件 WDK，NetworkProvider 部分
- NetworkProvider 部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf6b314dfdd847c4f1879cc48ddd614f21b72e0f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840647"
---
# <a name="including-a-networkprovider-section"></a>包含 NetworkProvider 节





**NetworkProvider** 节指定 **NetClient** 组件的替代设备名称或用于 NetWare **net view** 命令的短名称。

**请注意**，**NetClient** 组件在 Windows 8.1、Windows Server 2012 R2 和更高版本中已弃用。  

 

若要创建 **NetworkProvider** 节，请将 **NetworkProvider** 扩展添加到组件的 *DDInstall* 节，如以下示例中所示：
```INF
[DDInstall] ; Install section
[DDInstall.NetworkProvider] ; NetworkProvider section
```

### <a name="specifying-a-device-name"></a>指定设备名称

网络类安装程序通常会通过将组件的 **Ndi \\ 服务** 值复制到组件 **服务** 项下的 NetworkProvider 项来为网络提供程序创建设备名称。 有关详细信息，请参阅 [将 Service-Related 值添加到 Ndi 项](adding-service-related-values-to-the-ndi-key.md)。 若要为组件指定其他设备名称，请在组件的 **NetworkProvider** 部分中包含 **DeviceName** 条目，如以下示例中所示：

```INF
[DDInstall-section.NetworkProvider]
DeviceName = "nwrdr"
```

**DeviceName** 是可选的，仅当组件的 **Ndi \\ 服务** 值不足以作为网络提供程序的设备名称时，才应指定此选项。

### <a name="specifying-a-short-name"></a>指定短名称

若要为网络提供程序指定用于 NetWare **net view** 命令的短名称，请在组件的 **NetworkProvider** 部分中包含 **短名称** 项，如以下示例中所示：

```INF
[DDInstall-section.NetworkProvider]
ShortName = "nw"
```

下面是与 **net view** 命令一起使用的短名称的示例：

```INF
net view /n:nw
```

**短名称** 比网络提供程序的整个名称更容易记住和键入。

**短名称** 是可选的，只应在需要时指定。

 

 





