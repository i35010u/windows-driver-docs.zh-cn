---
title: 包括 NetworkProvider 部分
description: 包括 NetworkProvider 部分
ms.assetid: 8972f926-c4f5-4a2f-8f2d-f9353fdbd83f
keywords:
- INF 文件 WDK 网络，NetworkProvider 部分
- 可使用网络 INF 文件 WDK，NetworkProvider 部分
- NetworkProvider 部分 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e13c6bbbc5927cf4577f5c854d9c3089950126dd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545733"
---
# <a name="including-a-networkprovider-section"></a>包括 NetworkProvider 部分





一个**NetworkProvider**部分中指定的替换设备名称为**NetClient**组件或与 NetWare 一起使用的短名称**net 视图**命令还是两个。

**请注意**  **NetClient**组件在 Windows 8.1，Windows Server 2012 R2 中已弃用及更高版本。

 

若要创建**NetworkProvider**部分中，添加**NetworkProvider**扩展*DDInstall*部分组件，如下面的示例中所示：
```INF
[DDInstall] ; Install section
[DDInstall.NetworkProvider] ; NetworkProvider section
```

### <a name="specifying-a-device-name"></a>指定设备名称

网络类安装程序通常通过复制来创建网络提供商的设备名称**Ndi\\服务**下的组件的 NetworkProvider 键组件值**服务**密钥。 有关详细信息，请参阅[Adding Service-Related 值到 Ndi 密钥](adding-service-related-values-to-the-ndi-key.md)。 若要指定不同的设备名称的组件，包括**DeviceName**中的条目**NetworkProvider**部分组件，如下面的示例中所示：

```INF
[DDInstall-section.NetworkProvider]
DeviceName = "nwrdr"
```

**DeviceName**是可选的才应指定**Ndi\\服务**值的组件是作为网络提供商的设备名称不能满足需要。

### <a name="specifying-a-short-name"></a>指定的短名称

若要指定使用的网络提供程序的短名称具有 NetWare **net 视图**命令，包括**短名称**中的条目**NetworkProvider**部分组件，如下面的示例中所示：

```INF
[DDInstall-section.NetworkProvider]
ShortName = "nw"
```

下面是用于短名称的一个示例**net 视图**命令：

```INF
net view /n:nw
```

**短名称**容易记住和键入比网络提供程序的完整名称。

**短名称**是可选的应该只指定的如果需要。

 

 





