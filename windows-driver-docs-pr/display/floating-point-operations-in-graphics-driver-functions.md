---
title: 图形驱动程序函数中的浮点运算
description: 图形驱动程序函数中的浮点运算
ms.assetid: 5f85dc0b-27c1-4fee-9a0a-cb52d5f2dae7
keywords:
- GDI WDK Windows 2000 显示，浮点操作
- 图形驱动程序 WDK Windows 2000 显示，浮点操作
- 绘制 WDK GDI，浮点操作
- 浮点运算 WDK GDI
- FPU WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3153998ff3076fd403fd2efe35556a8d3ad5b1c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065630"
---
# <a name="floating-point-operations-in-graphics-driver-functions"></a>图形驱动程序函数中的浮点运算


## <span id="ddk_floating_point_operations_in_graphics_driver_functions_gg"></span><span id="DDK_FLOATING_POINT_OPERATIONS_IN_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


如果图形驱动程序函数包含使用浮点单元 (FPU) 的代码，则必须先调用 [**EngSaveFloatingPointState**](/windows/desktop/api/winddi/nf-winddi-engsavefloatingpointstate) ，然后调用 [**EngRestoreFloatingPointState**](/windows/desktop/api/winddi/nf-winddi-engrestorefloatingpointstate)。 有关图形驱动程序功能的列表，请参阅 [图形驱动程序函数](graphics-driver-functions.md)。

如果 FPU 可用，则任何将值分配给浮点变量或执行涉及浮点数计算的代码都将使用它。 例如，以下每行代码都使用 FPU。

```cpp
double myDouble = 5;
int myInt = 5 * 4.3;
int myInt = 50 * cos(2);
```

假设您正在编写使用 FPU 的 [**DrvAlphaBlend**](/windows/desktop/api/winddi/nf-winddi-drvalphablend) 函数。 下面的示例演示了应如何保存和还原浮点状态。

```cpp
#define DRIVER_TAG // Put your driver tag here, for example 'zyxD'

BOOL DrvAlphaBlend(...)
{
   ...
   ULONG result;
 double floatVal;
   VOID* pBuf;
   ULONG bufSize;

 // Determine the size of the required buffer.
   bufSize = EngSaveFloatingPointState(NULL, 0);

 if(bufSize > 0)
   {
 // Allocate a zeroed buffer in the nonpaged pool.
      pBuf = EngAllocMem(
         FL_NONPAGED_MEMORY|FL_ZERO_MEMORY, bufSize, DRIVER_TAG);

 if(pBuf != NULL)
      {
 // The buffer was allocated successfully.
 // Save the floating-point state.
         result = EngSaveFloatingPointState(pBuf, bufSize);

 if(TRUE == result)
         {
 // The floating-point state was saved successfully.
 // Use the FPU.
            floatVal = 0.8;
            ...
            EngRestoreFloatingPointState(pBuffer);
         }

         EngFreeMem(pBuf);
      }
   }
   ...
}
```

当转义为 OPENGL [**DrvEscape**](/windows/desktop/api/winddi/nf-winddi-drvescape) \_ CMD、OPENGL \_ GETINFO 或 MCDFUNCS 时，GDI 会自动保存对驱动程序的 DrvEscape 函数的任何调用的浮点状态。 在这些情况下，可以在 *DrvEscape* 函数中使用 FPU，无需调用 **EngSaveFloatingPointState** 和 **EngRestoreFloatingPointState**。

执行浮点运算的大多数 DirectDraw 和 Direct3D 回调函数也应保存并还原浮点状态。 有关详细信息，请参阅 [在 DirectDraw 中执行浮点运算](performing-floating-point-operations-in-directdraw.md) 和 [在 Direct3D 中执行浮点运算](performing-floating-point-operations-in-direct3d.md)。

有关 GDI 提供的浮点服务的信息，请参阅 [Gdi 浮点服务](gdi-floating-point-services.md)。

 

