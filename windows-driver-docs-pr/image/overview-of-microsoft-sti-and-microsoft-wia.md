---
title: Microsoft STI 和 Microsoft WIA 概述
description: Microsoft STI 和 Microsoft WIA 概述
ms.assetid: c973f9a2-48a5-420f-b317-0797171cf714
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: ef11d4821c786cccb6725049e8a0819e6c95be4e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392643"
---
# <a name="overview-of-microsoft-sti-and-microsoft-wia"></a>Microsoft STI 和 Microsoft WIA 概述

在旧的 Windows 操作系统映像的体系结构包括低级别的硬件抽象、 STI，以及一组高级的名为 TWAIN 的 Api。 在现代 Windows 操作系统中，Microsoft 使用 Windows 图像处理体系结构 (WIA)，基于 STI 映像体系结构。 下图说明了这些两个映像的体系结构。

![关系图说明了 twain / sti 和 microsoft wia 映像体系结构](images/sti-wia.png)

上图中，TWAIN 中所示 / STI 体系结构包括 TWAIN，图像采集 Api，以及 STI，低级别的硬件抽象一高级组。 WIA 体系结构为基础提供的完整解决方案的图像处理设备 Ihv 合并 STI。

### <a name="differences-between-sti-and-wia"></a>STI 和 WIA 之间的差异

WIA 驱动程序提供的 STI 为基础构建的并因此公开 STI 除了其自己的接口。 WIA 驱动程序必须公开至少**IStiUSD**接口。 STI 具有任何 WIA 接口上没有相应的依赖项。 由于 WIA 微型驱动程序必须符合 STI 微型驱动程序，就可以编写只 STI 微型驱动程序，使支持 WIA 的照相机或扫描仪 STI 映像设备。 但是，获得更好的用户体验建议 WIA。 例如，照相机 STI 驱动程序不显示在资源管理器中的缩略图。

STI 与 WIA 之间有些区别包括：

-   在客户端应用程序和系统服务进程; 运行 STIWIA 系统服务进程中运行。

-   STI，正在是低级别的硬件抽象，必须具有详细有关设备的信息，才能正常运行;WIA 可以运行不带此类设备详细的信息。

-   STI 不是完整的映像接口;WIA STI 上构建，是映像 ihv 完整的解决方案。 IHV 提供 UI 模块 (例如，Twain，) 必需 STI 体系结构中的因为它仅设备通信机制，并且不具有 UI 的前端。 WIA 微型驱动程序不需要其自己的 UI 模块，因为没有默认值 UI （扫描仪和照相机向导）。 此外，通过 TWAIN 兼容性层 WIA 体系结构中支持 Twain 接口。 Ihv 可以扩展或替换这些默认 Ui 中 WIA。

有关 WIA 体系结构的详细信息，请参阅[WIA 体系结构概述](wia-architecture-overview.md)。

 

 




