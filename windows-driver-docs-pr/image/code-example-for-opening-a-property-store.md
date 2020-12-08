---
title: 演示如何打开属性存储的代码示例
description: 演示如何打开属性存储的代码示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a7b9649feb907e1c3930799f744c1568d07ff18
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823191"
---
# <a name="code-example-for-opening-a-property-store"></a>演示如何打开属性存储的代码示例


下面的代码示例演示如何为当前函数实例对象打开属性存储。 获取 [函数实例对象](obtaining-a-function-instance-object.md)中介绍了获取当前函数实例对象的过程。

```cpp
/**************************************************************************\
* CWSDDevice::OpenPropertyStore
*
* Opens the Property Store that is associated with the current Function Instance. 
*
* Arguments:
*
*    pPropertyStore - returns the IPropertyStore interface. The caller must
*                     release it by calling IPropertyStore::Release
* Return Value:
*
*     S_OK if operation is successful, an error HRESULT otherwise
*
\**************************************************************************/

HRESULT
CWSDDevice::OpenPropertyStore(
    __out IPropertyStore **ppPropertyStore)
{
    HRESULT hr = S_OK;

    if (!ppPropertyStore)
    {
        hr = E_INVALIDARG;
        WIAS_ERROR((g_hInst, "Invalid argument, hr = 0x%08X", hr));
    }

    if (!m_pFunctionInstance)
    {
        hr = E_UNEXPECTED;
        WIAS_ERROR((g_hInst, "Communication interface not initialized, hr = 0x%08X", hr));
    }

    if (SUCCEEDED(hr))
    {
        hr = m_pFunctionInstance->OpenPropertyStore(STGM_READ, ppPropertyStore);
        if ((SUCCEEDED(hr)) && (!(*ppPropertyStore)))
        {
            hr = E_POINTER;
            WIAS_ERROR((g_hInst, 
                "IFunctionInstance::OpenPropertyStore returned hr = 0x%08X with a NULL property store interface, hr = 0x%08X", hr));
        }
        if (FAILED(hr))
        {
            WIAS_ERROR((g_hInst, "IFunctionInstance::OpenPropertyStore failed, hr = 0x%08X", hr));
        }
    }

    return hr;
}
```

 

 




