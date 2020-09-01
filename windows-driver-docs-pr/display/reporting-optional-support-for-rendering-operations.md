---
title: 报告渲染操作的可选支持
description: 报告渲染操作的可选支持
ms.assetid: 97a0b8c6-7ff8-47df-97df-4e9714ebc903
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24faa4dc0f49b918172b1a0a94e344ed56affab0
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066380"
---
# <a name="reporting-optional-support-for-rendering-operations"></a>报告渲染操作的可选支持


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


从 Windows 7 开始，显示微型端口驱动程序可以在 [**DXGK \_ PRESENTATIONCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps) 结构中设置其他成员，以指示驱动程序可以或不支持的某些呈现操作。

有关可用呈现功能设置的详细信息，请参阅 [**DXGK \_ PRESENTATIONCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)。

 

