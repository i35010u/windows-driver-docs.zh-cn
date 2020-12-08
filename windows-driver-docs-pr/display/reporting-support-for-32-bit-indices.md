---
title: 报告 32 位索引支持
description: 报告 32 位索引支持
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，索引缓冲区
- 索引缓冲区 WDK Directx 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e39d3d126935e244eac9948a77eed1759400f495
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832721"
---
# <a name="reporting-support-for-32-bit-indices"></a>报告 32 位索引支持


## <span id="ddk_reporting_support_for_32_bit_indices_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_32_BIT_INDICES_GG"></span>


在 DirectX 8.0 之前，顶点索引限制为16位。 DirectX 8.0 添加了对32位索引的支持。 驱动程序通过将当前还在 [**D3DHAL \_ D3DEXTENDEDCAPS**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)) 中的 **MaxVertexIndex** (字段的值设置为大于0xffff 的值，来报告对32位索引的支持。 此字段还允许驱动程序报告该驱动程序，尽管它支持需要32位存储的索引，但它不支持完整范围的32位值。

**仅限 DirectX 9.0 和更高版本。**

 

为了使驱动程序能够通过 DirectX 9.0 接口向应用程序公开其 Direct3D 硬件抽象层 (HAL) 设备，驱动程序必须将 **MaxVertexIndex** 的值设置为大于或等于0xffff 的值。
 

