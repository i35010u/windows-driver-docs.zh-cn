---
title: AGP 类型孔径空间段
description: AGP 类型孔径空间段
ms.assetid: a531f79e-541a-4454-8337-19a99aa046ae
keywords:
- 内存段 WDK 显示 AGP 类型 aperture 空间段
- AGP 类型 aperture 空间段 WDK 显示
- aperture 空间段 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bd9394c6548d497e3f467437b618217e3ceea79
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565985"
---
# <a name="agp-type-aperture-space-segments"></a>AGP 类型孔径空间段


## <span id="ddk_agp_type_aperture_space_segments_gg"></span><span id="DDK_AGP_TYPE_APERTURE_SPACE_SEGMENTS_GG"></span>


AGP 类型 aperture 空间段是类似于线性 aperture 空间段;但是，显示微型端口驱动程序不会公开 DXGK\_操作\_地图\_APERTURE\_段和 DXGK\_操作\_UNMAP\_APERTURE\_段操作类型的[ **DxgkDdiBuildPagingBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff559587) AGP 类型 aperture 空间段通过回调函数。 视频内存管理器而是使用 GART 驱动程序映射和取消映射系统页 （即，视频内存管理器不涉及显示微型端口驱动程序）。

该驱动程序必须设置**Agp**中的位域标志**标志**的成员[ **DXGK\_SEGMENTDESCRIPTOR** ](https://msdn.microsoft.com/library/windows/hardware/ff562035)结构若要指定 AGP 类型 aperture 空间段。

 

 





