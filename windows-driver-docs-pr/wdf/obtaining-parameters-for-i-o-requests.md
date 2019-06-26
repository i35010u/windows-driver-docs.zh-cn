---
title: 获取 I/O 请求的参数
description: 获取 I/O 请求的参数
ms.assetid: 1ba1fdcf-99bd-44e3-adbf-5dc93a790900
keywords:
- I/O 请求 WDK UMDF，获取参数
- 请求处理 WDK UMDF，获取参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10dc2f314f9e01885c27646a55804bf6bafe1d38
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375070"
---
# <a name="obtaining-parameters-for-io-requests"></a>获取 I/O 请求的参数


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

驱动程序接收的 I/O 请求，驱动程序可以使用下列方法之一[IWDFIoRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest)与请求相关的接口，以获得参数：

-   [**IWDFIoRequest::GetCreateParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getcreateparameters)或[ **IWDFIoRequest2::GetCreateParametersEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-getcreateparametersex)

-   [**IWDFIoRequest::GetDeviceIoControlParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getdeviceiocontrolparameters)

-   [**IWDFIoRequest::GetReadParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getreadparameters)

-   [**IWDFIoRequest::GetWriteParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getwriteparameters)

 

 





