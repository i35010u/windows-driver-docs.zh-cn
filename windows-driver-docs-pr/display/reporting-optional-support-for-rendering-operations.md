---
title: 报告渲染操作的可选支持
description: 报告渲染操作的可选支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b8b6fd5c90d5ff8dca1cfb8a1a347838866d736
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828055"
---
# <a name="reporting-optional-support-for-rendering-operations"></a>报告渲染操作的可选支持


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


从 Windows 7 开始，显示微型端口驱动程序可以在 [**DXGK \_ PRESENTATIONCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps) 结构中设置其他成员，以指示驱动程序可以或不支持的某些呈现操作。

有关可用呈现功能设置的详细信息，请参阅 [**DXGK \_ PRESENTATIONCAPS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)。

 

