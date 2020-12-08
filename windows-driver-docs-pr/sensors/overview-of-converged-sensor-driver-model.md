---
title: 通用传感器驱动程序模型概述
description: 在 Windows 10 中，桌面和移动设备的传感器驱动程序堆栈已合并以创建通用传感器驱动程序模型。
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3a8b1de5dc3d56c0bc7196e7233d9db8280945cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812341"
---
# <a name="overview-of-the-universal-sensor-driver-model"></a>通用传感器驱动程序模型概述


在 Windows 10 中，桌面和移动设备的传感器驱动程序堆栈已合并以创建通用传感器驱动程序模型。

硬件合作伙伴现在可以构建一个可在所有 Windows 设备平台上运行的驱动程序及其关联的应用程序。

>[!NOTE]
> 对于桌面版 (Home、Pro、Enterprise 和教育) 以及 Windows 10 移动版支持 KMDF 传感器驱动程序，适用于 Windows 10 的 Windows 10 支持1.0 版 UMDF 传感器驱动程序。

 

基于通用 Windows 驱动程序模型开发的传感器设备驱动程序，它们是使用最新版本的用户模式驱动程序框架（UMDF 2.0）来实现的。

通用传感器驱动程序模型具有以下功能：

-   允许每个驱动程序有多个传感器，以减少支持更多传感器所需的驱动程序数。
-   使用 (CS) 和当前报表间隔 (CRI) 的更改敏感度，以提供数据限制以提高电源使用情况并减少数据干扰。
-   使用基于统一 PROPERTYKEY/PROPVARIANT 的系统提供扩展性。
-   为 WinRT Api 提供向后兼容性。
-   支持 CX) 型号 (类扩展。 这提供的功能包括管理连接和订阅、在传感器可以断电时通知驱动程序，以及管理 i/o 队列和 i/o 请求的生存期。
-   支持 Windows 10 中新的传感器类型，例如，6轴合成传感器 (加速感应器 + Gyro) 。
-   支持基于 Windows core 体系结构的 Sku 的通用 HID 传感器类驱动程序。 这些 Sku 包括 Windows 10 移动版。  (以前，只有 Windows) 的桌面 Sku 支持 HID 传感器类驱动程序。
-   支持自定义传感器，通过 WinRT。

目前正在为 Windows 的下一个版本进行工作，这将允许 HID 传感器类驱动程序支持更多的传感器类型。 这些传感器类型包括 Pedometer 和传感器，用于活动检测、线性加速度、重力矢量、磁场方向等。

此外，通用传感器驱动程序模型为我们的合作伙伴带来了以下好处：

-   现在所有传感器都是可选的。 现在，合作伙伴可以选择在开发低成本设备时只包含所需的传感器。 这使他们能够更灵活地降低 BOM 成本
-   现在提供了 OEM 可替换的设备方向算法，OEM 可以选择不使用。
-   已从 Windows 中删除对加速感应器、环境光线传感器、陀螺仪、磁力仪、方向和邻近感应传感器的 "最小报表间隔" 要求。 这是创建汇聚机箱规范的结果。

下图显示组成通用传感器驱动程序模型的组件：

![汇聚传感器驱动程序模型的体系结构关系图。](images/sensorsv2-arch.png)

请注意，Microsoft Store Apps 组件可以包含由 Microsoft 开发的应用，也可以由第三方开发人员组成传感器。

 

 




