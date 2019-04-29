---
Description: 支持的内容-类型检索
title: 支持的内容-类型检索
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eadd713397859d635404ad4ea72447ab34e7712f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376205"
---
# <a name="supported-content-type-retrieval"></a>支持的内容-类型检索


当 WPD 程序调用**IPortableDeviceCapabilities::GetSupportedContentTypes**方法，此方法，反过来，触发调用**WpdCapabilities::OnGetSupportedContentTypes**中的示例驱动程序的方法。 后一种方法创建**IPortableDevicePropVariantCollection**驱动程序在其中存储的内容类型，它支持指定功能类别的对象。 （如果该驱动程序不支持给定功能类别的内容类型，它将返回一个空集合。）

```ManagedCPlusPlus
HRESULT WpdCapabilities::OnGetSupportedContentTypes(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr                     = S_OK;
    GUID    guidFunctionalCategory = GUID_NULL;
    CComPtr<IPortableDevicePropVariantCollection> pContentTypes;

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the functional category whose supported content types have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORY, &guidFunctionalCategory);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORY");
    }

    // CoCreate a collection to store the supported content types.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDevicePropVariantCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDevicePropVariantCollection,
                              (VOID**) &pContentTypes);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDevicePropVariantCollection");
    }

    // Add the supported content types for the specified functional
    // category to the collection.
    if (hr == S_OK)
    {
        PROPVARIANT pv = {0};
        PropVariantInit(&pv);
        // Don't call PropVariantClear, since we did not allocate the memory for these GUIDs

        // Add supported content types for known functional categories
        if (guidFunctionalCategory  == WPD_FUNCTIONAL_CATEGORY_STORAGE)
        {
            // Add WPD_CONTENT_TYPE_DOCUMENT to the supported content type collection
            pv.vt    = VT_CLSID;
            pv.puuid = (CLSID*)&WPD_CONTENT_TYPE_DOCUMENT;
            hr = pContentTypes->Add(&pv);
            CHECK_HR(hr, "Failed to add WPD_CONTENT_TYPE_DOCUMENT");

            if (hr == S_OK)
            {
                // Add WPD_CONTENT_TYPE_FOLDER to the supported content type collection
                pv.vt    = VT_CLSID;
                pv.puuid = (CLSID*)&WPD_CONTENT_TYPE_FOLDER;
                hr = pContentTypes->Add(&pv);
                CHECK_HR(hr, "Failed to add WPD_CONTENT_TYPE_FOLDER");
            }
        }
    }

    // Set the WPD_PROPERTY_CAPABILITIES_CONTENT_TYPES value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_CONTENT_TYPES, pContentTypes);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_CONTENT_TYPES");
    }

    return hr;
}
```

 

 




