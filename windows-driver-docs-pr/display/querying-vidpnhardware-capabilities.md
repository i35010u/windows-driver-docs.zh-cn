---
title: 查询 VidPN 硬件功能
description: 查询 VidPN 硬件功能
ms.assetid: fb7939bb-ff7e-4ba8-b801-ac10010c44b7
keywords:
- VidPN WDK 显示，硬件功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88bb6f4c110daa46412ae973c8ca82ebdae27849
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385044"
---
# <a name="querying-vidpn-hardware-capabilities"></a>查询 VidPN 硬件功能


从 Windows 7 开始，显示微型端口驱动程序所需报告的指定功能 VidPN 的所有硬件功能。 驱动程序应支持以下的回调函数和其关联的结构：

-   [**DxgkDdiQueryVidPnHWCapability** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability)函数

-   [**DXGKARG\_QUERYVIDPNHWCAPABILITY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_queryvidpnhwcapability)结构

-   [**D3DKMDT\_VIDPN\_HW\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_hw_capability)结构

当驱动程序报告的硬件功能时，应考虑克隆一个隐式过程，都将作为一部分旋转或缩放转换： 旋转或缩放之前，必须先克隆源。

如果任何成员 D3DKMDT\_VIDPN\_HW\_功能指定 VidPN 路径上没有任何意义，如果成员设置为非零值，显示模式下管理器 (DMM) 不会报告任何错误。 DMM 将它们报告给用户模式下客户端之前清除所有此类值。 但是，该驱动程序需要的值设置**保留**D3DKMDT 成员\_VIDPN\_HW\_为 0 的功能。

### <a name="span-idexamplescenariospanspan-idexamplescenariospanexample-scenario"></a><span id="example_scenario"></span><span id="EXAMPLE_SCENARIO"></span>**示例方案**

若要显示显示微型端口驱动程序报告的硬件功能的方式，请考虑下面的示例将一 P1、 P2 和 P3 的硬件配置：

-   **P1:** 图面是从源 S1 克隆、 然后旋转 90 度和缩放以适合目标。

-   **P2:** 图面进行克隆源 S1，与任何应用转换。

-   **P3:** 源 S2 有任何已应用的转换。

当[ **DxgkDdiQueryVidPnHWCapability** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_queryvidpnhwcapability)是调用，则驱动程序应返回旋转、 缩放和克隆的成员的值[ **D3DKMDT\_VIDPN\_HW\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_hw_capability)根据下表：

D3DKMDT 成员的返回值\_VIDPN\_HW\_功能的硬件功能 VidPN 路径 DriverRotation DriverScaling DriverCloning 硬件可以执行所有旋转、 缩放和克隆的转换。

P₁

0

0

0

P₂

0

0

0

P₃

0

0

0

硬件可以执行所有转换除外克隆

P₁

0

0

0

P₂

0

0

1

P₃

0

0

0

硬件可以执行克隆和缩放转换，但不是旋转。 驱动程序执行使用中间旋转位块旋转。

P₁

1

0

0

P₂

0

0

0

P₃

0

0

0

硬件不能执行克隆、 缩放或旋转转换。 驱动程序执行这些操作。

P₁

1

1

0

P₂

0

0

1

P₃

0

0

0

 

 

 





