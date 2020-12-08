---
title: 标注驱动程序的安装
description: 标注驱动程序的安装
keywords:
- Windows 筛选平台标注驱动程序 WDK，安装
- 标注驱动程序 WDK Windows 筛选平台，安装
- 安装标注驱动程序 WDK Windows 筛选平台
- 加载驱动程序 WDK Windows 筛选平台
- INF 文件 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6aba0863c1d6bb173b3b5a3266e8c17f3a95fa0d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803523"
---
# <a name="installation-of-callout-drivers"></a>标注驱动程序的安装


可以通过右键单击驱动程序的安装信息文件 (INF) 文件，然后从出现的弹出菜单中选择 " **安装** " 来安装标注驱动程序。

成功安装了标注驱动程序后，可通过在命令提示符下键入以下内容， (启动) 加载该驱动程序：

```cpp
net start drivername
```

根据为 drivername 中的 **StartType** 条目指定的值 \[ *drivername*。服务 " \] 部分中，系统下次重新启动时，可能会自动加载标注驱动程序。 标注驱动程序通常应为此值指定零 (服务 \_ 启动 \_ 开始) ，以便在启动筛选器引擎之前加载驱动程序并注册其标注。 有关详细信息，请参阅 [**INF AddService 指令**](../install/inf-addservice-directive.md) 。

可以通过在命令提示符下键入以下内容，将当前加载的标注驱动程序卸载 (停止) ：

```cpp
net stop drivername
```

还可以通过编写调用 Win32 服务控制管理器 API 的用户模式应用程序，安装、加载 (启动) 、卸载 (停止) 和/或卸载标注驱动程序。 有关 Win32 服务控制功能的详细信息，如 **CreateService**、 **OpenService**、 **StartService**、 **control 服务** 和 **DeleteService**，请参阅 [Microsoft Windows SDK](/windows/win32/services/service-reference)。

> [!NOTE]
> 从 Windows 8 及更高版本开始，无法在设备管理器中查看或管理标注驱动程序，因为即插即用 (PnP) 管理器不再为非 PnP (旧) 设备创建设备表示形式。
