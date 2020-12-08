---
title: 处理不受支持的 SRB_FUNCTION_XXX
description: 处理不受支持的 SRB_FUNCTION_XXX
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- 不支持的 SRB_FUNCTION_XXX
- SRB_FUNCTION_XXX 不受支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93bd5b2d682570a477876fb98ac35fd2e7eea9c4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804497"
---
# <a name="handling-unsupported-srb_function_xxx"></a>处理不受支持的 SRB \_ 函数 \_ XXX


## <span id="ddk_handling_unsupported_srb_function_xxx_kg"></span><span id="DDK_HANDLING_UNSUPPORTED_SRB_FUNCTION_XXX_KG"></span>


每个 *HwScsiStartIo* 例程必须处理收到不受支持的 SRB \_ 函数 \_ *XXX* ，如下所示：

1.  将输入 SRB 的 **SrbStatus** 设置为 SRB \_ STATUS \_ REQUEST STATUS 无效 \_ 。

2.  将 [**ScsiPortNotification**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification) 与 *NotificationType * * * RequestComplete** 和输入 SRB 一起调用。

3.  如果 HBA 支持标记队列或每个逻辑单元多个请求，请与 * NotificationType ***NextRequest** 或 **NextLuRequest** 一起调用 **ScsiPortNotification** 。

4.  返回控件。

 

