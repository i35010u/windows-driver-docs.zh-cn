---
title: 演示如何质询可能已断开连接的设备的代码示例
description: 演示如何质询可能已断开连接的设备的代码示例
ms.assetid: 74633481-229f-4074-a84e-cc515eaaacd0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31638e6a26d664fb817ddd76228d915811329eb7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373214"
---
# <a name="code-example-for-challenging-a-potentially-disconnected-device"></a>演示如何质询可能已断开连接的设备的代码示例

> [!IMPORTANT]  
> WSD 占领功能已弃用，将在 2018年中删除所有与 WSD 占领相关文档。

下面的代码示例演示如何调用**RegisterDeviceToChallenge**函数 (这中的代码示例中列出[实现帮助器方法的示例代码](code-example-for-implementing-helper-methods.md)) 质询可能断开连接的设备。

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

 

 




