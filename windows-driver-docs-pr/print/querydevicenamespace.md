---
title: QueryDeviceNamespace
description: IPrintTicketProvider QueryDeviceNamespace 例程提供 PrintTicket DEVMODE 和 DEVMODE PrintTicket 转换将使用在需要将打印票证中的功能或从专用的命名空间的选项时的默认命名空间。
ms.assetid: 5f940cdc-42c3-4521-91c5-cc8e340ce34a
keywords:
- QueryDeviceNamespace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45f407a88c495370fb3d892030d4d89fd86b876a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384690"
---
# <a name="querydevicenamespace"></a>QueryDeviceNamespace


[ **IPrintTicketProvider::QueryDeviceNamespace** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff554378(v=vs.85))例程提供 PrintTicket DEVMODE 和 DEVMODE PrintTicket 转换将在需要时将使用的默认命名空间功能或从打印票证中的专用命名空间的选项。

下面的示例代码说明了如何可以实现此方法。

```cpp
STDMETHODIMP
CPrintTicketProvider::QueryDeviceNamespace(BSTR *pDefaultNamespace)
{
    *pDefaultNamespace = SysAllocString(TEXT("http://schemas.contoso.com/printers/seriesA/v.1.0"));
    
    if (!(*pDefaultNamespace))
    {
        return E_OUTOFMEMORY;
    }
 
    return S_OK;
}
```

 

 




