---
title: 报告的多重采样支持
description: 报告的多重采样支持
ms.assetid: 05db3a79-08b3-4476-a016-d9a9bfa48504
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多重采样呈现报告
- 多重采样呈现 DirectX WDK 8.0，报告
- 呈现 multisamples WDK DirectX 8.0，报告
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdcb35249b53f7e87bde35a5a55dcc51cb8cae71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527205"
---
# <a name="reporting-multisample-support"></a>报告的多重采样支持


## <span id="ddk_reporting_multisample_support_gg"></span><span id="DDK_REPORTING_MULTISAMPLE_SUPPORT_GG"></span>


驱动程序报告其相关联的硬件的多重采样功能通过指定的每个像素它报告每个图面格式的样本数。 [ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)结构已扩展为包括一个称为结构**MultiSampleCaps**。 此结构具有让 express 为每像素 flip （全屏） 和 blt （窗口） 多重采样的样本数的驱动程序的成员。 其中每个成员是 WORD 类型中的单词的每一位值表示对给定数量的每个像素的示例的支持。 因此，该驱动程序可以表示对与单个图面上的格式项的多个不同的样本计数的支持。

 

 





