---
title: 报告 DDI 版本
description: 报告 DDI 版本
ms.assetid: f539a4b4-4652-4e40-928d-d90a3dd1988d
keywords:
- 版本号 WDK DirectX 9。0
- 报告 DDI 版本 WDK DirectX 9。0
- DDI 版本 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19560de1a3f62e2b7f728c79d900ac113c515d97
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064636"
---
# <a name="reporting-ddi-version"></a>报告 DDI 版本


## <span id="ddk_reporting_ddi_version_gg"></span><span id="DDK_REPORTING_DDI_VERSION_GG"></span>


DirectX 9.0 版本驱动程序必须报告其支持的 [DDI](direct3d-driver-ddi.md) 版本，以便 DirectX 9.0 运行时可以确定如何处理该驱动程序。 若要报告 DDI 版本，驱动程序将响应使用**GetDriverInfo2** D3DGDI2 \_ 类型 GETDDIVERSION 值的 GetDriverInfo2 请求 \_ 。 [**DD \_ GETDDIVERSIONDATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getddiversiondata)结构的**dwDXVersion**成员设置为9，指示 DirectX 9.0 运行时发出请求。

该驱动程序将 DD GETDDIVERSIONDATA 的 **dwDDIVersion** 成员设置 \_ 为它为 DirectX 9.0 运行时支持的 DDI 版本。 如果驱动程序是使用 prereleased 版本的 DirectX 9.0 驱动程序开发工具包生成的 (DDK) 在此版本中，DDI 版本号低于 DirectX 9.0 最终版本中的数字，则运行时改为将驱动程序视为 DirectX 8.0。

 

