---
title: 平铺资源支持
description: Windows 显示驱动程序模型（WDDM）1.3 和更高版本的驱动程序可以支持平铺资源。 此功能是从 Windows 8.1 开始的新功能。
ms.assetid: 02F3DFB8-2407-412A-B518-9AF4A3E1466A
ms.date: 10/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 54c29ba8b6bb085a0ff466cb2c2d55470968c2d0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825454"
---
# <a name="tiled-resource-support"></a>平铺资源支持


Windows 显示驱动程序模型（WDDM）1.3 和更高版本的驱动程序可以支持平铺资源。 此功能是从 Windows 8.1 开始的新功能。

以下参考主题介绍如何在用户模式显示驱动程序中实现此功能：

* [**PFND3DWDDM1_3DDI_CHECKMULTISAMPLEQUALITYLEVELS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_checkmultisamplequalitylevels)
* [**PFND3DWDDM1_3DDI_COPYTILEMAPPINGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_copytilemappings)
* [**PFND3DWDDM1_3DDI_COPYTILES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_copytiles)
* [**PFND3DWDDM1_3DDI_GETMIPPACKING**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_getmippacking)
* [**PFND3DWDDM1_3DDI_RELOCATEDEVICEFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_relocatedevicefuncs)
* [**PFND3DWDDM1_3DDI_RESIZETILEPOOL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_resizetilepool)
* [**PFND3DWDDM1_3DDI_TILEDRESOURCEBARRIER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_tiledresourcebarrier)
* [**PFND3DWDDM1_3DDI_UPDATETILEMAPPINGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_updatetilemappings)
* [**PFND3DWDDM1_3DDI_UPDATETILES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3dwddm1_3ddi_updatetiles)
* [**D3DWDDM1\_3DDI\_检查\_多级采样\_质量\_\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_check_multisample_quality_levels_flag)
* [**D3DWDDM1\_3DDI\_D3D11\_选项\_DATA1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3dwddm1_3ddi_d3d11_options_data1)
* [**D3DWDDM1\_3DDI\_DEVICEFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3dwddm1_3ddi_devicefuncs)
* [**D3DWDDM1\_3DDI\_磁贴\_复制\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_tile_copy_flag)
* [**D3DWDDM1\_3DDI\_磁贴\_映射\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_tile_mapping_flag)
* [**D3DWDDM1\_3DDI\_磁贴\_范围\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_tile_range_flag)
* [**D3DWDDM1\_3DDI\_\_区域\_大小**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3dwddm1_3ddi_tile_region_size)
* [**D3DWDDM1\_3DDI\_平铺\_资源\_坐标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3dwddm1_3ddi_tiled_resource_coordinate)
* [**D3DWDDM1\_3DDI\_平铺\_资源\_支持\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3dwddm1_3ddi_tiled_resources_support_flag)
* [**D3D10\_2DDICAPS\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_2ddicaps_type)（**D3DWDDM1\_3DDICAPS\_D3D11\_OPTIONS1**常量值）
* [**D3D10\_DDI\_filter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_filter) （**D3DWDDM1\_3DDI\_FILTER\_XXX**常数值）
* [**D3D10\_DDI\_资源\_杂项\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_resource_misc_flag)（**D3DWDDM1\_3DDI\_资源\_杂项\_平铺**和**D3DWDDM1\_3DDI\_资源\_杂项\_磁贴\_池**常数值）
* [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice) （**pWDDM1\_3DeviceFuncs**成员）
* [**D3D11DDIARG\_CREATEDEFERREDCONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext) （**pWDDM1\_3ContextFuncs**成员）

 

 





