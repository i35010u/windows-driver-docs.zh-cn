---
title: 专用显示微型端口驱动程序 IOCTL_VIDEO_XXX 请求
description: 微型端口驱动程序可以定义一个或更专用的其对应的 I/O 控制代码显示驱动程序。
ms.assetid: 45d8c9bc-993c-4fd3-949d-dfb30bb685d7
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，处理请求
- 请求处理 WDK 微型端口
- 私下定义 IOCTL_VIDEO_XXX 请求 WDK 微型端口
- IOCTL_VIDEO_XXX 请求 WDK 微型端口
- I/O WDK 微型端口
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: db95944e4fdd510d1de432f4f52a0740055d7256
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363728"
---
# <a name="privately-defined-display-miniport-driver-ioctlvideoxxx-requests"></a>私下定义显示微型端口驱动程序 IOCTL\_视频\_XXX 请求

微型端口驱动程序可以定义一个或更专用的其对应的 I/O 控制代码显示驱动程序。

但是，只有特定显示微型端口驱动程序对可以使用私人定义的 I/O 控制代码。 即，运行在现有的显示器驱动程序微型端口驱动程序不应定义专用的 I/O 控制代码由于现有的显示器驱动程序不能进行新的 I/O 控制请求，而无需进行重写，并在可能，而不会中断现有已使用的微型端口驱动程序。 现有的或泛型显示器驱动程序上层的多个不同模型的适配器，如 SVGA 适配器，也不能依赖于私人定义的 I/O 控制代码，在每个基础的微型端口驱动程序中有相同的效果。

有关详细信息，有关定义专用的 I/O 控制代码，请参阅[使用的 I/O 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)。

 

 





