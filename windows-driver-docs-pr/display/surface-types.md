---
title: 图面类型
description: 图面类型
ms.assetid: 7374b783-ef09-4238-a17a-fafcd9d87b3f
keywords:
- DIB WDK GDI
- 设备管理的表面 WDK GDI
- 引擎管理的平面 WDK GDI
- surface 协商 WDK GDI，表面类型
- 表面类型 WDK GDI
- 与设备相关的位图 WDK GDI
- DDB WDK GDI
- 与设备无关的位图 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b1f4221a71c7422157a9b3bfa6580791f737d24
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066558"
---
# <a name="surface-types"></a>图面类型


## <span id="ddk_surface_types_gg"></span><span id="DDK_SURFACE_TYPES_GG"></span>


可以在处理它们的方式的上下文中查看表面类型。 存在以下类型：

-   引擎管理的图面

-   设备管理的图面 (标准格式位图) 

-   设备管理的图面 (非标准格式位图) 

### <a name="span-idengine-managed_surfacesspanspan-idengine-managed_surfacesspanspan-idengine-managed_surfacesspanengine-managed-surfaces"></a><span id="Engine-Managed_Surfaces"></span><span id="engine-managed_surfaces"></span><span id="ENGINE-MANAGED_SURFACES"></span>引擎管理的图面

引擎管理的图面：

-   由 GDI 创建和管理。

-   创建为与设备无关的位图 (DIB) 采用标准 DIB 格式之一：自顶向下，其中原点位于左上角，或靠下，原点在左下角，原点位于左上角。

-   的类型为 s \_ 位图。

-   没有对应的设备句柄。

标准格式位图是一种单平面的压缩像素 (，其中每个像素的数据按) 格式位图的连续方式存储。 位图的每个扫描行都按四字节边界对齐。

在 [**EngCreateBitmap**](/windows/desktop/api/winddi/nf-winddi-engcreatebitmap) 函数中创建的位图采用 DIB 格式。 位图必须为 DIB 格式，引擎才能对其进行管理。

### <a name="span-iddevice-managed_surfaces__standard-format_bitmaps_spanspan-iddevice-managed_surfaces__standard-format_bitmaps_spanspan-iddevice-managed_surfaces__standard-format_bitmaps_spandevice-managed-surfaces-standard-format-bitmaps"></a><span id="Device-Managed_Surfaces__Standard-Format_Bitmaps_"></span><span id="device-managed_surfaces__standard-format_bitmaps_"></span><span id="DEVICE-MANAGED_SURFACES__STANDARD-FORMAT_BITMAPS_"></span>设备管理的图面 (标准格式位图) 

设备管理的图面：

-   是通过调用设备驱动程序的 [**DrvCreateDeviceBitmap**](/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap) 函数创建的。

-   具有关联的设备句柄到 surface (DHSURF;有关详细信息，请参阅 [**SURFOBJ**](/windows/desktop/api/winddi/ns-winddi-_surfobj)) 。

-   可以是不 *透明* 的，也可以是 *nonopaque*。

不透明的设备管理的图面是 GDI 既不包含有关位图格式的任何信息，也不包含对位图中的位的引用。 由于这些原因，驱动程序必须至少支持 [**DrvBitBlt**](/windows/desktop/api/winddi/nf-winddi-drvbitblt)、 [**DrvTextOut**](/windows/desktop/api/winddi/nf-winddi-drvtextout)和 [**DrvStrokePath**](/windows/desktop/api/winddi/nf-winddi-drvstrokepath) 函数。 此类图面的类型为 s \_ DEVBITMAP。

Nonopaque 设备管理的图面是 GDI 包含有关位图格式的信息并知道位在位图中的位置。 因此，该驱动程序不需要实现任何绘图操作，而是将所有绘图操作都延迟为 GDI。 此类图面的类型为 SYTPE \_ 位图。

若要使驱动程序将设备托管的不透明位图转换为 nonopaque 的，它必须调用 [**EngModifySurface**](/windows/desktop/api/winddi/nf-winddi-engmodifysurface) 函数。 通过此调用，驱动程序将在内存中通知位图格式和位图位置的 GDI。

当驱动程序具有设备托管的 DIB 图面时，驱动程序可以回调到 GDI 以便在表面上绘制 GDI。 如果驱动程序管理自己的图面，但使用的是 DIB，则仍可通过使用 [**EngCreateBitmap**](/windows/desktop/api/winddi/nf-winddi-engcreatebitmap) 函数) 围绕其图面创建的 dib (来引用 GDI。 以下步骤介绍了驱动程序如何在设备托管的 DIB 表面上进行 GDI 绘制：

1.  驱动程序调用 [**EngCreateBitmap**](/windows/desktop/api/winddi/nf-winddi-engcreatebitmap) 来创建 DIB 引擎管理的图面。

2.  驱动程序调用 [**EngCreateDeviceBitmap**](/windows/desktop/api/winddi/nf-winddi-engcreatedevicebitmap) 函数来创建与设备相关的位图 (DDB) 图面，该图面是设备托管的 DIB 表面。

3.  驱动程序在内部将引擎托管的 DIB 数据保存在设备托管的 DDB 数据中。

4.  GDI 始终调用驱动程序，通过设备托管的 DDB 数据与表面交互。

5.  当驱动程序收到来自 GDI 的调用并且无法处理调用 (例如，驱动程序无法处理复杂的剪辑) ，驱动程序将检索存储在 DDB 数据中的 DIB 数据，并将 DIB 数据传递给 GDI 以呈现。

### <a name="span-iddevice-managed_surfaces__nonstandard-format_bitmaps_spanspan-iddevice-managed_surfaces__nonstandard-format_bitmaps_spanspan-iddevice-managed_surfaces__nonstandard-format_bitmaps_spandevice-managed-surfaces-nonstandard-format-bitmaps"></a><span id="Device-Managed_Surfaces__Nonstandard-Format_Bitmaps_"></span><span id="device-managed_surfaces__nonstandard-format_bitmaps_"></span><span id="DEVICE-MANAGED_SURFACES__NONSTANDARD-FORMAT_BITMAPS_"></span>设备管理的图面 (非标准格式位图) 

驱动程序可以通过调用 [**EngCreateDeviceSurface**](/windows/desktop/api/winddi/nf-winddi-engcreatedevicesurface) 函数来启用设备托管的非 DIB 表面，使 GDI 创建该图面并向其返回一个句柄。 GDI 依赖于驱动程序来访问、控制绘图并从设备管理的表面进行读取。

与设备相关的位图 (DDB) ，有时称为设备格式的位图，是另一种非 DIB、设备管理的图面。 支持该 DDB 来实现某些驱动程序（如 VGA 驱动程序），以实现更快的位图到屏幕块传输。 DDB 还允许驱动程序在屏幕外显示内存中，将其绘制到存款或非 DIB 位图。 如果需要使用 DDB，驱动程序可以支持 [**DrvCreateDeviceBitmap**](/windows/desktop/api/winddi/nf-winddi-drvcreatedevicebitmap) 函数，并调用 [**EngCreateDeviceBitmap**](/windows/desktop/api/winddi/nf-winddi-engcreatedevicebitmap) 函数使引擎返回位图的句柄。

 

