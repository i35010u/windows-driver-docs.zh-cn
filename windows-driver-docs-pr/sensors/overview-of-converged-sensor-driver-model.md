---
title: 通用传感器驱动程序模型概述
description: 在 Windows 10 桌面和移动设备的传感器驱动程序堆栈已合并以创建通用传感器驱动程序模型。
ms.assetid: 3591F4DD-2404-4893-88F3-1DC6A0CC3F0D
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5e7205b333c10e1ec19a8fe5843222f9ecd527a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522853"
---
# <a name="overview-of-the-universal-sensor-driver-model"></a>通用传感器驱动程序模型概述


在 Windows 10 桌面和移动设备的传感器驱动程序堆栈已合并以创建通用传感器驱动程序模型。

硬件合作伙伴现在可以生成单个驱动程序，以及其关联的应用，可在所有 Windows 设备平台上运行。

>[!NOTE]
> 对于桌面版本 （主页、 专业版、 企业版和教育版），在 Windows 10 中支持 V1.0 UMDF 传感器驱动程序和 KMDF 传感器驱动程序支持的 Windows 10 移动版。

 

传感器设备驱动程序开发的基于通用 Windows 驱动程序模型，以及通过使用最新版本的用户模式驱动程序框架-UMDF 2.0 实现这些概念。

通用传感器驱动程序模型具有以下功能：

-   允许多个传感器每个驱动程序，以减少驱动程序支持多个传感器所需的数量。
-   使用更改敏感度 (CS) 和当前的报告间隔 (CRI) 提供数据限制，以提高电源使用情况并降低数据噪声。
-   提供使用统一的基于 PROPERTYKEY/PROPVARIANT 的系统的可扩展性。
-   提供向后的兼容性 WinRT Api。
-   支持的类扩展 (CX) 模型。 这提供了功能，其中包括管理连接和订阅、 传感器可以关闭时通知该驱动程序和管理的 I/O 队列和 I/O 请求生存期。
-   支持新于 Windows 10，例如，6 轴合成传感器 （加速感应器 + 回转仪） 等的传感器类型。
-   对基于 Windows 的核心体系结构的 Sku 的通用 HID 传感器类驱动程序支持。 这些 Sku 包括 Windows 10 移动版。 （以前，HID 传感器类驱动程序仅支持在 Windows 的桌面 Sku 上）。
-   对于自定义传感器，通过 WinRT 的支持。

有工作当前正在为下一版本的 Windows，将允许 HID 传感器类驱动程序以支持更多传感器类型。 这些传感器类型包括活动检测、 线性加速、 向量重力、 Geomagnetic 方向等计步器和传感器。

此外，通用传感器驱动程序模型为我们的合作伙伴提供以下优势：

-   所有传感器现在都是可选的。 合作伙伴现在可以选择包含所需时他们开发的成本较低的设备的传感器。 这使它们更灵活地 BOM 成本降至最低。
-   现在有了，OEM 还可以选择不使用的 OEM 可替换设备方向算法。
-   加速感应器、 环境光线传感器、 陀螺仪、 磁力仪，方向和接近传感器的"最小报表时间间隔内"要求已从 Windows 中删除。 这是创建汇聚的底盘规范的结果。

下图显示了组成的通用传感器驱动程序模型的组件：

![聚合的传感器驱动程序模型的体系结构关系图。](images/sensorsv2-arch.png)

请注意，Microsoft Store 应用程序组件可以包含由 Microsoft 或第三方开发人员随附传感器开发的应用。

 

 




