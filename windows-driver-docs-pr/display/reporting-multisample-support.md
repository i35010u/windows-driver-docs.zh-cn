---
title: 报告多重采样支持
description: 报告多重采样支持
ms.assetid: 05db3a79-08b3-4476-a016-d9a9bfa48504
keywords:
- DirectX 8.0 发行说明了 WDK Windows 2000 显示、多级显示、报告
- 以多级显示方式呈现 WDK DirectX 8.0，报告
- 呈现 multisamples WDK DirectX 8.0，报告
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a5ea2acaf081250355dfe8cfdc0e5936be3eb67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825936"
---
# <a name="reporting-multisample-support"></a>报告多重采样支持


## <span id="ddk_reporting_multisample_support_gg"></span><span id="DDK_REPORTING_MULTISAMPLE_SUPPORT_GG"></span>


驱动程序通过为其报告的每个表面格式指定每个像素的样本数，来报告其关联硬件的多级功能。 [**DDPIXELFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构已扩展为包含名为**MultiSampleCaps**的结构。 此结构具有成员，使驱动程序可以将每个像素的样本数表示为翻转（全屏）和 blt （有窗口）多级多级。 其中每个成员都是 WORD 类型，其中的每个单词值都表示支持给定数量的每个像素的样本。 因此，该驱动程序可以使用单个表面格式条目来支持多个不同的采样计数。

 

 





