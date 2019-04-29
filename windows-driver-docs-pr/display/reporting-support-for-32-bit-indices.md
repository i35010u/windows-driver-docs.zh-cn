---
title: 报告 32 位索引支持
description: 报告 32 位索引支持
ms.assetid: e9ea5f0e-9b95-4671-a947-55692eca8902
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示、 索引缓冲区
- 索引缓冲区 WDK Directx 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8db61dd470f7d506a94ed0242544809ae0f89bcf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383253"
---
# <a name="reporting-support-for-32-bit-indices"></a>报告 32 位索引支持


## <span id="ddk_reporting_support_for_32_bit_indices_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_32_BIT_INDICES_GG"></span>


之前 DirectX 8.0 顶点索引是限制为 16 位数量。 DirectX 8.0 将添加对 32 位索引的支持。 驱动程序报告的值设置为 32 位索引的支持**MaxVertexIndex** D3DCAPS8 字段 (当前还在[ **D3DHAL\_D3DEXTENDEDCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff544753)) 到大于 0xFFFF 的值。 此字段还允许驱动程序添加到，虽然它支持需要 32 位的存储的索引，但是它不支持 32 位值的完整范围的报表。

**DirectX 9.0 和更高版本。**

 

为了使驱动程序来公开其 Direct3D 硬件抽象层 (HAL) 设备如何通过 DirectX 9.0 接口应用程序，该驱动程序必须设置的值**MaxVertexIndex**为大于或等于 0xFFFF 的值。
 

 





