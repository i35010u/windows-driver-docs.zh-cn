---
title: 处理不受支持的 SRB_FUNCTION_XXX
description: 处理不受支持的 SRB_FUNCTION_XXX
ms.assetid: 95b9288c-290f-4908-9de3-11d68ed624e2
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiStartIo
- HwScsiStartIo
- 不支持的 SRB_FUNCTION_XXX
- 不受支持的 SRB_FUNCTION_XXX
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53764b5a0dea1f3800db006f6a58d29dbbe44dfe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371155"
---
# <a name="handling-unsupported-srbfunctionxxx"></a>处理不受支持的 SRB\_函数\_XXX


## <span id="ddk_handling_unsupported_srb_function_xxx_kg"></span><span id="DDK_HANDLING_UNSUPPORTED_SRB_FUNCTION_XXX_KG"></span>


每个*HwScsiStartIo*例程必须处理接收不受支持 SRB\_函数\_*XXX* ，如下所示：

1.  设置输入 SRB 的**SrbStatus**到 SRB\_状态\_无效\_请求。

2.  调用[ **ScsiPortNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)与*NotificationType * * * RequestComplete** 和 SRB 中的输入。

3.  调用**ScsiPortNotification**再次使用 * NotificationType ***NextRequest**，或与**NextLuRequest**如果 HBA 支持有标记的队列或多个请求每个逻辑单元。

4.  返回控件。

 

 




