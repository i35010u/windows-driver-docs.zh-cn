---
title: 用于筛选错误代码的宏示例
description: 用于筛选错误代码的宏示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6be0d0ba5b4118d11318db15133906dd42bd49e8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824095"
---
# <a name="macro-example-to-filter-error-codes"></a>用于筛选错误代码的宏示例

> [!IMPORTANT]  
> 已弃用 WSD 争取冠军宝座功能，并且2018中将删除所有与 WSD 争取冠军宝座相关的文档。

下面的宏示例筛选通信失败错误代码。

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

 




