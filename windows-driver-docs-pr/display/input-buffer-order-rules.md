---
title: 输入缓冲区顺序规则
description: 输入缓冲区顺序规则
ms.assetid: 2c588276-88c3-42e4-9f73-50a05e31c451
keywords:
- 输入缓冲区 WDK DirectX VA
- 取消隔行扫描 WDK DirectX va，因此输入的缓冲区顺序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd66848fb10ff098da827566c1dd7e52e51f08ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365507"
---
# <a name="input-buffer-order-rules"></a>输入缓冲区顺序规则


## <span id="ddk_input_buffer_order_rules_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_RULES_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

在应用层的顺序**lpBufferInfo**数组符合以下规则：

-   数组中的第一个面是目标图面。 该驱动程序只会写入到目标图面。

-   下一步一系列数组中的图面是任何以前的目标应用层的组，为其请求取消隔行扫描设备的临时顺序相反其取消隔行扫描算法。

-   下一步一系列数组中的图面是输入隔行扫描或渐进式图面，设备要求若要执行的集合及其取消隔行扫描操作。

-   下一步一系列数组中的图面是视频的子流图面，Z 顺序中的集合。

 

 





