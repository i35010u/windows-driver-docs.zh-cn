---
title: 图面类型
description: 图面类型
ms.assetid: 7374b783-ef09-4238-a17a-fafcd9d87b3f
keywords:
- DIB WDK GDI
- 设备管理面 WDK GDI
- 引擎管理面 WDK GDI
- 图面协商 WDK GDI，图面类型
- 图面类型 WDK GDI
- 设备相关位图 WDK GDI
- DDB WDK GDI
- 与设备无关位图 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9a36f88e5be4804d74aa33ff48f5d5e94c95a81
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354209"
---
# <a name="surface-types"></a>图面类型


## <span id="ddk_surface_types_gg"></span><span id="DDK_SURFACE_TYPES_GG"></span>


可以在处理方式的上下文中查看图面类型。 存在以下类型：

-   引擎管理图面

-   设备管理图面 （标准格式位图）

-   设备管理图面 （非标准格式位图）

### <a name="span-idengine-managedsurfacesspanspan-idengine-managedsurfacesspanspan-idengine-managedsurfacesspanengine-managed-surfaces"></a><span id="Engine-Managed_Surfaces"></span><span id="engine-managed_surfaces"></span><span id="ENGINE-MANAGED_SURFACES"></span>引擎管理图面

引擎管理面：

-   创建和管理通过 GDI。

-   标准 DIB 之一与设备无关位图 (DIB) 格式创建： 自上而下，原点位于左上角中或自下而上，原点位于左下角。

-   类型 STYPE\_位图。

-   没有对应的设备的句柄图面。

标准格式位图的单平面打包像素 （其中每个像素的数据存储以连续方式） 格式的位图。 位图的每个扫描行的 4 字节边界上对齐。

在创建位图[ **EngCreateBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff564199)函数是 DIB 格式。 要对其进行管理的引擎 DIB 格式必须为位图。

### <a name="span-iddevice-managedsurfacesstandard-formatbitmapsspanspan-iddevice-managedsurfacesstandard-formatbitmapsspanspan-iddevice-managedsurfacesstandard-formatbitmapsspandevice-managed-surfaces-standard-format-bitmaps"></a><span id="Device-Managed_Surfaces__Standard-Format_Bitmaps_"></span><span id="device-managed_surfaces__standard-format_bitmaps_"></span><span id="DEVICE-MANAGED_SURFACES__STANDARD-FORMAT_BITMAPS_"></span>设备管理图面 （标准格式位图）

设备管理的面：

-   创建的设备驱动程序调用[ **DrvCreateDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff556185)函数。

-   具有关联的设备的句柄图面 (DHSURF; 有关详细信息，请参阅[ **SURFOBJ**](https://msdn.microsoft.com/library/windows/hardware/ff569901))。

-   可以是*不透明*或*nonopaque*。

一个不透明的设备管理的图面是一个为 GDI 具有既不位图格式有关的任何信息，也不引用位在位图中。 出于这些原因，该驱动程序必须支持，最低[ **DrvBitBlt**](https://msdn.microsoft.com/library/windows/hardware/ff556180)， [ **DrvTextOut**](https://msdn.microsoft.com/library/windows/hardware/ff557277)，和[ **DrvStrokePath** ](https://msdn.microsoft.com/library/windows/hardware/ff556316)函数。 此类的表面类型是 STYPE\_DEVBITMAP。

Nonopaque 的设备管理面是一个为其 GDI 位图格式有关的信息和知道位图中的位的位置。 因此，不需要实现任意绘制操作，将延迟到 GDI 的所有驱动程序。 此类的表面类型是 SYTPE\_位图。

若要将设备管理的不透明位图转换为一个 nonopaque 的驱动程序，它必须调用[ **EngModifySurface** ](https://msdn.microsoft.com/library/windows/hardware/ff564976)函数。 凭借此调用，该驱动程序告知 GDI 位图格式，在内存中的位图的位置。

当驱动程序的设备管理 DIB 图面时，该驱动程序可以回叫 GDI 要具有 GDI 绘制图面上。 管理其自己的图面，但使用的 DIB 的驱动程序仍可通过包装 DIB 引用回调到 GDI (它与在创建[ **EngCreateBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff564199)函数) 围绕其图面。 以下步骤介绍如何使该驱动程序具有 GDI 的设备管理 DIB 图面上绘制：

1.  驱动程序调用[ **EngCreateBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff564199)若要创建的 DIB 引擎管理图面。

2.  驱动程序调用[ **EngCreateDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff564204)函数来创建设备相关位图 (DDB) 面上，这是设备管理 DIB 图面。

3.  驱动程序在内部将引擎管理 DIB 数据保存在设备管理的 DDB 数据。

4.  GDI 始终调用驱动程序与设备管理的 DDB 数据通过在图面进行交互。

5.  该驱动程序时接收调用，从 GDI 和无法处理该呼叫 （例如，该驱动程序不能处理复杂的剪辑），该驱动程序检索存储在 DDB 数据并将 DIB 数据传递给 GDI 呈现的 DIB 数据。

### <a name="span-iddevice-managedsurfacesnonstandard-formatbitmapsspanspan-iddevice-managedsurfacesnonstandard-formatbitmapsspanspan-iddevice-managedsurfacesnonstandard-formatbitmapsspandevice-managed-surfaces-nonstandard-format-bitmaps"></a><span id="Device-Managed_Surfaces__Nonstandard-Format_Bitmaps_"></span><span id="device-managed_surfaces__nonstandard-format_bitmaps_"></span><span id="DEVICE-MANAGED_SURFACES__NONSTANDARD-FORMAT_BITMAPS_"></span>设备管理图面 （非标准格式位图）

驱动程序可以通过调用来启用设备管理非-DIB 面[ **EngCreateDeviceSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff564206)函数具有 GDI 创建在图面，并返回一个句柄。 GDI 依赖于驱动程序将访问控制，绘制并读取设备管理的图面中。

设备相关位图 (DDB)，这有时称为设备格式位图，是另一种类型的非-DIB，设备管理面。 DDB 支持为允许特定驱动程序，如 VGA 驱动程序，以实现更快地与屏幕位图的块传输。 DDB 还允许驱动程序要绘制到存款或非 DIB 位图屏幕外显示内存中。 如果 DDB 是必需的该驱动程序可以支持[ **DrvCreateDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff556185)函数，并调用[ **EngCreateDeviceBitmap** ](https://msdn.microsoft.com/library/windows/hardware/ff564204)函数能够返回到位图的句柄的引擎。

 

 





