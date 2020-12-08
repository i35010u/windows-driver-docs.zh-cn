---
title: 修改可处理已完成请求的代码
description: 修改可处理已完成请求的代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 351b2062f0d0da4ebb83d03e14fc815ad512c685
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787127"
---
# <a name="revise-code-that-handles-completed-requests"></a>修改可处理已完成请求的代码


Windows 驱动程序框架 (WDF) 提供以下三种方法来完成 i/o 请求：

-   [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)
-   [**WdfRequestCompleteWithInformation**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)
-   [**WdfRequestCompleteWithPriorityBoost**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost) (KMDF 仅) 

有关使用这些方法的信息，请参阅 [完成 I/o 请求](completing-i-o-requests.md)。

 

