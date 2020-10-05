---
title: 标注驱动程序的安装
description: 标注驱动程序的安装
ms.assetid: 3baefd81-04bc-4a34-b4cd-afa544308a90
keywords:
- Windows 筛选平台标注驱动程序 WDK，安装
- 标注驱动程序 WDK Windows 筛选平台，安装
- 安装标注驱动程序 WDK Windows 筛选平台
- 加载驱动程序 WDK Windows 筛选平台
- INF 文件 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03b331301ef105e0c840e08884d6e349733de89e
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733937"
---
# <a name="installation-of-callout-drivers"></a>标注驱动程序的安装


可以通过右键单击驱动程序的安装信息文件 (INF) 文件，然后从出现的弹出菜单中选择 " **安装** " 来安装标注驱动程序。

成功安装了标注驱动程序后，可通过在命令提示符下键入以下内容， (启动) 加载该驱动程序：

```cpp
net start drivername
```

根据为 drivername 中的**StartType**条目指定的值 \[ *drivername*。服务 " \] 部分中，系统下次重新启动时，可能会自动加载标注驱动程序。 标注驱动程序通常应为此值指定零 (服务 \_ 启动 \_ 开始) ，以便在启动筛选器引擎之前加载驱动程序并注册其标注。 有关详细信息，请参阅 [**INF AddService 指令**](../install/inf-addservice-directive.md) 。

可以通过在命令提示符下键入以下内容，将当前加载的标注驱动程序卸载 (停止) ：

```cpp
net stop drivername
```

还可以通过编写调用 Win32 服务控制管理器 API 的用户模式应用程序，安装、加载 (启动) 、卸载 (停止) 和/或卸载标注驱动程序。 有关 Win32 服务控制功能的详细信息，如 **CreateService**、 **OpenService**、 **StartService**、 **control 服务**和 **DeleteService**，请参阅 [Microsoft Windows SDK](/windows/win32/services/service-reference)。

> [!NOTE]
> 从 Windows 8 及更高版本开始，无法在设备管理器中查看或管理标注驱动程序，因为即插即用 (PnP) 管理器不再为非 PnP (旧) 设备创建设备表示形式。