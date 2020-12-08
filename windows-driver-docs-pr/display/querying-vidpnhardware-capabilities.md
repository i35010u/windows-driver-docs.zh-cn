---
title: 查询 VidPN 硬件功能
description: 查询 VidPN 硬件功能
keywords:
- VidPN WDK 显示，硬件功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f290b89c19393ab0573a45456b09528ef9b4999d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840181"
---
# <a name="querying-vidpn-hardware-capabilities"></a>查询 VidPN 硬件功能


从 Windows 7 开始，需要显示小型端口驱动程序来报告指定功能 VidPN 的所有硬件功能。 驱动程序应支持以下回调函数及其关联的结构：

-   [**DxgkDdiQueryVidPnHWCapability**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability) 函数

-   [**DXGKARG \_QUERYVIDPNHWCAPABILITY**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryvidpnhwcapability) 结构

-   [**D3DKMDT \_VIDPN \_ HW \_ 功能**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_hw_capability) 结构

当驱动程序报告硬件功能时，它应考虑克隆为隐式过程，该过程是作为旋转或缩放转换的一部分完成的：必须先克隆源，然后才能对其进行旋转或缩放。

如果 D3DKMDT \_ vidpn HW 功能的任何成员 \_ \_ 在指定的 VIDPN 路径上没有任何意义，则显示模式管理器 (call center.dmm) 如果成员设置为非零值，则不会报告任何错误。 在向用户模式客户端报告这些值之前，CALL CENTER.DMM 将清除所有此类值。 但是，驱动程序需要将 D3DKMDT VIDPN HW 功能的 **保留** 成员的值设置 \_ \_ \_ 为0。

### <a name="span-idexample_scenariospanspan-idexample_scenariospanexample-scenario"></a><span id="example_scenario"></span><span id="EXAMPLE_SCENARIO"></span>**示例方案**

若要显示显示微型端口驱动程序应如何报告硬件功能，请考虑下面的示例硬件配置 P1、P2 和 P3：

-   **P1：** 将从源 S1 克隆图面，然后旋转90度并缩放以适合目标。

-   **P2：** Surface 从源 S1 克隆，无应用转换。

-   **P3：** 源 S2 没有已应用的转换。

调用 [**DxgkDdiQueryVidPnHWCapability**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability) 时，驱动程序应根据下表返回 [**D3DKMDT \_ VIDPN \_ HW \_ 功能**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_hw_capability) 的旋转、缩放和克隆成员的值：

D3DKMDT \_ vidpn \_ HW \_ 功能硬件功能的返回值 Vidpn Path DriverRotation DriverScaling DriverCloning 硬件可以执行所有旋转、缩放和仿制转换。

P ₁

0

0

0

P ₂

0

0

0

P ₃

0

0

0

硬件可以执行除克隆以外的所有转换

P ₁

0

0

0

P ₂

0

0

1

P ₃

0

0

0

硬件可以执行克隆和缩放转换，但不能进行旋转。 驱动程序使用中间旋转 array.blit 执行旋转。

P ₁

1

0

0

P ₂

0

0

0

P ₃

0

0

0

硬件无法执行克隆、缩放或旋转转换。 这些操作由驱动程序执行。

P ₁

1

1

0

P ₂

0

0

1

P ₃

0

0

0

 

 

