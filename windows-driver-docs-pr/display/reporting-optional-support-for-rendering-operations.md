---
title: 报告渲染操作的可选支持
description: 报告渲染操作的可选支持
ms.assetid: 97a0b8c6-7ff8-47df-97df-4e9714ebc903
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4418dc5d9ef4cff1e95e240b7b24166ae8532c20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359299"
---
# <a name="reporting-optional-support-for-rendering-operations"></a>报告渲染操作的可选支持


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


从 Windows 7 开始，显示微型端口驱动程序可以设置其他成员[ **DXGK\_PRESENTATIONCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)结构，以指示驱动程序可以某些呈现操作或不能支持。

有关可用的呈现功能设置的详细信息，请参阅[ **DXGK\_PRESENTATIONCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)。

 

 





