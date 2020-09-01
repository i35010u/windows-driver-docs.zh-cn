---
title: 获取 I/O 请求的参数
description: 获取 I/O 请求的参数
ms.assetid: 1ba1fdcf-99bd-44e3-adbf-5dc93a790900
keywords:
- I/o 请求 WDK UMDF，获取参数
- 请求处理 WDK UMDF，获取参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0276122596d10230e02d06ad70a84d257c11e275
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184619"
---
# <a name="obtaining-parameters-for-io-requests"></a>获取 I/O 请求的参数


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当驱动程序收到 i/o 请求时，驱动程序可以使用 [IWDFIoRequest](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest) 接口的以下方法来获取与请求相关的参数：

-   [**IWDFIoRequest：： GetCreateParameters**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getcreateparameters)或[ **IWDFIoRequest2：： GetCreateParametersEx**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-getcreateparametersex)

-   [**IWDFIoRequest::GetDeviceIoControlParameters**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getdeviceiocontrolparameters)

-   [**IWDFIoRequest::GetReadParameters**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getreadparameters)

-   [**IWDFIoRequest::GetWriteParameters**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getwriteparameters)

 

