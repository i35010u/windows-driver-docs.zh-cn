---
title: 输入缓冲区顺序
description: 输入缓冲区顺序
ms.assetid: 99110b1a-1511-44f5-a4bb-a5e38fd41fff
keywords:
- 输入缓冲 WDK DirectX VA
- 取消隔行扫描 WDK DirectX VA，输入缓冲区顺序
- 缓冲 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1558f24c5e4019fb41440b68dc0a54e1f1885172
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423672"
---
# <a name="input-buffer-order"></a>输入缓冲区顺序


## <span id="ddk_input_buffer_order_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

对于每个组合取消隔行扫描和子流组合操作，VMR 将启动对驱动程序提供的 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数的调用。 在*DdMoCompRender*调用中， [**DD \_ RENDERMOCOMPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_rendermocompdata)结构的**lpBufferInfo**成员指向一组缓冲区，这些缓冲区描述目标图面和每个输入视频源示例的图面。 *DdMoCompRender*函数反过来调用驱动程序的[**DeinterlaceBltEx**](./dxva-deinterlacebobdeviceclass-deinterlacebltex.md)函数。 有关详细信息，请参阅 [从用户模式组件调用取消隔行扫描 DDI](calling-the-deinterlace-ddi-from-a-user-mode-component.md)。

[**DXVA \_ DeinterlaceBltEx**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacebltex)结构的**源**成员中[**DXVA \_ VideoSample2**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videosample2)结构的数组中元素的顺序与**lpBufferInfo**数组匹配，但目标表面不存在。

以下主题描述了在 **lpBufferInfo** 数组中排列图面的规则，并提供了说明曲面序列顺序的示例：

[输入缓冲区顺序规则](input-buffer-order-rules.md)

[输入缓冲区顺序示例 1](input-buffer-order-example-1.md)

[输入缓冲区顺序示例 2](input-buffer-order-example-2.md)

[输入缓冲区顺序示例 3](input-buffer-order-example-3.md)

[输入缓冲区顺序示例 4](input-buffer-order-example-4.md)

[输入缓冲区顺序示例 5](input-buffer-order-example-5.md)

[输入缓冲区顺序示例 6](input-buffer-order-example-6.md)

 

