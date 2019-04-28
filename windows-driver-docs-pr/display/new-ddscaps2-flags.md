---
title: 新的 DDSCAPS2 标志
description: 新的 DDSCAPS2 标志
ms.assetid: a5171865-7339-422f-8470-154a0aadc496
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示、 演示文稿
- 演示文稿 WDK DirectX 8.0
- 呈现结果可见 WDK DirectX 8.0
- 可见结果 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9938243a85570bd1bdcb85e5ef95200bdc7ed24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345554"
---
# <a name="new-ddscaps2-flags"></a>新的 DDSCAPS2 标志


## <span id="ddk_new_ddscaps2_flags_gg"></span><span id="DDK_NEW_DDSCAPS2_FLAGS_GG"></span>


新的标志，DDSCAPS2\_引入了 DISCARDBACKBUFFER，以指示不需要保留的后台缓冲区。 如果应用程序已设置 D3DSWAPEFFECT 设置主表面和后台缓冲区\_放弃上**存在**API。

DX8 运行时现在设置另一个新的标志，DDSCAPS2\_NOTUSERLOCKABLE，在主数据库和后台缓冲区如果翻转链不是可锁定，或者不是可锁定任何呈现器目标上。 这允许进行后台优化背后的驱动程序。 请注意，仍可锁定图面，以便该驱动程序必须处理这些情况下，但这种锁不太频繁，并且不应是快地执行。

该驱动程序还可以确定深度/模具缓冲区是否是由 DDSCAPS2 存在可锁定\_NOTUSERLOCKABLE 标志。

 

 





