---
title: Microsoft STI 和 Microsoft WIA 概述
description: Microsoft STI 和 Microsoft WIA 概述
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 649ecba5b71bf009e2180446f719d22d664f10e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841101"
---
# <a name="overview-of-microsoft-sti-and-microsoft-wia"></a>Microsoft STI 和 Microsoft WIA 概述

旧版 Windows 操作系统中的映像体系结构由低级别硬件抽象、STI 以及一组称为 TWAIN 的高级 Api 组成。 在新式 Windows 操作系统中，Microsoft 使用 (WIA) 的 Windows 映像体系结构，该体系结构是在 STI 上构建的。 下图演示了这两种图像处理体系结构。

![阐释 twain/sti 和 microsoft wia 图像体系结构的示意图](images/sti-wia.png)

如上图所示，TWAIN/STI 体系结构包括 TWAIN、一组高级的映像采集 Api 以及 STI （一种低级别硬件抽象）。 WIA 体系结构将 STI 作为基础，为映像设备 Ihv 提供完整的解决方案。

### <a name="differences-between-sti-and-wia"></a>STI 和 WIA 之间的差异

WIA 驱动程序建立在 STI 所提供的基础之上，因此除了自身之外，还公开了 STI 接口。 WIA 驱动程序至少必须公开 **IStiUSD** 接口。 STI 在任何 WIA 接口上没有对应的依赖项。 由于 WIA 微型驱动程序必须符合 STI 微型驱动程序，因此可以只编写一个 STI 微型驱动程序，使支持 WIA 的照相机或扫描仪成为 STI 图像设备。 但是，建议使用 WIA 以获得更好的用户体验。 例如，照相机的 STI 驱动程序不会在资源管理器中显示缩略图。

STI 和 WIA 之间的一些差异包括：

-   STI 在客户端应用程序进程和系统服务进程中运行;WIA 仅在系统服务进程中运行。

-   STI 是一种低级别硬件抽象，必须具有有关设备的详细信息，才能操作;WIA 可以在没有此类详细设备信息的情况下运行。

-   STI 不是完整的映像界面;WIA 是在 STI 的基础上构建的，它是映像 Ihv 的完整解决方案。 IHV 提供的 UI 模块 (例如 Twain、) 在 STI 体系结构中是必需的，因为它只有设备通信机制，并且没有 UI 前端。 WIA 微型驱动程序不需要自己的 UI 模块，因为)  (扫描仪和照相机向导的默认 UI。 此外，通过 WIA 体系结构中的 TWAIN 兼容层支持 Twain 接口。 Ihv 可以在 WIA 中扩展或替换这些默认的 Ui。

有关 WIA 体系结构的详细信息，请参阅 [WIA 体系结构概述](wia-architecture-overview.md)。

 

 




