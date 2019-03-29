---
Description: 功能-类别检索
title: 功能-类别检索
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2703ee629fc030a754d98fcf2a6e7e974585d9ee
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349426"
---
# <a name="functional-category-retrieval"></a>功能-类别检索


当 WPD 程序调用**IPortableDeviceCapabilities::GetFunctionalCategories**方法，此方法，反过来，触发调用**WpdCapabilities::OnGetFunctionalCategories**中的示例驱动程序的方法。 该方法将创建**IPortableDevicePropVariantCollection**驱动程序将两个受支持的类别存储到其中的对象 (WPD\_功能\_类别\_设备和 WPD\_功能\_类别\_存储)。

```ManagedCPlusPlus
HRESULT WpdCapabilities::OnGetFunctionalCategories(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr = S_OK;
    CComPtr<IPortableDevicePropVariantCollection> pFunctionalCategories;

    UNREFERENCED_PARAMETER(pParams);

    // CoCreate a collection to store the supported functional categories.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDevicePropVariantCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDevicePropVariantCollection,
                              (VOID**) &pFunctionalCategories);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDevicePropVariantCollection");
    }

    // Add the supported functional categories to the collection.
    if (hr == S_OK)
    {
        for (DWORD dwIndex = 0; dwIndex < ARRAYSIZE(g_SupportedFunctionalCategories); dwIndex++)
        {
            PROPVARIANT pv = {0};
            PropVariantInit(&pv);
            // Don't call PropVariantClear, since we did not allocate the memory for these GUIDs

            pv.vt    = VT_CLSID;
            pv.puuid = (GUID*) &g_SupportedFunctionalCategories[dwIndex];

            hr = pFunctionalCategories->Add(&pv);
            CHECK_HR(hr, "Failed to add supported functional category at index %d", dwIndex);
            if (FAILED(hr))
            {
                break;
            }
        }
    }

    // Set the WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORIES value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORIES, pFunctionalCategories);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORIES");
    }

    return hr;
}
```

 

 




