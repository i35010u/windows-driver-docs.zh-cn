---
title: 预加载的驱动程序包
description: 预加载的驱动程序包
ms.assetid: e617764d-0b48-4cd8-aeac-04d6039aba71
keywords:
- 安装应用程序 WDK，预加载的驱动程序包
- 设备安装应用程序 WDK，预加载的驱动程序包
- 预加载的驱动程序包 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70c02af27baab235d5f4d857d4be127a855b8371
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522891"
---
# <a name="preloading-driver-packages"></a>预加载的驱动程序包


插即用 (PnP)[驱动程序包](driver-packages.md)可以是*预加载*Windows 安装的或者之后的计算机上安装 Windows 的计算机上。 网络管理员也可以预加载的网络计算机安装的驱动程序包中提供的源的网络服务器上的驱动程序包。 当 Windows 搜索与设备匹配的驱动程序时，Windows 将检查是否有与设备匹配的预加载的驱动程序包。

如何配置预加载的驱动程序包的 Windows 安装是此文档的讨论范围内。 有关如何配置 Windows 安装，预加载的驱动程序包的信息，请参阅[如何添加 OEM 即插即用和驱动程序与 Windows XP](https://go.microsoft.com/fwlink/p/?linkid=3100&ID=314479)和[如何添加 OEM 即插即用和驱动程序与 Windows 安装](https://go.microsoft.com/fwlink/p/?linkid=70235).

安装 Windows 后，[驱动程序包](driver-packages.md)可以采用以下方式之一预加载：

1.  若要预加载在本地计算机上的驱动程序包，将驱动程序包复制到本地计算机上的特定于包的目录，并连接到驱动程序包的本地目录路径**DevicePath**值下条目**HKLM\\软件\\Microsoft\\Windows\\CurrentVersion**的注册表子项。

2.  若要预加载计算机网络的驱动程序包，网络管理员可以将驱动程序包复制到网络服务器上的共享目录并将连接到的共享目录的路径**DevicePath**值中的项目有权访问共享目录的网络计算机的注册表。

**DevicePath**值项是[REG_EXPAND_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)-键入包含项 *%systemroot%\\inf*目录路径和零个或多个目录路径条目。 格式**DevicePath**值项是以下内容，其中每个目录路径是本地目录路径或网络服务器上共享目录的路径位置预加载[驱动程序包](driver-packages.md)所在：

```cpp
%SystemRoot%\inf;DirectoryPath1;DirectoryPath2;...
```

例如，若要预加载中的网络适配器的驱动程序包 *%systemroot%\\驱动程序\\NIC*目录的本地计算机上，管理员将驱动程序包复制到该目录和连接的路径**DevicePath**值项，按如下所示：

```cpp
%SystemRoot%\inf;...;%SystemRoot%\inf\Drivers\NIC
```

例如，若要预加载的共享目录中的网络适配器的驱动程序包 *\\ \\DriverPackageServer\\ShareName\\驱动程序\\NIC*在网络中，网络管理员将驱动程序包复制到共享目录，并将连接的共享的目录路径**DevicePath**值中的网络计算机的注册表条目，如下所示：

```cpp
%SystemRoot%\inf;...;\\DriverPackageServer\ShareName\Drivers\NIC
```

 

 





