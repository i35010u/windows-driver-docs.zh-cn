---
title: 在示例中使用的定义和变量
description: 在示例中使用的定义和变量
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9f149cc49d8b90adf41ec89aa9796782b796bfb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813775"
---
# <a name="definitions-and-variables-used-in-the-examples"></a>在示例中使用的定义和变量

> [!IMPORTANT]  
> 已弃用 WSD 争取冠军宝座功能，并且2018中将删除所有与 WSD 争取冠军宝座相关的文档。

下面的代码演示了在本部分的代码示例中使用的常量定义和常见变量。

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

 

 




