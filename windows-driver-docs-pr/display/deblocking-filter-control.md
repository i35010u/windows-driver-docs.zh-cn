---
title: 除块筛选器控制
description: 除块筛选器控制
keywords:
- macroblocks WDK DirectX VA，deblocking filter control
- deblocking 筛选器控件 WDK DirectX VA
- 色度预测块 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e347429d123c81bc454bf56cf4fb716875ee6260
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820837"
---
# <a name="deblocking-filter-control"></a>除块筛选器控制


## <span id="ddk_deblocking_filter_control_gg"></span><span id="DDK_DEBLOCKING_FILTER_CONTROL_GG"></span>


Deblocking 筛选器控件命令（如果存在）将为宏块中的每个明亮块发送一次，并为每对色度块发送一次。 筛选器控件命令是在宏块内以光栅扫描顺序发送的。 在色度的任何块之前，将针对亮度的所有块发送筛选器控件命令。 然后，将为一个色度4:2:0 块发送筛选器控制命令，然后针对一个色度4:2:2 块 (如果4:2:2 正在) 使用，则对于两个色度4:4:4 命令 (相同的筛选将应用于这两个色度 *组件*) 。

每个块的筛选都是通过在块的上边缘指定 deblocking 来完成的，后跟块左边缘的 deblocking。 Deblocking 仅指定给色度一次，并同时用于 Cb 和 Cr 组件的相同 Deblocking 命令。 例如，通过向亮度块发送两组两个 (top 和 left) 的边缘筛选命令，然后为两个色度块发送一组两个边缘筛选命令，就可以使用8x8 块中包含4:2:0 数据的16x16 宏块的 deblocking。

 

 





