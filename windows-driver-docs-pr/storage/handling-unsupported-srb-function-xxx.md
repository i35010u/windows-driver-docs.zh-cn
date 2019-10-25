---
title: 处理不受支持的 SRB_FUNCTION_XXX
description: 处理不受支持的 SRB_FUNCTION_XXX
ms.assetid: 95b9288c-290f-4908-9de3-11d68ed624e2
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- 不支持的 SRB_FUNCTION_XXX
- 不支持 SRB_FUNCTION_XXX
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cae8f7c6c8ebf5f7aec914f0c6d3561c6a46eec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833714"
---
# <a name="handling-unsupported-srb_function_xxx"></a>处理不受支持的 SRB\_函数\_XXX


## <span id="ddk_handling_unsupported_srb_function_xxx_kg"></span><span id="DDK_HANDLING_UNSUPPORTED_SRB_FUNCTION_XXX_KG"></span>


每个*HwScsiStartIo*例程必须按如下所示处理收到不支持的 SRB\_函数\_*XXX* ：

1.  将输入 SRB 的**SrbStatus**设置为 SRB\_状态\_无效\_请求。

2.  将[**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)与*NotificationType * * * RequestComplete** 和输入 SRB 一起调用。

3.  如果 HBA 支持标记队列或每个逻辑单元多个请求，请与 * NotificationType ***NextRequest**或**NextLuRequest**一起调用**ScsiPortNotification** 。

4.  返回控件。

 

 




