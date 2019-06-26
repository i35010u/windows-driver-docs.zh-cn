---
title: 枚举扩展格式
description: 枚举扩展格式
ms.assetid: 504464ff-4449-43fa-9fc8-645400ac8236
keywords:
- 使用了非标准的显示模式 WDK DirectX 9.0 中，扩展
- 扩展了非标准的显示模式 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbbbdd464946532ce1ba20ff33f4bb5234fd8f6c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355546"
---
# <a name="enumerating-extended-formats"></a>枚举扩展格式


## <span id="ddk_enumerating_extended_formats_gg"></span><span id="DDK_ENUMERATING_EXTENDED_FORMATS_GG"></span>


运行时必须验证驱动程序支持执行使用的任何操作之前的扩展使用了非标准的显示模式 DirectX 9.0 的显示模式。 若要验证的驱动程序支持的非标准的显示模式的数，运行时发送**GetDriverInfo2**请求使用 D3DGDI2\_类型\_GETEXTENDEDMODECOUNT 值。 如果该驱动程序不支持任何使用了非标准的显示模式，它将返回零**dwModeCount**的成员[ **DD\_GETEXTENDEDMODECOUNTDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_getextendedmodecountdata)此请求的结构。 若要接收有关每个受支持的非标准显示模式的信息，运行时发送**GetDriverInfo2**请求使用 D3DGDI2\_类型\_GETEXTENDEDMODE 每种模式的值。 该驱动程序然后返回 D3DDISPLAYMODE 结构，它指定中使用了非标准的显示模式**模式下**的成员[ **DD\_GETEXTENDEDMODEDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_getextendedmodedata)结构。 有关详细信息**GetDriverInfo2**，请参阅[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。 有关 D3DDISPLAYMODE 详细信息，请参阅最新的 DirectX SDK 文档。

 

 





