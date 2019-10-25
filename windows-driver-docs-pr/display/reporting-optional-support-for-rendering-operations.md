---
title: 报告渲染操作的可选支持
description: 报告渲染操作的可选支持
ms.assetid: 97a0b8c6-7ff8-47df-97df-4e9714ebc903
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e53f898c34ac57a20bb8cb631178ff5c88afd7c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825931"
---
# <a name="reporting-optional-support-for-rendering-operations"></a>报告渲染操作的可选支持


## <span id="ddk_introduction_to_command_and_dma_buffers_gg"></span><span id="DDK_INTRODUCTION_TO_COMMAND_AND_DMA_BUFFERS_GG"></span>


从 Windows 7 开始，显示微型端口驱动程序可以在[**DXGK\_PRESENTATIONCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)结构中设置其他成员，以指示驱动程序可以或不支持的某些呈现操作。

有关可用呈现功能设置的详细信息，请参阅[**DXGK\_PRESENTATIONCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_presentationcaps)。

 

 





