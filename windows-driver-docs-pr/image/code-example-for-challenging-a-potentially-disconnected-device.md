---
title: 演示如何质询可能已断开连接的设备的代码示例
description: 演示如何质询可能已断开连接的设备的代码示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2366575b3d615ca5949abf2d574ed7ccbb41c1d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798173"
---
# <a name="code-example-for-challenging-a-potentially-disconnected-device"></a>演示如何质询可能已断开连接的设备的代码示例

> [!IMPORTANT]  
> 已弃用 WSD 争取冠军宝座功能，并且2018中将删除所有与 WSD 争取冠军宝座相关的文档。

下面的代码示例演示对 **RegisterDeviceToChallenge** 函数的调用 (该函数在用于 [实现帮助器方法的示例代码](code-example-for-implementing-helper-methods.md) 中列出，) 以质询可能断开连接的设备。

```cpp
HRESULT hr = S_OK;

if (SUCCEEDED(hr))
{
    //
    // Activate ScanProxy to retrieve the IScanService interface for it
    //
    hr = m_pFunctionInstance->QueryService(__uuidof(WSDScanProxy),
                                           __uuidof(IScanService),
                                           (void**) &m_pScanProxy);
    if (FAILED(hr))
    {
        WIAS_ERROR((g_hInst, "IFunctionInstance::QueryService(WSDScanProxy, IScanService) failed, cannot activate ScanProxy, hr = 0x%08X", hr));
 
        if (WSD_COMMUNICATION_ERROR(hr))
        {
            RegisterDeviceToChallenge();
        }
    }
}

if (SUCCEEDED(hr))
{
    //
    // Retrieve the IScanServiceEvents interface from the ScanProxy
    //
    hr = m_pScanProxy->QueryInterface(__uuidof(IScanServiceEvents), (void**)&m_pScanEvents);
    if (FAILED(hr))
    {
        WIAS_ERROR((g_hInst, "IScanService::QueryInterface(IScanServiceEvents) failed, hr = 0x%08X", hr));
 
        if (WSD_COMMUNICATION_ERROR(hr))
        {
            RegisterDeviceToChallenge();
        }
    }
}
```

 

 




