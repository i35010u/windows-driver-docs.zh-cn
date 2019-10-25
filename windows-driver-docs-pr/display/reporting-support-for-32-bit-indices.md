---
title: 报告 32 位索引支持
description: 报告 32 位索引支持
ms.assetid: e9ea5f0e-9b95-4671-a947-55692eca8902
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，索引缓冲区
- 索引缓冲区 WDK Directx 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8708676d8110702118d4275eb59ece7a38440bce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829591"
---
# <a name="reporting-support-for-32-bit-indices"></a>报告 32 位索引支持


## <span id="ddk_reporting_support_for_32_bit_indices_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_32_BIT_INDICES_GG"></span>


在 DirectX 8.0 之前，顶点索引限制为16位。 DirectX 8.0 添加了对32位索引的支持。 驱动程序通过将 D3DCAPS8 的**MaxVertexIndex**字段的值（当前也在[**D3DHAL\_D3DEXTENDEDCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)中）设置为大于0xffff 的值来报告对32位索引的支持。 此字段还允许驱动程序报告该驱动程序，尽管它支持需要32位存储的索引，但它不支持完整范围的32位值。

**仅限 DirectX 9.0 和更高版本。**

 

为了使驱动程序能够通过 DirectX 9.0 接口向应用程序公开其 Direct3D 硬件抽象层（HAL）设备，驱动程序必须将**MaxVertexIndex**的值设置为大于或等于0xffff 的值。
 

 





