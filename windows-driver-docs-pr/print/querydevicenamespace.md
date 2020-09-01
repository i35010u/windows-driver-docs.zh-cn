---
title: QueryDeviceNamespace
description: 如果 IPrintTicketProvider QueryDeviceNamespace 例程提供了一个默认命名空间，则在需要从专用命名空间中放置一个功能或选项时，该命名空间转换将使用该命名空间。
ms.assetid: 5f940cdc-42c3-4521-91c5-cc8e340ce34a
keywords:
- QueryDeviceNamespace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc5b9a41ee4a848e6c96a55128b401bdab750c3f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207071"
---
# <a name="querydevicenamespace"></a>QueryDeviceNamespace


[**IPrintTicketProvider：： QueryDeviceNamespace**](/previous-versions/windows/hardware/drivers/ff554378(v=vs.85))例程提供一个默认命名空间，如果该命名空间需要从专用命名空间中放置一个功能或选项，则该命名空间转换将使用该命名空间。

下面的示例代码演示如何实现此方法。

```cpp
STDMETHODIMP
CPrintTicketProvider::QueryDeviceNamespace(BSTR *pDefaultNamespace)
{
    *pDefaultNamespace = SysAllocString(TEXT("https://schemas.contoso.com/printers/seriesA/v.1.0"));
    
    if (!(*pDefaultNamespace))
    {
        return E_OUTOFMEMORY;
    }
 
    return S_OK;
}
```

 

