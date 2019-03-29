---
title: 支持非标准显示模式
description: 支持非标准显示模式
ms.assetid: 33a10aed-dfc9-4b64-97fb-e4b7c744dc0d
keywords:
- 使用了非标准的显示模式 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f56ef493d16ceda5ee3b055a76164a41c82b4af6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563765"
---
# <a name="supporting-nonstandard-display-modes"></a>支持非标准显示模式


## <span id="ddk_supporting_nonstandard_display_modes_gg"></span><span id="DDK_SUPPORTING_NONSTANDARD_DISPLAY_MODES_GG"></span>


DirectX 9.0 版本支持任何使用了非标准的显示模式，例如 10-位的每个通道 (10:10:10:2) 的设备驱动程序显示，呈现器目标格式必须响应请求，以枚举这些扩展了非标准的显示模式。 此外，DirectX 9.0 驱动程序必须能够执行操作启用标准和非标准的显示模式之间切换。 以下部分介绍如何驱动程序支持使用了非标准的显示模式：

[枚举扩展的格式](enumerating-extended-formats.md)

[标准和非标准模式之间切换](switching-between-standard-and-nonstandard-modes.md)

[处理非标准的显示模式](handling-nonstandard-display-modes.md)

 

 





