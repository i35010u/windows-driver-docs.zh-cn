---
title: 预加载驱动程序包
description: 预加载驱动程序包
keywords:
- 安装应用程序 WDK，预加载的驱动程序包
- 设备安装应用程序 WDK，预加载的驱动程序包
- 预加载的驱动程序包 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07a2fb982f79c2c79ded1cf81be1752baab1cbcd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796053"
---
# <a name="preloading-driver-packages"></a>预加载驱动程序包


在 Windows 安装过程中或在计算机上安装 Windows 后，可以在计算机上 *预加载* 即插即用 (PnP) [驱动程序包](driver-packages.md)。 网络管理员还可以在为网络计算机上安装的驱动程序包提供源的网络服务器上预加载驱动程序包。 当 Windows 搜索与设备匹配的驱动程序时，Windows 将检查是否存在与设备匹配的预加载的驱动程序包。

如何配置 Windows 安装以预加载驱动程序包超出了本文档的范围。 有关如何配置 Windows 安装以预加载驱动程序包的信息，请参阅 [如何向 WINDOWS XP 添加 oem 即插即用驱动](https://go.microsoft.com/fwlink/p/?linkid=3100&ID=314479) 程序和 [如何将 Oem 即插即用驱动程序添加到 windows 安装](/troubleshoot/windows-server/deployment/add-oem-plug-play-drivers)。

安装 Windows 后，可以通过以下方式之一预加载 [驱动程序包](driver-packages.md) ：

1.  若要在本地计算机上预加载驱动程序包，请将驱动程序包复制到本地计算机上特定于包的目录中，并将驱动程序包的本地目录路径连接到注册表的 **Hklm\ \\ SOFTWARE \\ Microsoft \\ Windows \\ CurrentVersion** 子项下的 **DevicePath** 值条目。

2.  若要预加载计算机网络的驱动程序包，网络管理员可以将驱动程序包复制到网络服务器上的共享目录，并将共享目录的路径连接到有权访问共享目录的网络计算机的注册表中的 **DevicePath** 值条目。

**DevicePath** 值条目是一个 [REG_EXPAND_SZ](/windows/desktop/SysInfo/registry-value-types)类型的条目，其中包含 *% SystemRoot% \\ inf* 目录路径以及零个或多个目录路径条目。 **DevicePath** 值条目的格式如下所示，其中每个目录路径都是本地目录路径或网络服务器上的共享目录的路径，预加载的 [驱动程序包](driver-packages.md)位于该位置：

```cpp
%SystemRoot%\inf;DirectoryPath1;DirectoryPath2;...
```

例如，若要在本地计算机上的 *% SystemRoot% driver \\ \\ NIC* 目录中预加载网络适配器的驱动程序包，管理员需要将驱动程序包复制到该目录并连接 **DevicePath** 值条目的路径，如下所示：

```cpp
%SystemRoot%\inf;...;%SystemRoot%\inf\Drivers\NIC
```

例如，若要为网络上的共享目录 DriverPackageServer 共享项 *\\ \\ \\ 驱动程序 \\ \\ NIC* 中的网络适配器预加载驱动程序包，网络管理员会将驱动程序包复制到该共享目录，并连接网络计算机注册表中 " **DevicePath** " 值条目的共享目录路径，如下所示：

```cpp
%SystemRoot%\inf;...;\\DriverPackageServer\ShareName\Drivers\NIC
```

> [!NOTE]
> 在具有 point 和打印客户端连接的计算机的 DevicePath 中指定网络共享可能导致网络共享访问过多和打印延迟。 这是因为每次 printerdata 在服务器中发生更改时，客户端将循环访问 DevicePath 目录以检查是否有较新的打印驱动程序的可用性。
