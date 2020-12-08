---
title: 获取 I/O 请求的参数
description: 获取 I/O 请求的参数
keywords:
- I/o 请求 WDK UMDF，获取参数
- 请求处理 WDK UMDF，获取参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b00a40428af5b0e7549b395556dceec4d6f4a63
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840855"
---
# <a name="obtaining-parameters-for-io-requests"></a>获取 I/O 请求的参数


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当驱动程序收到 i/o 请求时，驱动程序可以使用 [IWDFIoRequest](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest) 接口的以下方法来获取与请求相关的参数：

-   [**IWDFIoRequest：： GetCreateParameters**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getcreateparameters)或 [ **IWDFIoRequest2：： GetCreateParametersEx**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-getcreateparametersex)

-   [**IWDFIoRequest::GetDeviceIoControlParameters**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getdeviceiocontrolparameters)

-   [**IWDFIoRequest::GetReadParameters**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getreadparameters)

-   [**IWDFIoRequest::GetWriteParameters**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getwriteparameters)

 

