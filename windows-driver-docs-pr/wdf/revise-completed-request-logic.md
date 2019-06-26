---
title: 修改可处理已完成请求的代码
description: 修改可处理已完成请求的代码
ms.assetid: 0DD48424-A728-4887-9F26-46B7004CB12C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5871d27f47daa0267843b3f88b97ff733104738a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376221"
---
# <a name="revise-code-that-handles-completed-requests"></a>修改可处理已完成请求的代码


Windows 驱动程序框架 (WDF) 提供了完成 I/O 请求的三个方法：

-   [**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
-   [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)
-   [**WdfRequestCompleteWithPriorityBoost** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) (仅适用于 KMDF)

有关使用这些方法的信息，请参阅[完成 I/O 请求](completing-i-o-requests.md)。

 

 





