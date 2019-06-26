---
title: 报告 DDI 版本
description: 报告 DDI 版本
ms.assetid: f539a4b4-4652-4e40-928d-d90a3dd1988d
keywords:
- 版本号 WDK DirectX 9.0
- 报告 DDI WDK DirectX 9.0 版
- DDI WDK DirectX 9.0 版
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acffaa94c4ba1a3ba38c3749b7ee94ff2ec70da2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380169"
---
# <a name="reporting-ddi-version"></a>报告 DDI 版本


## <span id="ddk_reporting_ddi_version_gg"></span><span id="DDK_REPORTING_DDI_VERSION_GG"></span>


DirectX 9.0 版本驱动程序必须报告的新版[DDI](direct3d-driver-ddi.md)它支持，以便 DirectX 9.0 运行时能够确定如何处理驱动程序。 若要报告 DDI 版本，该驱动程序响应**GetDriverInfo2**使用 D3DGDI2 请求\_类型\_GETDDIVERSION 值。 **DwDXVersion**的成员[ **DD\_GETDDIVERSIONDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_getddiversiondata)结构设置为 9，以指示 DirectX 9.0 运行时发出请求。

驱动程序集**dwDDIVersion** DD 成员\_GETDDIVERSIONDATA 到支持的 DirectX 9.0 运行时的 DDI 版本。 如果该驱动程序生成的预发布版本的 DirectX 9.0 驱动程序开发工具包 (DDK) 在其中 DDI 版本数已低于 DirectX 9.0 的最终版本中的编号，运行时将驱动程序视为 DirectX 8.0 相反。

 

 





