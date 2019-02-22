---
title: 定义和示例中所用的变量
description: 定义和示例中所用的变量
ms.assetid: 55dd0618-2171-406b-a22a-437412c77cbc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 142e5d678d5e0460ec79ab893052173cc9fa7127
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543897"
---
# <a name="definitions-and-variables-used-in-the-examples"></a>定义和示例中所用的变量

> [!IMPORTANT]  
> WSD 占领功能已弃用，将在 2018年中删除所有与 WSD 占领相关文档。

下面的代码演示在本部分中的代码示例中的常量定义和使用的公共变量。

```cpp
//
// WSD Challenge DLL name (including a forward path separator) and public API names
 
//
#define WSDCHNGR_DLL_NAME                    L"\\WSDCHNGR.DLL"
#define WSDCHNR_INITIALIZE                   "WSDCHNGRInitialize" 
#define WSDCHNR_SHUTDOWN                     "WSDCHNGRShutdown" 
#define WSDCHNR_REGISTER_DEVICE_TO_CHALLENGE "WSDCHNGRRegisterDeviceToChallenge" 

//
// Function pointer types for public WSD Challenge APIs
//
typedef HRESULT (*PFN_WSDCHNR_INITIALIZE)();
typedef HRESULT (*PFN_WSDCHNR_SHUTDOWN)();
typedef HRESULT (*PFN_WSDCHNR_REGISTER_DEVICE_TO_CHALLENGE)(__in IFunctionInstance *pFunctionInstance);

//
// The instance module of the WSD Challenge DLL (WSDCHNGR.DLL)
//
HMODULE m_hChallengeDll;

//
// Function pointer for public WSD Challenge APIs that are used by this driver
//
PFN_WSDCHNR_REGISTER_DEVICE_TO_CHALLENGE m_pfnRegisterDeviceToChallenge;
PFN_WSDCHNR_INITIALIZE m_pfnInitializeChallenge;
PFN_WSDCHNR_SHUTDOWN m_pfnShutdownChallenge;
```

 

 




