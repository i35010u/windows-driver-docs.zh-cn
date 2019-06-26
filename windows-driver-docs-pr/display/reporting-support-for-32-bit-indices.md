---
title: 报告 32 位索引支持
description: 报告 32 位索引支持
ms.assetid: e9ea5f0e-9b95-4671-a947-55692eca8902
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示、 索引缓冲区
- 索引缓冲区 WDK Directx 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 065ad0f4ab916fb6af9dec769bddccd8140d84d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369276"
---
# <a name="reporting-support-for-32-bit-indices"></a>报告 32 位索引支持


## <span id="ddk_reporting_support_for_32_bit_indices_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_32_BIT_INDICES_GG"></span>


之前 DirectX 8.0 顶点索引是限制为 16 位数量。 DirectX 8.0 将添加对 32 位索引的支持。 驱动程序报告的值设置为 32 位索引的支持**MaxVertexIndex** D3DCAPS8 字段 (当前还在[ **D3DHAL\_D3DEXTENDEDCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)) 到大于 0xFFFF 的值。 此字段还允许驱动程序添加到，虽然它支持需要 32 位的存储的索引，但是它不支持 32 位值的完整范围的报表。

**DirectX 9.0 和更高版本。**

 

为了使驱动程序来公开其 Direct3D 硬件抽象层 (HAL) 设备如何通过 DirectX 9.0 接口应用程序，该驱动程序必须设置的值**MaxVertexIndex**为大于或等于 0xFFFF 的值。
 

 





