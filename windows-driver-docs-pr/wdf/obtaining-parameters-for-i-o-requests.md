---
title: 获取 I/O 请求的参数
description: 获取 I/O 请求的参数
ms.assetid: 1ba1fdcf-99bd-44e3-adbf-5dc93a790900
keywords:
- I/o 请求 WDK UMDF，获取参数
- 请求处理 WDK UMDF，获取参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7f6f8cb1ee6c0c9ec8e9e3aed92a1de937f7061
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75208919"
---
# <a name="obtaining-parameters-for-io-requests"></a>获取 I/O 请求的参数


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当驱动程序收到 i/o 请求时，驱动程序可以使用[IWDFIoRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)接口的以下方法来获取与请求相关的参数：

-   [**IWDFIoRequest：： GetCreateParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getcreateparameters)或[ **IWDFIoRequest2：： GetCreateParametersEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-getcreateparametersex)

-   [**IWDFIoRequest::GetDeviceIoControlParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getdeviceiocontrolparameters)

-   [**IWDFIoRequest::GetReadParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getreadparameters)

-   [**IWDFIoRequest::GetWriteParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getwriteparameters)

 

 





