---
Description: 功能-对象检索
title: 功能-对象检索
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b04095aa98d365cc8dbd4109df8510033ab2efe
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348680"
---
# <a name="functional-object-retrieval"></a>功能-对象检索


当 WPD 程序调用**IPortableDeviceCapabilities::GetFunctionalObjects**方法，此方法，反过来，触发调用**WpdCapabilities::OnGetFunctionalObjects**中的方法示例驱动程序。 后一种方法创建**IPortableDevicePropVariantCollection**驱动程序将请求的功能对象存储到其中的对象。 对于示例驱动程序，支持只有两个对象类型：WPD\_设备\_对象\_ID 或存储\_对象\_id。 根据请求的功能类别，此方法可以返回一个或这两种类型。

```ManagedCPlusPlus
HRESULT WpdCapabilities::OnGetFunctionalObjects(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr                     = S_OK;
    GUID    guidFunctionalCategory = GUID_NULL;
    CComPtr<IPortableDevicePropVariantCollection> pFunctionalObjects;

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the functional category whose functional object identifiers have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORY, &guidFunctionalCategory);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORY");
    }

    // CoCreate a collection to store the supported functional object identifiers.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDevicePropVariantCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDevicePropVariantCollection,
                              (VOID**) &pFunctionalObjects);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDevicePropVariantCollection");
    }

    // Add the supported functional object identifiers for the specified functional
    // category to the collection.
    if (hr == S_OK)
    {
        PROPVARIANT pv = {0};
        PropVariantInit(&pv);
        // Don't call PropVariantClear, since we did not allocate the memory for these object identifiers

        // Add WPD_DEVICE_OBJECT_ID to the functional object identifiers collection
        if (hr == S_OK)
        {
            if ((guidFunctionalCategory  == WPD_FUNCTIONAL_CATEGORY_DEVICE) ||
                (guidFunctionalCategory  == WPD_FUNCTIONAL_CATEGORY_ALL))
            {
                pv.vt       = VT_LPWSTR;
                pv.pwszVal  = WPD_DEVICE_OBJECT_ID;
                hr = pFunctionalObjects->Add(&pv);
                CHECK_HR(hr, "Failed to add device object ID");
            }
        }

        // Add STORAGE_OBJECT_ID to the functional object identifiers collection
        if (hr == S_OK)
        {
            if ((guidFunctionalCategory  == WPD_FUNCTIONAL_CATEGORY_STORAGE) ||
                (guidFunctionalCategory  == WPD_FUNCTIONAL_CATEGORY_ALL))
            {
                pv.vt       = VT_LPWSTR;
                pv.pwszVal  = STORAGE_OBJECT_ID;
                hr = pFunctionalObjects->Add(&pv);
                CHECK_HR(hr, "Failed to add storage object ID");
            }
        }
    }

    // Set the WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_OBJECTS value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_OBJECTS, pFunctionalObjects);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_OBJECTS");
    }

    return hr;
}
```

 

 




