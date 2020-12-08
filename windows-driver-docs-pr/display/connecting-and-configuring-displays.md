---
title: 连接和配置显示
description: 连接和配置显示
keywords:
- 显示 WDK Windows 7 显示
- 显示 WDK Windows Server 2008 R2 显示
- 显示 WDK Windows 7 显示，连接
- 显示 WDK Windows Server 2008 R2 显示，连接
- 显示 WDK Windows 7 显示，配置
- 显示 WDK Windows Server 2008 R2 显示，配置
- 连接显示 WDK Windows 7 显示
- 连接显示 WDK Windows Server 2008 R2 显示器
- 配置显示 WDK Windows 7 显示
- 配置显示 WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b87ebe58232ce9d3b2e07e461197d939ad05b6d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810173"
---
# <a name="connecting-and-configuring-displays"></a>连接和配置显示


本部分仅适用于 Windows 7 和更高版本，以及 Windows Server 2008 R2 及更高版本的 Microsoft Windows 操作系统。

新的连接和配置显示了在 [CCD DDIs](ccd-ddis.md) 中介绍的 (CCD) Win32 api，可更好地控制桌面显示器设置。 它们还可用于使您的应用程序 [在纵向设备上正确显示](displaying-app-on-portrait-device.md)。 例如，在 Windows 7 之前的 Windows 版本中，无法使用 **ChangeDisplaySettingsEx** 函数设置克隆模式。 新的 CCD Api 脱离了使用 Windows 图形设备接口 (GDI) 概念，如视图名称和面向 [Windows 的显示驱动程序模型 (WDDM) ](windows-vista-display-driver-model-design-guide.md) 概念，如适配器、源和目标标识符。

 (HPD) manager 的 "显示控制面板"、"新建热键" 和 "热插拔检测" 可以使用 CCD Api。 Oem 可以将 CCD Api 用于其值-添加 applet，而不是使用私有驱动程序转义。

CCD Api 提供以下功能：

-   枚举当前连接的显示中可能的显示路径。

-   设置拓扑 (例如，克隆和扩展一个函数调用中所有已连接显示器的) 、布局信息、分辨率、方向和纵横比。 通过对一个函数调用中的所有连接的显示执行多个设置，减少屏幕闪烁的次数。

-   添加或更新持久性数据库的设置。

-   应用保存在数据库中的设置。

-   使用最佳模式逻辑应用最佳显示设置。

-   使用最佳拓扑逻辑应用所连接显示器的最佳拓扑。

-   启动或停止强制输出。

-   允许 OEM 热键使用新的操作系统持久性数据库。

CCD Api 无法处理以下任务。 此外，CCD Api 与 [Windows 2000 显示驱动程序模型](windows-2000-display-driver-model-design-guide.md)不向后兼容。

-   替换硬件供应商先前提供的用于控制桌面显示器设置的 API 集和私有驱动程序转义符。

-   将专用数据向下传递到内核模式显示微型端口驱动程序。

-   提供一组新的监视控件 Api。

-   查询监视器功能，其中包括 EDID、DDCCI 等。

-   提供用于唯一标识 CCD Api 从持久性数据库中检索的设置的上下文标识符。

-   尽管 CCD Api 允许调用方获取和设置显示，但它们并不提供用于枚举给定路径中可能的源模式的任何功能。 Windows 7 之前存在的 Api 已经提供此功能。

以下部分更详细地介绍了 CCD Api：

[CCD 概念](ccd-concepts.md)

[CCD API](ccd-apis.md)

**注意**   除了使用 CCD Api 设置桌面显示器，硬件供应商还必须修改其 Windows 7 [Windows 显示器驱动程序模型 (WDDM)](windows-vista-display-driver-model-design-guide.md) 显示微型端口驱动程序以支持 CCD。 有关在显示微型端口驱动程序中支持 CCD 的详细信息，请参阅 [CCD DDIs](ccd-ddis.md)。

 

 

 





