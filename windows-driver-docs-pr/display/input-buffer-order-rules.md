---
title: 输入缓冲区顺序规则
description: 输入缓冲区顺序规则
keywords:
- 输入缓冲 WDK DirectX VA
- 取消隔行扫描 WDK DirectX VA，输入缓冲区顺序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b9c38958b8cddd9eddd5de7e6d208ecf21e5b1c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827237"
---
# <a name="input-buffer-order-rules"></a>输入缓冲区顺序规则


## <span id="ddk_input_buffer_order_rules_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_RULES_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

**LpBufferInfo** 数组中的图面的顺序符合以下规则：

-   数组中的第一个表面是目标图面。 驱动程序仅写入目标图面。

-   数组中的下一个图面序列是取消隔行扫描设备为其隔行扫描算法请求的任何先前目标面的组（反向时态顺序）。

-   数组中的下一个图面的序列是设备在执行其取消隔行扫描操作时所需的输入交错或渐进式曲面的集合。

-   数组中的下一个图面的序列是按 Z 顺序排列的视频子流图面的集合。

 

 





