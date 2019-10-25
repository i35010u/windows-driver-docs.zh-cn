---
title: 查询 VidPN 硬件功能
description: 查询 VidPN 硬件功能
ms.assetid: fb7939bb-ff7e-4ba8-b801-ac10010c44b7
keywords:
- VidPN WDK 显示，硬件功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8c9aafe2bb105868b05234a0491697907348aa2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825957"
---
# <a name="querying-vidpn-hardware-capabilities"></a>查询 VidPN 硬件功能


从 Windows 7 开始，需要显示小型端口驱动程序来报告指定功能 VidPN 的所有硬件功能。 驱动程序应支持以下回调函数及其关联的结构：

-   [**DxgkDdiQueryVidPnHWCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability)函数

-   [**DXGKARG\_QUERYVIDPNHWCAPABILITY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryvidpnhwcapability)结构

-   [**D3DKMDT\_VIDPN\_HW\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_hw_capability)结构

当驱动程序报告硬件功能时，它应考虑克隆为隐式过程，该过程是作为旋转或缩放转换的一部分完成的：必须先克隆源，然后才能对其进行旋转或缩放。

如果 D3DKMDT 的任何成员\_VIDPN\_HW\_功能在指定的 VidPN 路径上没有意义，则如果成员设置为非零值，则显示模式管理器（CALL CENTER.DMM）不会报告任何错误。 在向用户模式客户端报告这些值之前，CALL CENTER.DMM 将清除所有此类值。 但是，驱动程序需要将 D3DKMDT\_VIDPN\_HW\_功能的**保留**成员的值设置为0。

### <a name="span-idexample_scenariospanspan-idexample_scenariospanexample-scenario"></a><span id="example_scenario"></span><span id="EXAMPLE_SCENARIO"></span>**示例方案**

若要显示显示微型端口驱动程序应如何报告硬件功能，请考虑下面的示例硬件配置 P1、P2 和 P3：

-   **P1：** 将从源 S1 克隆图面，然后旋转90度并缩放以适合目标。

-   **P2：** Surface 从源 S1 克隆，无应用转换。

-   **P3：** 源 S2 没有已应用的转换。

调用[**DxgkDdiQueryVidPnHWCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability)时，驱动程序应根据下表返回[**D3DKMDT\_VIDPN\_HW\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_hw_capability)的旋转、缩放和克隆成员的值：

D3DKMDT 的成员的返回值\_VIDPN\_HW\_功能硬件功能 VidPN 路径 DriverRotation DriverScaling DriverCloning 硬件可以执行所有旋转、缩放和克隆转换。

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

 

 

 





