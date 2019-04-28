---
title: 连接和配置显示
description: 连接和配置显示
ms.assetid: 8c16f99e-c7fd-46e2-b102-f5f0a297fbec
keywords:
- 显示 WDK Windows 7 显示
- 显示 WDK Windows Server 2008 R2 显示
- 显示 WDK Windows 7 显示连接
- 显示 WDK Windows Server 2008 R2 显示连接
- 显示 WDK Windows 7 显示配置
- 显示 WDK Windows Server 2008 R2 显示配置
- 连接显示 WDK Windows 7 显示
- 连接显示 WDK Windows Server 2008 R2 显示
- 配置显示 WDK Windows 7 显示
- 配置显示 WDK Windows Server 2008 R2 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 009254a44c1b873eea26023ec2ba5cc6c0dff709
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327527"
---
# <a name="connecting-and-configuring-displays"></a>连接和配置显示


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Microsoft Windows 操作系统。

新的连接和配置显示 (CCD) 中所述的 Win32 Api [CCD DDIs](ccd-ddis.md)提供更好地控制桌面显示安装程序。 它们还可用于使应用能够[纵向设备上正确显示](displaying-app-on-portrait-device.md)。 例如，在 Windows 7 之前的 Windows 版本，它是不可能使用设置克隆模式**ChangeDisplaySettingsEx**函数。 新的 CCD Api 将从使用 Windows 图形设备接口 (GDI) 概念类似视图名称和向移[Windows 显示器驱动程序模型 (WDDM)](windows-vista-display-driver-model-design-guide.md)概念，如适配器、 源和目标的标识符。

显示控件面板、 新热键和热插拔检测 (HPD) 管理器可以使用 CCD Api。 Oem 可以使用 CCD Api，可用于其值的添加而不是使用专用驱动程序转义符的小程序。

CCD Api 提供以下功能：

-   枚举是从当前连接的显示可能的显示路径。

-   设置拓扑 （例如，克隆和扩展），布局信息、 解析、 方向和一个函数调用中的所有连接显示的纵横比。 通过对所有已连接显示在一个函数调用中执行多个设置，减少屏幕闪烁的数。

-   添加或更新到持久性数据库的设置。

-   将保留在数据库中的设置应用。

-   使用最佳模式逻辑应用的最佳显示设置。

-   使用最佳的拓扑逻辑应用连接显示的最佳拓扑。

-   启动或停止强制的输出。

-   允许 OEM 热密钥，以便使用新的操作系统持久性数据库。

CCD Api 不能处理以下任务。 此外，CCD Api 不向后的兼容[Windows 2000 显示器驱动程序模型](windows-2000-display-driver-model-design-guide.md)。

-   替换的 API 集和专用驱动程序检测不到控制桌面以前提供的硬件供应商显示安装程序。

-   将传递到内核模式显示微型端口驱动程序的专用数据。

-   提供一组新的监视器控件 Api。

-   查询监视器功能，包括 EDID、 DDCCI，等等。

-   提供一个上下文标识符，用于唯一地标识 CCD Api 从持久性数据库中检索的设置。

-   尽管 CCD Api 允许调用方来获取和设置显示，但它们不提供任何功能来枚举给定路径中的可能的源模式。 已为 Windows 7 之前存在的 Api 提供的此功能。

以下部分介绍了更详细地 CCD Api:

[CCD 概念](ccd-concepts.md)

[CCD Api](ccd-apis.md)

**请注意**  除了使用 CCD Api 将桌面显示设置，硬件供应商必须修改其 Windows 7 [Windows 显示驱动程序模型 (WDDM)](windows-vista-display-driver-model-design-guide.md)支持 CCD 显示微型端口驱动程序。 在显示微型端口驱动程序中支持 CCD 的详细信息，请参阅[CCD DDIs](ccd-ddis.md)。

 

 

 





