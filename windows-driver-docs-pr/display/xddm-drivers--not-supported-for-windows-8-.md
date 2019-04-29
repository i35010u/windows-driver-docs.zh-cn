---
title: 不支持针对 Windows 8 的 XDDM 驱动程序
description: XDDM 驱动程序不支持针对 Windows 8，并将安装或 Windows 8 上运行。
ms.assetid: 2D527787-55AF-4D44-BBA2-8052FB594902
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8439c0f8c8b47824e386bb263c4e0f7fb3c5ccaa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388973"
---
# <a name="xddm-drivers-not-supported-for-windows-8"></a>不支持针对 Windows 8 的 XDDM 驱动程序


XDDM 驱动程序不支持针对 Windows 8，并将安装或 Windows 8 上运行。

如果将 Windows 8 中框图形驱动程序，Windows 8 将兼容的驱动程序安装 Windows 更新或 OEM/IHV 站点从 Windows 8 之前运行 MSBDD 不支持图形硬件。

**请注意**  供应商可以开发 Windows 8 兼容仅显示硬件驱动程序，如果它是一种服务器产品。

 

T*能 1 Windows 8 中的驱动程序升级体验*汇总图形驱动程序迁移行为了 Windows 8 升级过程并清理安装。 在此表中， *ITB* = 中框和*OTB* =-现成的; 这是 OEM 或 IHV 零售驱动程序包或 Windows 更新包。

**表 1 Windows 8 中的驱动程序升级体验**

| 在 Windows 7 中使用的驱动程序                                       | 应用场景 | Windows 8 中框覆盖率 | 在 Windows 8 中的生成初始驱动程序 |
|----------------------------------------------------------------|----------|---------------------------|---------------------------------------|
| Win7 OTB 驱动程序 / Win7 ITB 驱动程序 / 没有驱动程序 / XDDM 驱动程序    | 升级  | ITB 驱动程序支持        | Win8 ITB 驱动程序                       |
| Win7 OTB 驱动程序                                                | 升级  | 没有 ITB 驱动程序支持     | Win7 OTB 驱动程序                       |
| Win7 ITB 驱动程序 / 没有驱动程序阻塞 OTB 驱动程序 / XDDM 驱动程序 | 升级  | 没有 ITB 驱动程序支持     | Win8 MSBDD                            |
| 不可用                                                            | clean    | ITB 驱动程序支持        | Win8 ITB 驱动程序                       |
| 不可用                                                            | clean    | 没有 ITB 驱动程序支持     | Win8 MSBDD                            |

 

在 Windows 7 图形驱动程序本身不迁移到哪里的情况下，任何 IHV 或 OEM 值-将添加 Windows 8 升级安装后可以保留从 Windows 7 图形的驱动程序包，例如控制面板和 OpenGL 支持库的组件。 这是因为 Windows 8 安装程序无法知道这些值的添加组件将与 Windows 7 零售或 OEM 驱动程序包相关联。 这些值-添加组件可能无法正常工作中不存在其驱动程序包的其余部分。

Ihv 应强化这些值添加组件只需在这种情况下退出。 在其中增值会导致问题的少数情况下，特定于值-添加组件可以阻止迁移通过 Microsoft 兼容性团队。 在某些情况下，IHV 的 Windows 8 中现成驱动程序中删除值添加升级的组件。 这是最 IHV 多。

有意将一些零售和 OEM Windows 7 图形驱动程序结构以防止其在 Windows 8 上的安装。 Windows 8 可能会尝试将迁移此类驱动程序根据上述规则，但它将无法在 Windows 8，导致使用 MSBDD 上安装。

IHV 可以创建为 WDDM 1.2 驱动程序在 Windows 8 中，但这看上去像 WDDM 1.1 或 1.0 驱动程序上以前 Windows 版本的统一的驱动程序包。

 

 





