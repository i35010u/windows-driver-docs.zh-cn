---
title: 支持非标准显示模式
description: 支持非标准显示模式
keywords:
- 非标准显示模式 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdb00c7d196cce7c33906c1f2b4020928ae57d87
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803897"
---
# <a name="supporting-nonstandard-display-modes"></a>支持非标准显示模式


## <span id="ddk_supporting_nonstandard_display_modes_gg"></span><span id="DDK_SUPPORTING_NONSTANDARD_DISPLAY_MODES_GG"></span>


支持任何非标准显示模式的设备的 DirectX 9.0 版本驱动程序，如每通道10位数 (10:10:10:2) 显示和呈现目标格式，则必须响应枚举这些扩展非标准显示模式的请求。 此外，DirectX 9.0 驱动程序必须能够执行启用在标准和非标准显示模式之间切换的操作。 以下各节介绍了驱动程序如何支持非标准显示模式：

[枚举扩展格式](enumerating-extended-formats.md)

[在标准与非标准模式之间切换](switching-between-standard-and-nonstandard-modes.md)

[处理非标准显示模式](handling-nonstandard-display-modes.md)

 

 





