---
title: 获取 I/O 请求的参数
description: 获取 I/O 请求的参数
ms.assetid: 1ba1fdcf-99bd-44e3-adbf-5dc93a790900
keywords:
- I/O 请求 WDK UMDF，获取参数
- 请求处理 WDK UMDF，获取参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc2b548e9d319346afa33c8743476f8c8462552d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576543"
---
# <a name="obtaining-parameters-for-io-requests"></a>获取 I/O 请求的参数


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

驱动程序接收的 I/O 请求，驱动程序可以使用下列方法之一[IWDFIoRequest](https://msdn.microsoft.com/library/windows/hardware/ff558985)与请求相关的接口，以获得参数：

-   [**IWDFIoRequest::GetCreateParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff559088)或[ **IWDFIoRequest2::GetCreateParametersEx**](https://msdn.microsoft.com/library/windows/hardware/ff558989)

-   [**IWDFIoRequest::GetDeviceIoControlParameters**](https://msdn.microsoft.com/library/windows/hardware/ff559095)

-   [**IWDFIoRequest::GetReadParameters**](https://msdn.microsoft.com/library/windows/hardware/ff559113)

-   [**IWDFIoRequest::GetWriteParameters**](https://msdn.microsoft.com/library/windows/hardware/ff559130)

 

 





