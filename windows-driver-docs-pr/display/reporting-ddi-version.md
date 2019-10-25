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
ms.openlocfilehash: fa7cb45f8b85649ef8e334d8b2946f477c4e9863
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825943"
---
# <a name="reporting-ddi-version"></a>报告 DDI 版本


## <span id="ddk_reporting_ddi_version_gg"></span><span id="DDK_REPORTING_DDI_VERSION_GG"></span>


DirectX 9.0 版本驱动程序必须报告其支持的[DDI](direct3d-driver-ddi.md)版本，以便 DirectX 9.0 运行时可以确定如何处理该驱动程序。 若要报告 DDI 版本，驱动程序将响应使用 D3DGDI2\_类型\_GETDDIVERSION 值的**GetDriverInfo2**请求。 [**DD\_GETDDIVERSIONDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getddiversiondata)结构的**dwDXVersion**成员设置为9，指示 DirectX 9.0 运行时发出请求。

驱动程序将 DD\_GETDDIVERSIONDATA 的**dwDDIVersion**成员设置为 DirectX 9.0 运行时所支持的 DDI 版本。 如果驱动程序是使用 prereleased 版本的 DirectX 9.0 驱动程序开发工具包（DDK）构建的，而 DDI 版本号低于最终版本的 DirectX 9.0 中的数字，则运行时改为将驱动程序视为 DirectX 8.0。

 

 





