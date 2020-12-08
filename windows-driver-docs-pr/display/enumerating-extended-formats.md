---
title: 枚举扩展格式
description: 枚举扩展格式
keywords:
- 非标准显示模式 WDK DirectX 9.0，扩展
- 扩展非标准显示模式 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8539294e2ac74ecfc47fa4b73754bc0927892cb9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786883"
---
# <a name="enumerating-extended-formats"></a>枚举扩展格式


## <span id="ddk_enumerating_extended_formats_gg"></span><span id="DDK_ENUMERATING_EXTENDED_FORMATS_GG"></span>


DirectX 9.0 运行时必须在使用这些显示模式执行任何操作之前，验证驱动程序支持的扩展非标准显示模式。 若要验证驱动程序支持的非标准显示模式数量，运行时将使用 **GetDriverInfo2** D3DGDI2 \_ 类型 GETEXTENDEDMODECOUNT 值发送 GetDriverInfo2 请求 \_ 。 如果驱动程序不支持任何非标准的显示模式，它将在此请求的 [**DD \_ GETEXTENDEDMODECOUNTDATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getextendedmodecountdata)结构的 **dwModeCount** 成员中返回零。 若要接收每个受支持的非标准显示模式的相关 **GetDriverInfo2** 信息，运行时使用 D3DGDI2 \_ TYPE \_ GETEXTENDEDMODE 值为每个模式发送 GetDriverInfo2 请求。 然后，该驱动程序将返回 D3DDISPLAYMODE 结构，该结构在 [**DD \_ GETEXTENDEDMODEDATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getextendedmodedata)结构的 **mode** 成员中指定非标准显示模式。 有关 **GetDriverInfo2** 的详细信息，请参阅 [支持 GetDriverInfo2](supporting-getdriverinfo2.md)。 有关 D3DDISPLAYMODE 的详细信息，请参阅最新的 DirectX SDK 文档。

 

