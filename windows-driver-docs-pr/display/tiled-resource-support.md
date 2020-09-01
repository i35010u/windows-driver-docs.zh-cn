---
title: 平铺资源支持
description: " (WDDM) 1.3 及更高版本的驱动程序，Windows 显示驱动程序模型可以支持平铺资源。 此功能是从 Windows 8.1 开始的新功能。"
ms.assetid: 02F3DFB8-2407-412A-B518-9AF4A3E1466A
ms.date: 10/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: b003bade2e8e22046674ed5f89253d6462742e7e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065986"
---
# <a name="tiled-resource-support"></a>平铺资源支持


 (WDDM) 1.3 及更高版本的驱动程序，Windows 显示驱动程序模型可以支持平铺资源。 此功能是从 Windows 8.1 开始的新功能。

以下参考主题介绍如何在用户模式显示驱动程序中实现此功能：

* [**PFND3DWDDM1_3DDI_CHECKMULTISAMPLEQUALITYLEVELS**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_checkmultisamplequalitylevels)
* [**PFND3DWDDM1_3DDI_COPYTILEMAPPINGS**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_copytilemappings)
* [**PFND3DWDDM1_3DDI_COPYTILES**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_copytiles)
* [**PFND3DWDDM1_3DDI_GETMIPPACKING**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_getmippacking)
* [**PFND3DWDDM1_3DDI_RELOCATEDEVICEFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_relocatedevicefuncs)
* [**PFND3DWDDM1_3DDI_RESIZETILEPOOL**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_resizetilepool)
* [**PFND3DWDDM1_3DDI_TILEDRESOURCEBARRIER**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_tiledresourcebarrier)
* [**PFND3DWDDM1_3DDI_UPDATETILEMAPPINGS**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_updatetilemappings)
* [**PFND3DWDDM1_3DDI_UPDATETILES**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_updatetiles)
* [**D3DWDDM1 \_ 3DDI \_ 检查 \_ 多级 \_ 多级 \_ \_ 标记**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_check_multisample_quality_levels_flag)
* [**D3DWDDM1 \_ 3DDI \_ D3D11 \_ 选项 \_ DATA1**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3dwddm1_3ddi_d3d11_options_data1)
* [**D3DWDDM1 \_ 3DDI \_ DEVICEFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3dwddm1_3ddi_devicefuncs)
* [**D3DWDDM1 \_ 3DDI \_ 磁贴 \_ 复制 \_ 标志**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_tile_copy_flag)
* [**D3DWDDM1 \_ 3DDI \_ 磁贴 \_ 映射 \_ 标志**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_tile_mapping_flag)
* [**D3DWDDM1 \_ 3DDI \_ 磁贴 \_ 范围 \_ 标志**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_tile_range_flag)
* [**D3DWDDM1 \_ 3DDI \_ 平铺 \_ 区域 \_ 大小**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3dwddm1_3ddi_tile_region_size)
* [**D3DWDDM1 \_ 3DDI \_ 平铺 \_ 资源 \_ 坐标**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3dwddm1_3ddi_tiled_resource_coordinate)
* [**D3DWDDM1 \_ 3DDI \_ 平铺 \_ 资源 \_ 支持 \_ 标志**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_tiled_resources_support_flag)
* [**D3D10 \_ 2DDICAPS \_ TYPE**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_2ddicaps_type) (**D3DWDDM1 \_ 3DDICAPS \_ D3D11 \_ OPTIONS1** 常量值) 
* [**D3D10 \_DDI \_ 筛选器**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_filter) (**D3DWDDM1 \_ 3DDI \_ FILTER \_ XXX** 常数值) 
* [**D3D10 \_DDI \_ 资源 \_ 杂项 \_ 标志**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_resource_misc_flag) (**D3DWDDM1 \_ 3DDI \_ 资源 \_ 杂项 \_ ** 平铺和 **D3DWDDM1 \_ 3DDI \_ 资源 \_ 杂项 \_ 磁贴 \_ 池** 常量值) 
* [**D3D10DDIARG \_CREATEDEVICE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice) (**pWDDM1 \_ 3DeviceFuncs** 成员) 
* [**D3D11DDIARG \_CREATEDEFERREDCONTEXT**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext) (**pWDDM1 \_ 3ContextFuncs** 成员) 

 

