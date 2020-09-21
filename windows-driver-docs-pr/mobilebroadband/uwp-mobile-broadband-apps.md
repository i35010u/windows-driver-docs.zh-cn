---
title: UWP 移动宽带应用概述
description: UWP 移动宽带应用概述
ms.assetid: bb02397b-0da5-4e09-be1c-8812abec6fd5
ms.date: 07/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: 14884d4d2910403d5b8edb836a944e0e044eb298
ms.sourcegitcommit: 74a8dc9ef1da03857dec5cab8d304e2869ba54a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90759784"
---
# <a name="uwp-mobile-broadband-apps-overview"></a>UWP 移动宽带应用概述

本主题中提供了以下各节：

- [UWP 应用](#uwp-apps)
- [UWP 移动宽带应用](#uwp-mobile-broadband-apps)
- [UWP mobile 宽带应用和 MBAE 应用](#uwp-mobile-broadband-apps-and-mbae)

## <a name="uwp-apps"></a>UWP 应用

UWP 应用是为以下各项定制的全屏或有窗口应用：

-   用户的需求

-   它们运行的设备

-   触摸交互

-   Windows 用户界面

UWP 应用经过优化，可用于触摸，知道用户的位置和标识，并在 Microsoft Store 中托管。 UWP 应用始终处于打开状态并可供使用，并且始终与 web 上的最新内容连接。 用户可以在 Microsoft Store 中发现和购买这些应用：可快速安装应用并将其完全卸载。

所有 UWP 应用都具有以下功能和优势：

-   **开发平台** UWP 应用是使用适用于 Windows 10 的 Windows 软件开发工具包和 Windows 运行时 Api 构建的。

-   **编程语言** 您可以通过将 JavaScript 用于 HTML 和级联样式表 (CSS) 表示层，或者使用 c + + 或 c + + 或 c # 与 Extensible Application Markup Language (XAML) 表示层一起使用来生成 UWP 应用。

-   **触摸优化** 触摸交互支持是内置的。 你可以为触控设计移动宽带应用，Windows 提供键盘、鼠标和图形缩放支持。

有关 UWP 应用的详细信息，请参阅 [Windows 10 应用](/windows/uwp/get-started/)入门。

## <a name="uwp-mobile-broadband-apps"></a>UWP 移动宽带应用


UWP mobile 宽带应用是由移动运营商创作并与移动宽带连接关联的 UWP 应用。 除了成为 UWP 应用的好处外，此应用还具有对特权移动宽带 Api 的特殊访问权限。

移动宽带应用具有以下优势：

-   **客户连接增加** 用户可以从 Windows 的 " **开始** " 屏幕和 "网络" 列表中轻松地发现操作员的品牌和服务。

-   **持续控制体验** 您可以使用该应用程序更改订阅者的帐户体验。

-   **降低部署和维护负担** 该应用会通过 Internet 自动部署到客户设备上，也可以由原始设备制造商预安装。 用户首次附加移动宽带硬件后，Windows 会使用服务元数据自动搜索已与设备关联的移动宽带应用的 Microsoft Store，并为移动宽带连接自动安装适当的应用。 这样，用户就可以更轻松地发现和使用与该设备关联的移动宽带设备和服务。

此应用不提供连接管理功能，而是为你的服务提供帐户体验和品牌。

> [!IMPORTANT]
> 应用必须针对触控输入进行优化，并遵循 Windows 10 UI 设计原则。 有关如何为移动宽带应用设计用户体验的详细信息，请参阅 [设计移动宽带应用的用户体验](designing-the-user-experience-of-a-mobile-broadband-app.md)。

## <a name="uwp-mobile-broadband-apps-and-mbae"></a>UWP mobile 宽带应用和 MBAE

在 Windows 10 版本1803及更高版本中，MO UWP apps 替换了移动宽带应用体验应用或 MBAE 应用。 MO UWP 应用现在是 COSA 的一部分，无需在 Windows 开发人员中心硬件仪表板上创建服务元数据， (Sysdev) 。 1803之前的 windows 8、Windows 8.1 和 Windows 10 版本通过 Sysdev 上发布的服务元数据继续使用 MBAE 应用。 

在 Windows 10 版本1803中，MBAE 应用无需迁移到 COSA 即可工作。 但是，我们强烈建议移动运营商迁移到 MO UWP 应用和 COSA。 有关 COSA 的详细信息，请参阅 [COSA 概述](cosa-overview.md)。 有关 COSA 设置的详细信息，请参阅 [DESKTOP COSA/APN 数据库设置](desktop-cosa-apn-database-settings.md)。

如果在 COSA 中填写 **AppID** 设置，则 Windows 将不会检查匹配的 Sysdev metadata 包以下载应用。 如果未填写 **AppID** ，则 Windows 将检查匹配的 Sysdev 元数据包以下载应用。

下表提供了有关 MBAE 和 MO UWP 应用之间的差异的信息。

|  应用类型 | 目标平台 | 传递机制 | 图标检索 |
| --- | --- | --- | --- |
| MBAE | Windows 8、Windows 8.1 或 Windows 10 | Sysdev 元数据 | Sysdev metadata 或 COSA （如果声明为配置文件的一部分） | 
| MO UWP 应用 | Windows 10 (最好版本1803及更高版本，具有相同的 SDK 版本)  | COSA 数据库 | COSA 数据库 |

由于 Windows 8/Windows 8.1 和 Windows 10 UI 原则之间的更改，MBAE 和 MO UWP 应用之间的 UI 源代码可能会有所不同。 然而，大多数业务逻辑源代码不需要做很多更改。 例如，用于访问后端和访问移动宽带信息的代码可能是相同的。 但是，MOs 应该相应地验证每个 [移动宽带应用方案](./account-management.md) 。