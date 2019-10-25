---
title: 不是由 RDBSS 使用的例程
description: 不是由 RDBSS 使用的例程
ms.assetid: bf3e2936-05c9-4012-a55b-40022844f5db
keywords:
- 小型重定向程序 WDK，RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 183069f6d22ce2d5c6c390a9a42d115fa4732d8c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840981"
---
# <a name="routines-not-used-by-rdbss"></a>不是由 RDBSS 使用的例程


RDBSS 不会调用 MINIRDR\_调度结构中列出的许多例程，也不会使用这些例程。 网络小型重定向程序无需实现其中的任何例程，因为它们永远不会被调用。 网络小型重定向程序应在\_MINIRDR 中从其[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程传入的[**RxRegisterMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr)中为所有这些例程设置**NULL**指针。

下面是 RDBSS 未使用的例程的完整列表：

-   **MRxCancel**

-   **MRxCancelCreateSrvCall**

-   **MRxClosedFcbTimeOut**

-   **MRxClosedSrvOpenTimeOut**

-   **MRxClosePrintFile**

-   **MRxEnumeratePrintQueue**

-   **MRxLowIOSubmit\[LOWIO\_操作\_CLEAROUT\]**

-   **MRxOpenPrintFile**

-   **MRxUpdateNetRootState**

-   **MRxWritePrintFile**

 

 




