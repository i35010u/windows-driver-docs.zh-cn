---
description: 支持的内容-类型检索
title: 支持的内容-类型检索
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 816029f126cccafc06cab9fe4a62e43fb494ea9a
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969522"
---
# <a name="supported-content-type-retrieval"></a>支持的内容-类型检索


当 WPD 应用程序调用 **IPortableDeviceCapabilities：： GetSupportedContentTypes** 方法时，此方法将触发对示例驱动程序中的 **WpdCapabilities：： OnGetSupportedContentTypes** 方法的调用。 后一种方法会创建一个 **IPortableDevicePropVariantCollection** 对象，驱动程序会将其支持的内容类型存储在指定的功能类别中。  (如果驱动程序不支持给定功能类别的内容类型，则返回一个空集合。 ) 

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

 

 




