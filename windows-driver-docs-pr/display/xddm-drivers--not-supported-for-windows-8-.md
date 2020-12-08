---
title: Windows 8 不支持 XDDM 驱动程序
description: Windows 8 不支持 XDDM 驱动程序，并且不会在 Windows 8 上安装或运行。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22736172b9a65de8bcc6bd02b31d787eb47de836
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818505"
---
# <a name="xddm-drivers-not-supported-for-windows-8"></a>Windows 8 不支持 XDDM 驱动程序


Windows 8 不支持 XDDM 驱动程序，并且不会在 Windows 8 上安装或运行。

如果 Windows 8 内置图形驱动程序不支持图形硬件，Windows 8 将运行 MSBDD，直到从 Windows 更新或 OEM/IHV 站点安装 Windows 8 兼容的驱动程序。

**注意**  
如果设备是服务器产品，则供应商可以为硬件开发仅适用于 Windows 8 的显示驱动程序。

 

*Windows 8 中的第1个驱动程序升级体验在* windows 8 升级和全新安装期间汇总了图形驱动程序迁移行为。 在此表中， *ITB* = 内置和 *OTB* = 开箱即用;这是一个 OEM 或 IHV 零售驱动程序包，或 Windows 更新包。

**表 1 Windows 8 中的驱动程序升级体验**

| Windows 7 中使用的驱动程序                                       | 方案 | Windows 8 机箱内覆盖面 | Windows 8 中生成的初始驱动程序 |
|----------------------------------------------------------------|----------|---------------------------|---------------------------------------|
| Win7 OTB 驱动程序/Win7 ITB 驱动程序/无驱动程序/XDDM 驱动程序    | 升级  | ITB 驱动程序支持        | Win8 ITB 驱动程序                       |
| Win7 OTB 驱动程序                                                | 升级  | 无 ITB 驱动程序支持     | Win7 OTB 驱动程序                       |
| Win7 ITB 驱动程序/No 驱动程序/阻止的 OTB 驱动程序/XDDM 驱动程序 | 升级  | 无 ITB 驱动程序支持     | Win8 MSBDD                            |
| 空值                                                            | clean    | ITB 驱动程序支持        | Win8 ITB 驱动程序                       |
| 空值                                                            | clean    | 无 ITB 驱动程序支持     | Win8 MSBDD                            |

 

在 Windows 7 图形驱动程序本身未迁移的情况下，windows 7 图形驱动程序包中的任何 IHV 或 OEM 值添加组件（例如，控制面板和 OpenGL 支持库）都可以在安装 Windows 8 后保存。 出现这种情况的原因是 Windows 8 安装程序无法知道这些值添加组件与 Windows 7 零售版或 OEM 驱动程序包相关联。 如果缺少驱动程序包的其余部分，则这些值添加组件可能无法正常工作。

在这种情况下，Ihv 应强制实施这些值添加组件。 在出现值添加导致问题的罕见情况下，Microsoft 兼容性团队可能会阻止特定的值添加组件迁移。 在某些情况下，IHV 的 Windows 8 内置驱动程序将删除升级时的值添加组件。 这取决于 IHV。

某些零售和 OEM Windows 7 图形驱动程序是特意构建的，以防止在 Windows 8 上安装。 Windows 8 可能会尝试根据上述规则迁移此类驱动程序，但它将无法在 Windows 8 上安装，从而导致使用 MSBDD。

IHV 可以在 Windows 8 上创建作为 WDDM 1.2 驱动程序的统一驱动程序包，但在以前的 Windows 版本中，该驱动程序似乎类似于 WDDM 1.1 或1.0 驱动程序。

 

 





