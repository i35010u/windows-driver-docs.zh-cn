---
title: GetSupportedVersions
description: IPrintTicketProvider GetSupportedVersions 方法返回打印驱动程序支持的打印架构的主版本号。 目前，版本1是存在的唯一版本，因此此方法只能返回一个受支持的版本。
ms.assetid: 0b648cc3-4d61-401c-b626-34db2b026b2a
keywords:
- GetSupportedVersions
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77536b124297b8a0d1c519a1aa8d3d6f20159326
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217737"
---
# <a name="getsupportedversions"></a>GetSupportedVersions


[**IPrintTicketProvider：： GetSupportedVersions**](/previous-versions/windows/hardware/drivers/ff554371(v=vs.85))方法返回打印驱动程序支持的打印架构的主版本号。 目前，版本1是存在的唯一版本，因此此方法只能返回一个受支持的版本。

以下示例代码中所示的实现适用于 Windows Vista 的初始版本，并且在添加新版本之前。 支持新版本时，此值将更改。

```cpp
STDMETHODIMP 
CPrintTicketProvider::
GetSupportedVersions(THIS_ HANDLE hPrinter,
                           INT *ppVersions[],
                           INT *pcVersions)
{
    if ( (*ppVersions = (INT*)CoTaskMemAlloc(sizeof(INT))) != NULL)
    {
         (*ppVersions)[0] = 1;  // Version 1
        *pcVersions = 1; // 1 supported version
        return S_OK;
    }
    else
        return E_OUTOFMEMORY;
}
```

 

