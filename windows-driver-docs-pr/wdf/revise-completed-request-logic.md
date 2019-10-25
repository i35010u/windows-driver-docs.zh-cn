---
title: 修改可处理已完成请求的代码
description: 修改可处理已完成请求的代码
ms.assetid: 0DD48424-A728-4887-9F26-46B7004CB12C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ddcc18ccbd5f1806f9b2677f3189abd5f4bad32
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842201"
---
# <a name="revise-code-that-handles-completed-requests"></a>修改可处理已完成请求的代码


Windows 驱动程序框架（WDF）提供了三种方法来完成 i/o 请求：

-   [**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
-   [**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)
-   [**WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) （仅限 KMDF）

有关使用这些方法的信息，请参阅[完成 I/o 请求](completing-i-o-requests.md)。

 

 





