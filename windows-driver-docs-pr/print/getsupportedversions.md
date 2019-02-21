---
title: GetSupportedVersions
description: IPrintTicketProvider GetSupportedVersions 方法返回的打印架构的打印驱动程序支持的主要版本号。 现在，版本 1 是不存在，因此此方法必须返回一个受支持的版本的唯一版本。
ms.assetid: 0b648cc3-4d61-401c-b626-34db2b026b2a
keywords:
- GetSupportedVersions
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 789e8584590b7abaab5001e9279c1d47a535b6a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521037"
---
# <a name="getsupportedversions"></a>GetSupportedVersions


[ **IPrintTicketProvider::GetSupportedVersions** ](https://msdn.microsoft.com/library/windows/hardware/ff554371)方法返回的打印架构的打印驱动程序支持的主要版本号。 现在，版本 1 是不存在，因此此方法必须返回一个受支持的版本的唯一版本。

下面的示例代码中显示的实现将适用于初始版本的 Windows Vista 和之前添加的新版本。 如果支持新版本，则将更改此值。

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

 

 




