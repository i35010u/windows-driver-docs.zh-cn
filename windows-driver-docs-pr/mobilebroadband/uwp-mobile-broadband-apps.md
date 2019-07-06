---
title: UWP 移动宽带应用程序概述
description: UWP 移动宽带应用程序概述
ms.assetid: bb02397b-0da5-4e09-be1c-8812abec6fd5
ms.date: 07/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: eeee111f72524da72685883471b124dcb79664b9
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608552"
---
# <a name="uwp-mobile-broadband-apps-overview"></a>UWP 移动宽带应用程序概述

本主题中提供了以下各节：

- [UWP 应用](#uwp-apps)
- [UWP 移动宽带应用程序](#uwp-mobile-broadband-apps)
- [UWP 移动宽带应用程序和 MBAE 应用](#uwp-mobile-broadband-apps-and-mbae)

## <a name="uwp-apps"></a>UWP 应用

UWP 应用是全屏幕或窗口专门针对以下编写的应用：

-   用户的需求

-   它们运行的设备

-   触摸交互

-   Windows 用户界面

UWP 应用针对触控进行了优化，了解用户的位置和标识，和托管在 Microsoft Store。 UWP 应用始终上并可供即时使用，并始终相连 web 的最新内容。 用户可以发现和购买 Microsoft Store 中的这些应用： 应用程序可以快速安装和完全卸载。

所有 UWP 应用都共享以下功能和优点：

-   **开发平台**UWP 应用使用生成的 Windows 软件开发工具包适用于 Windows 10 和 Windows 运行时 Api。

-   **编程语言**可生成 UWP 应用，通过使用 JavaScript with HTML 和级联样式表 (CSS) 表示层，或通过使用C++或C#与 Extensible Application Markup Language (XAML) 表示层。

-   **触摸优化**触摸交互支持已内置。 您可以设计您的触控体验，移动宽带的应用程序，并且 Windows 提供键盘、 鼠标和图形的缩放支持。

有关 UWP 应用的详细信息，请参阅[开始开发 Windows 10 应用](https://docs.microsoft.com/windows/uwp/get-started/)。

## <a name="uwp-mobile-broadband-apps"></a>UWP 移动宽带应用


UWP 移动宽带应用是由移动运营商编写，并且与移动宽带连接相关联的 UWP 应用。 除了 UWP 应用的优点，此应用具有特权的移动宽带 api 的特殊访问权限。

移动宽带应用提供以下优势：

-   **提高客户连接**操作员的品牌和从 Windows 服务，用户可以轻松地发现**启动**屏幕，以及从网络列表。

-   **对体验进行控制**可用应用程序来更改订阅服务器的帐户体验。

-   **减少了部署和维护负担**通过使用 Internet 的客户设备上自动部署应用程序或由原始设备制造商预安装。 当用户首次附加移动宽带硬件时，Windows 会自动搜索的移动宽带应用程序已通过使用服务元数据与设备相关联，会自动安装相应的应用的 Microsoft Store移动宽带连接。 这使用户更轻松地发现和使用移动宽带设备和与该设备相关联的服务。

此应用程序不提供连接的管理功能，而是提供帐户体验和适用于你的服务的品牌。

> [!IMPORTANT]
> 您的应用程序必须针对触摸屏输入进行优化，并遵循 Windows 10 UI 设计原则。 有关如何设计的移动宽带应用程序的用户体验的详细信息，请参阅[设计用户体验的移动宽带应用](designing-the-user-experience-of-a-mobile-broadband-app.md)。

## <a name="uwp-mobile-broadband-apps-and-mbae"></a>UWP 移动宽带应用程序和 MBAE

移动宽带应用体验应用或 MBAE 应用，在 Windows 10，版本 1803年和更高版本的月 UWP 应用中替换。 MO UWP 应用现在是 COSA 的一部分，无需在 Windows 开发人员中心硬件仪表板 (Sysdev) 上创建服务元数据。 Windows 8、 Windows 8.1 和 Windows 10 之前继续使用通过 Sysdev 上发布服务元数据的 MBAE 应用 1803年的版本。 

在 Windows 10，版本 1803，MBAE 应用而无需将迁移到 COSA 工作。 但是，我们强烈建议移动运营商迁移到一个月 UWP 应用和 COSA。 有关 COSA 详细信息，请参阅[COSA 概述](cosa-overview.md)。 有关 COSA 设置的详细信息，请参阅[桌面 COSA/APN 数据库设置](desktop-cosa-apn-database-settings.md)。

如果**AppID**设置填写 COSA 中，Windows 将不检查匹配的 Sysdev 元数据包，若要下载你的应用。 如果**AppID**未填充，则 Windows 将检查是否有匹配的 Sysdev 元数据包，若要下载你的应用。

下表提供了有关 MBAE 和月 UWP 应用程序之间的差异的信息。

|   | 目标平台 | 交付机制 | 图标检索 |
| --- | --- | --- | --- |
| MBAE | Windows 8、 Windows 8.1 或 Windows 10 | Sysdev 元数据 | Sysdev 元数据或 COSA 如果声明为配置文件的一部分 | 
| MO UWP 应用 | Windows 10 （最好是版本 1803 和更高版本使用相同的 SDK 版本） | COSA 数据库 | COSA 数据库 |

UI 之间 MBAE 和月 UWP 应用的源代码可能会因 Windows 8/Windows 8.1 和 Windows 10 UI 原则之间的更改。 但是，大多数业务逻辑源代码，应该不需要很多更改。 例如，用于访问后端和访问移动宽带信息的代码可能相同。 但是，MOs 应验证每个[移动宽带应用方案](mobile-broadband-app-scenarios.md)相应地。
