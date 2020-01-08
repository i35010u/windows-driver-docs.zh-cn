---
title: QueryDeviceNamespace
description: 如果 IPrintTicketProvider QueryDeviceNamespace 例程提供了一个默认命名空间，则在需要从专用命名空间中放置一个功能或选项时，该命名空间转换将使用该命名空间。
ms.assetid: 5f940cdc-42c3-4521-91c5-cc8e340ce34a
keywords:
- QueryDeviceNamespace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27c2a49de895530c78ff7cb7cf42109d2944a036
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652848"
---
# <a name="querydevicenamespace"></a>QueryDeviceNamespace


[**IPrintTicketProvider：： QueryDeviceNamespace**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554378(v=vs.85))例程提供一个默认命名空间，如果该命名空间需要从专用命名空间中放置一个功能或选项，则该命名空间转换将使用该命名空间。

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

 

 




