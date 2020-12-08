---
title: 新的 DDSCAPS2 标志
description: 新的 DDSCAPS2 标志
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，演示
- 演示文稿 WDK DirectX 8。0
- 呈现结果可见 WDK DirectX 8。0
- 可见结果 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89bebd15fedcea4ef6e7c3c1ab21376a118eec0a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840377"
---
# <a name="new-ddscaps2-flags"></a>新的 DDSCAPS2 标志


## <span id="ddk_new_ddscaps2_flags_gg"></span><span id="DDK_NEW_DDSCAPS2_FLAGS_GG"></span>


引入了新标志 DDSCAPS2 \_ DISCARDBACKBUFFER，表示不需要保留后台缓冲区。 如果应用程序已 \_ 在 **当前** API 上设置 D3DSWAPEFFECT 放弃，则会在主表面和后台缓冲区上设置此设置。

DX8 运行时现在在 \_ 主缓冲区和后台缓冲区上设置另一个新标志 DDSCAPS2 NOTUSERLOCKABLE，如果翻转链不可锁定，则设置为; 否则，在任何不可锁定的呈现目标上设置另一个新标志。 这使得驱动程序能够在幕后优化后进行。 请注意，仍可以锁定表面，以便驱动程序必须处理这些情况，但这种锁很少出现，并且预计速度不会过快。

驱动程序还可以通过存在 DDSCAPS2 NOTUSERLOCKABLE 标志来确定深度/模具缓冲区是否可锁定 \_ 。

 

 





