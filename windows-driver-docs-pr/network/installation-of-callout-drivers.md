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
ms.openlocfilehash: 12200ae5547499daf0dfc284ccf50df25da619b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324931"
---
# <a name="installation-of-callout-drivers"></a>标注驱动程序的安装


可以通过右键单击驱动程序的安装信息文件 (INF) 文件并选择安装的标注驱动程序**安装**从显示的弹出菜单。

标注驱动程序已成功安装后，它可以加载 （已启动） 通过在命令提示符下键入以下内容：

```cpp
net start drivername
```

为指定的值根据**StartType**中的条目\[ *drivername*。服务\]INF 文件标注驱动程序的部分可能会自动加载下次重新启动系统。 标注驱动程序通常应指定零 (服务\_启动\_开始) 为此值使是否加载了驱动程序，并且其标注在注册之前筛选器引擎已启动。 请参阅[ **INF AddService 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546326)有关详细信息。

可以卸载当前加载的标注驱动程序 （停止） 通过在命令提示符下键入以下内容：

```cpp
net stop drivername
```

标注驱动程序也可以安装、 加载 （已启动），卸载 （停止） 和/或通过编写调用 Win32 服务控制管理器 API 的用户模式应用程序卸载。 有关 Win32 服务控制函数，如**CreateService**， **OpenService**， **StartService**， **control服务**，并**DeleteService**，请参阅[Microsoft Windows SDK](https://go.microsoft.com/fwlink/p/?linkid=122165)。

> [!NOTE]
> 从 Windows 8 及更高版本，标注驱动程序无法查看，或管理的设备管理器中，因为即插即用 Play (PnP) 管理器无法再创建为非 PnP （旧） 设备的设备表示形式。
