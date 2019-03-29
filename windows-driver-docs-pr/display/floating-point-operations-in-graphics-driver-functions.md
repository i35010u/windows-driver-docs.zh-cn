---
title: 图形驱动程序函数中的浮点运算
description: 图形驱动程序函数中的浮点运算
ms.assetid: 5f85dc0b-27c1-4fee-9a0a-cb52d5f2dae7
keywords:
- GDI WDK Windows 2000 显示，浮点运算
- 图形驱动程序 WDK Windows 2000 显示，浮点运算
- 绘制 WDK GDI，浮点运算
- 浮点运算 WDK GDI
- FPU WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46ea99e3f760b67aeef21a21517d4eb3ca8779b7
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348970"
---
# <a name="floating-point-operations-in-graphics-driver-functions"></a>图形驱动程序函数中的浮点运算


## <span id="ddk_floating_point_operations_in_graphics_driver_functions_gg"></span><span id="DDK_FLOATING_POINT_OPERATIONS_IN_GRAPHICS_DRIVER_FUNCTIONS_GG"></span>


如果图形驱动程序函数包含使用浮点单元 (FPU) 的代码，必须通过调用前面的代码[ **EngSaveFloatingPointState** ](https://msdn.microsoft.com/library/windows/hardware/ff565010)并调用后跟[ **EngRestoreFloatingPointState**](https://msdn.microsoft.com/library/windows/hardware/ff565006)。 图形驱动程序函数的列表，请参阅[图形驱动程序函数](graphics-driver-functions.md)。

如果 FPU 不可用，它将使用的任何代码，它将值分配给浮点变量或执行计算时如果涉及浮点数。 例如，以下代码行的每个使用 FPU。

```cpp
double myDouble = 5;
int myInt = 5 * 4.3;
int myInt = 50 * cos(2);
```

假设您要编写[ **DrvAlphaBlend** ](https://msdn.microsoft.com/library/windows/hardware/ff556176)使用 FPU 函数。 下面的示例演示如何应保存和还原的浮点状态。

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

GDI，将自动保存对驱动程序的任何调用的浮点状态[ **DrvEscape** ](https://msdn.microsoft.com/library/windows/hardware/ff556217)函数时转义符，OPENGL\_CMD、 OPENGL\_GETINFO 或 MCDFUNCS。 在这些情况下，你可以使用在 FPU 你*DrvEscape*而无需调用函数**EngSaveFloatingPointState**并**EngRestoreFloatingPointState**。

大多数 DirectDraw 和 Direct3D 执行浮点操作的回调函数还应保存和还原的浮点状态。 有关详细信息，请参阅[DirectDraw 中执行浮点操作](performing-floating-point-operations-in-directdraw.md)并[Direct3D 中执行浮点操作](performing-floating-point-operations-in-direct3d.md)。

提供的 GDI 的浮点服务的信息，请参阅[GDI 浮点服务](gdi-floating-point-services.md)。

 

 





