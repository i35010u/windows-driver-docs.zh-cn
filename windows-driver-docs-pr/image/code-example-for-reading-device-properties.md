---
title: 演示如何读取设备属性的代码示例
description: 演示如何读取设备属性的代码示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 118e7bc1e9fc01daa5ee5d28e9ae5ac59be8c60e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823189"
---
# <a name="code-example-for-reading-device-properties"></a>演示如何读取设备属性的代码示例


下面的代码示例演示如何从属性存储区中读取设备属性。 有关如何为当前函数实例对象打开属性存储的示例，请参阅 [用于打开属性存储的代码示例](code-example-for-opening-a-property-store.md)。

```cpp
/**************************************************************************\
* CWSDDevice::ReadDeviceProperty
*
* Reads a LPWTSR device property from the device metadata and returns 
* a copy of its value as a BSTR character string. 
*
*
* Arguments:
*
*    pPropertyStore        - IPropertyStore interface, optional
*                            (if not specified a new property store
*                            Is opened and closed for each call)
*    pPropertyKey          - property key (for example, PKEY_PNPX_FirmwareVersion)
*    pbstrPropertyValue    - Returns the property value; this valuemust be 
*                            freed by caller using SysFreeString
*
* Return Value:
*
*     S_OK if operation is successful, an error HRESULT otherwise
*
\**************************************************************************/

HRESULT
CWSDDevice::ReadDeviceProperty(
    __in_opt IPropertyStore *pPropertyStore,
    __in const PROPERTYKEY  *pPropertyKey,
    __out BSTR              *pbstrPropertyValue)
{
    HRESULT hr = S_OK;
    IPropertyStore *pThisPropertyStore = NULL;
    BOOL bClosePropertyStore = FALSE;
    PROPVARIANT propvar = {0};

    if ((!pbstrPropertyValue) || (!pPropertyKey))
    {
        hr = E_INVALIDARG;
        WIAS_ERROR((g_hInst, "Invalid argument, hr = 0x%08X", hr));
    }

    if ((!m_pFunctionInstance) || (!m_pScanProxy))
    {
        hr = E_UNEXPECTED;
        WIAS_ERROR((g_hInst, "ScanProxy not initialized, hr = 0x%08X", hr));
    }

    if (SUCCEEDED(hr))
    {
        pThisPropertyStore = pPropertyStore;
 
        if (!pThisPropertyStore)
        {
            hr = m_pFunctionInstance->OpenPropertyStore(STGM_READ, &pThisPropertyStore);
            if ((SUCCEEDED(hr)) && (!pThisPropertyStore))
            {
                hr = E_POINTER;
                WIAS_ERROR((g_hInst, 
                    "IFunctionInstance::OpenPropertyStore returned hr = 0x%08X with a NULL property store interface, hr = 0x%08X", hr));
            }
            if (FAILED(hr))
            {
                WIAS_ERROR((g_hInst, "IFunctionInstance::OpenPropertyStore failed, hr = 0x%08X", hr));
            }

            if (pThisPropertyStore)
            {
                bClosePropertyStore = TRUE;
            }
        }    
    }
 
    PropVariantInit(&propvar);

    if (SUCCEEDED (hr))
    {
        hr = pThisPropertyStore->GetValue(*pPropertyKey, &propvar);
        if (FAILED(hr))
        {
            WIAS_ERROR((g_hInst, "IPropertyStore::GetValue failed, hr = 0x%08X", hr));
        }
    }

    if ((SUCCEEDED(hr)) && (VT_EMPTY == propvar.vt))
    {
        hr = E_FAIL;
        WIAS_ERROR((g_hInst, "IPropertyStore::GetValue returned no value (VT_EMPTY), hr = 0x%08X", hr));
    }

    if ((SUCCEEDED(hr)) && (VT_LPWSTR != propvar.vt))
    {
        hr = E_UNEXPECTED;
        WIAS_ERROR((g_hInst, "IPropertyStore::GetValue returned an unexpected PROPVARIANT type, hr = 0x%08X", hr));
    }

    if (SUCCEEDED (hr))
    {
        *pbstrPropertyValue = SysAllocString(propvar.pwszVal);
        if (!(*pbstrPropertyValue))
        {
            hr = E_OUTOFMEMORY;
            WIAS_ERROR((g_hInst, 
                "Cannot make a copy of the value returned by IPropertyStore::GetValue, %ws, hr = 0x%08X", propvar.pwszVal, hr));
        }
    }

    PropVariantClear(&propvar);

    if ((bClosePropertyStore) && (pThisPropertyStore))
    {
        pThisPropertyStore->Release();
        pThisPropertyStore = NULL;
    }

    return hr;
}
```

 

 




