---
title: 驱动程序初始化和清理
description: 驱动程序初始化和清理
ms.assetid: 57f22818-a298-4f9a-87a6-5ca4d97bf32b
keywords:
- 绘制 WDK GDI，初始化，说明
- 初始化图形驱动程序 WDK Windows 2000 显示、描述
- GDI WDK Windows 2000 显示、初始化、描述
- 图形驱动程序 WDK Windows 2000 显示、初始化、描述
- DrvEnableDriver
- 绘制 WDK GDI，清理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32c067316a38f09b35fc5b6f5d6d6efce727f394
ms.sourcegitcommit: abe7fe9f3fbee8d12641433eeab623a4148ffed3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92185232"
---
# <a name="driver-initialization-and-cleanup"></a>驱动程序初始化和清理

尽管设备驱动程序可以实现多个或多个函数，但它仅将 [**DrvEnableDriver**](/windows/win32/api/winddi/nf-winddi-drvenabledriver) 导出到 GDI。 驱动程序通过函数表公开其他支持的函数。 第一次调用 GDI 向 **DrvEnableDriver** 函数发出设备驱动程序。 在此函数中，驱动程序将填充传入的 [**DRVENABLEDATA**](/windows/win32/api/winddi/ns-winddi-drvenabledata) 结构，使 GDI 可以确定支持哪些其他 *DrvXxx* 函数以及它们所在的位置。 驱动程序在 DRVENABLEDATA 中提供以下信息：

* **IDriverVersion**成员包含特定 Windows 操作系统版本的图形 DDI 版本号。 *Winddi*标头定义以下常量：

   | 返回的常量 | 操作系统版本 |
   | -------- | ------------------------ |
   | DDI_DRIVER_VERSION_NT4 | Windows NT 4.0 |
   | DDI_DRIVER_VERSION_NT5 | Windows 2000 |
   | DDI_DRIVER_VERSION_NT5_01 | Windows XP |

   有关如何使用这些常量的详细信息，请参阅 [**DRVENABLEDATA**](/windows/win32/api/winddi/ns-winddi-drvenabledata)。

* **C**成员包含数组中的 DRVFN 结构数。

* **Pdrvfn**成员指向[**DRVFN**](/windows/win32/api/winddi/ns-winddi-drvfn)结构的数组，其中列出了支持的函数及其索引。

对于 GDI 若要调用除驱动程序的 enable 和 disable 函数之外的其他函数，驱动程序必须使该函数的名称和位置对 GDI 可用。

尽管 [**DrvEnableDriver**](/windows/win32/api/winddi/nf-winddi-drvenabledriver) 也可以执行一次性初始化（如分配信号量），但驱动程序在 **DrvEnableDriver**期间不应实际启用硬件。 硬件初始化应该出现在驱动程序的 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) 函数中。 同样，驱动程序应在 [**DrvEnableSurface**](/windows/win32/api/winddi/nf-winddi-drvenablesurface) 函数中启用该图面。

GDI 将调用 [**DrvDisableDriver**](/windows/win32/api/winddi/nf-winddi-drvdisabledriver) 函数以通知驱动程序即将卸载。 为了响应此调用，驱动程序此时应释放驱动程序仍分配的所有资源和内存。

如果需要重置硬件，则 GDI 将调用驱动程序的 [**DrvAssertMode**](/windows/win32/api/winddi/nf-winddi-drvassertmode) 函数。
