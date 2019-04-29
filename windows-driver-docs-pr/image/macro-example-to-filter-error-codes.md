---
title: 用于筛选错误代码的宏示例
description: 用于筛选错误代码的宏示例
ms.assetid: 68aa0a75-82c7-4dd9-8f8f-eca5de6ea102
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f2f6ccd212cfcefbfb4c36956a4b51ac8a9a167
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373914"
---
# <a name="macro-example-to-filter-error-codes"></a>用于筛选错误代码的宏示例

> [!IMPORTANT]  
> WSD 占领功能已弃用，将在 2018年中删除所有与 WSD 占领相关文档。

下面的宏示例筛选器的通信失败错误代码。

```cpp
//
// Example of a macro to filter device communication errors
//
#define WSD_COMMUNICATION_ERROR(hr) \
    ((HRESULT_FROM_WIN32(ERROR_WINHTTP_CANNOT_CONNECT)) == hr) || \
    ((HRESULT_FROM_WIN32(ERROR_WINHTTP_CONNECTION_ERROR)) == hr) || \
    ((HRESULT_FROM_WIN32(ERROR_WINHTTP_TIMEOUT)) == hr) || \
    ((HRESULT_FROM_WIN32(ERROR_TIMEOUT)) == hr) || \
    ((HRESULT_FROM_WIN32(ERROR_WINHTTP_NAME_NOT_RESOLVED)) == hr))
```

 




