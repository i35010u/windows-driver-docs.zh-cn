---
title: 报告多重采样支持
description: 报告多重采样支持
keywords:
- DirectX 8.0 发行说明了 WDK Windows 2000 显示、多级显示、报告
- 以多级显示方式呈现 WDK DirectX 8.0，报告
- 呈现 multisamples WDK DirectX 8.0，报告
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d393d373f335698e546d3f16330858b4968d1314
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828057"
---
# <a name="reporting-multisample-support"></a>报告多重采样支持


## <span id="ddk_reporting_multisample_support_gg"></span><span id="DDK_REPORTING_MULTISAMPLE_SUPPORT_GG"></span>


驱动程序通过为其报告的每个表面格式指定每个像素的样本数，来报告其关联硬件的多级功能。 [**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构已扩展为包含名为 **MultiSampleCaps** 的结构。 此结构具有成员，使驱动程序可以将每个像素的样本数表示为翻转 (全屏) 和 blt (按窗口) 多级。 其中每个成员都是 WORD 类型，其中的每个单词值都表示支持给定数量的每个像素的样本。 因此，该驱动程序可以使用单个表面格式条目来支持多个不同的采样计数。

 

