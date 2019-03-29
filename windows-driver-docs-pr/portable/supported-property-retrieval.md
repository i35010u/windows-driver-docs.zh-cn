---
Description: 支持的属性检索
title: 支持的属性检索
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a93b0e31aa3a7d511ff134de60fa21c76307e36
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350156"
---
# <a name="supported-property-retrieval"></a>支持的属性检索


当 WPD 程序调用**IPortableDeviceProperties::GetSupportedProperties**方法，此方法，反过来，触发调用**WpdObjectProperties::OnGetSupportedProperties**中的示例驱动程序的方法。 后一种方法创建**IPortableDeviceKeyCollection**驱动程序将属性存储到其中的对象为给定对象支持的属性的密钥。

```ManagedCPlusPlus
HRESULT WpdObjectProperties::OnGetSupportedProperties(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr          = S_OK;
    LPWSTR  wszObjectID = NULL;
    CComPtr<IPortableDeviceKeyCollection> pKeys;

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the object identifier whose supported properties have been requested
    hr = pParams->GetStringValue(WPD_PROPERTY_OBJECT_PROPERTIES_OBJECT_ID, &wszObjectID);
    if (hr != S_OK)
    {
        hr = E_INVALIDARG;
        CHECK_HR(hr, "Missing string value for WPD_PROPERTY_OBJECT_PROPERTIES_OBJECT_ID");
    }

    // CoCreate a collection to store the supported property keys.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceKeyCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceKeyCollection,
                              (VOID**) &pKeys);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDeviceKeyCollection");
    }

    // Add supported property keys for the specified object to the collection
    if (hr == S_OK)
    {
        hr = AddSupportedPropertyKeys(wszObjectID, pKeys);
        CHECK_HR(hr, "Failed to add supported property keys for object '%ws'", wszObjectID);
    }

    // Set the WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_KEYS value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIPortableDeviceKeyCollectionValue(WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_KEYS, pKeys);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_KEYS");
    }

    // Free the memory.  CoTaskMemFree ignores NULLs so no need to check.
    CoTaskMemFree(wszObjectID);

    return hr;
}
```

 

 




