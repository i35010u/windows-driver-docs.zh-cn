---
title: QueryDeviceNamespace
description: IPrintTicketProvider QueryDeviceNamespace 例程提供 PrintTicket DEVMODE 和 DEVMODE PrintTicket 转换将使用在需要将打印票证中的功能或从专用的命名空间的选项时的默认命名空间。
ms.assetid: 5f940cdc-42c3-4521-91c5-cc8e340ce34a
keywords:
- QueryDeviceNamespace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bb3fb6db8507c4896c7ef1ce78a6df090cc73bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567888"
---
# <a name="querydevicenamespace"></a>QueryDeviceNamespace


[ **IPrintTicketProvider::QueryDeviceNamespace** ](https://msdn.microsoft.com/library/windows/hardware/ff554378)例程提供 PrintTicket DEVMODE 和 DEVMODE PrintTicket 转换将在需要时将使用的默认命名空间功能或从打印票证中的专用命名空间的选项。

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

 

 




