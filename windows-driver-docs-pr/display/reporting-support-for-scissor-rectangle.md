---
title: 报告裁切矩形支持
description: 报告裁切矩形支持
keywords:
- 剪刀矩形 WDK DirectX 9.0，报告支持
- 矩形剪辑区域 WDK DirectX 9.0，报告支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2001e65cab56871b493af27362d2d2be817b1a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838799"
---
# <a name="reporting-support-for-scissor-rectangle"></a>报告裁切矩形支持


## <span id="ddk_reporting_support_for_scissor_rectangle_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_SCISSOR_RECTANGLE_GG"></span>


DirectX 9.0 版本驱动程序通过设置 \_ D3DCAPS9 结构的 **RasterCaps** 成员中的 D3DPRASTERCAPS SCISSORTEST 功能位，指示其设备支持剪刀测试。

 

 





