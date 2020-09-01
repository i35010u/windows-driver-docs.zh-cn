---
title: 处理不受支持的 SRB_FUNCTION_XXX
description: 处理不受支持的 SRB_FUNCTION_XXX
ms.assetid: 95b9288c-290f-4908-9de3-11d68ed624e2
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- 不支持的 SRB_FUNCTION_XXX
- SRB_FUNCTION_XXX 不受支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7d5bde6d90eab0255b30ca3e4583578820b024f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188825"
---
# <a name="handling-unsupported-srb_function_xxx"></a>处理不受支持的 SRB \_ 函数 \_ XXX


## <span id="ddk_handling_unsupported_srb_function_xxx_kg"></span><span id="DDK_HANDLING_UNSUPPORTED_SRB_FUNCTION_XXX_KG"></span>


每个*HwScsiStartIo*例程必须处理收到不受支持的 SRB \_ 函数 \_ *XXX* ，如下所示：

1.  将输入 SRB 的 **SrbStatus** 设置为 SRB \_ STATUS \_ REQUEST STATUS 无效 \_ 。

2.  将 [**ScsiPortNotification**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification) 与 *NotificationType * * * RequestComplete** 和输入 SRB 一起调用。

3.  如果 HBA 支持标记队列或每个逻辑单元多个请求，请与 * NotificationType ***NextRequest**或**NextLuRequest**一起调用**ScsiPortNotification** 。

4.  返回控件。

 

