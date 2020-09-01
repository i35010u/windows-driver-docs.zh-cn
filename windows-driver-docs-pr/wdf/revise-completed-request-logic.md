---
title: 修改可处理已完成请求的代码
description: 修改可处理已完成请求的代码
ms.assetid: 0DD48424-A728-4887-9F26-46B7004CB12C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f5abba0773fb4c0dcbd4c5d2ba5afe5dc825767
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189657"
---
# <a name="revise-code-that-handles-completed-requests"></a>修改可处理已完成请求的代码


Windows 驱动程序框架 (WDF) 提供以下三种方法来完成 i/o 请求：

-   [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
-   [**WdfRequestCompleteWithInformation**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)
-   [**WdfRequestCompleteWithPriorityBoost**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) (KMDF 仅) 

有关使用这些方法的信息，请参阅 [完成 I/o 请求](completing-i-o-requests.md)。

 

