---
Description: 属性-值检索
title: 属性-值检索
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab9ceae3b642ececd2ad222bf9f2a3dbfd12f3db
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350224"
---
# <a name="property-value-retrieval"></a>属性-值检索


当 WPD 程序调用**IPortableDeviceProperties::GetValues**方法，此方法，反过来，触发的一个调用**WpdObjectProperties::OnGetPropertyValues**或**WpdObjectProperties::OnGetAllPropertyValues**中的示例驱动程序的方法。 如果调用后一种方法的第二个参数**IPortableDeviceProperties::GetValues**是**NULL**。 这些方法的示例驱动程序中创建**IPortableDeviceValues**驱动程序将请求的属性的属性值存储到其中的对象。 下面的示例摘自示例驱动程序包含的代码**WpdObjectProperties::OnGetPropertyValues**方法。

```ManagedCPlusPlus
HRESULT WpdObjectProperties::OnGetPropertyValues(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr          = S_OK;
    LPWSTR  wszObjectID = NULL;
    CComPtr<IPortableDeviceValues>        pValues;
    CComPtr<IPortableDeviceKeyCollection> pKeys;

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the object identifier whose property values have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetStringValue(WPD_PROPERTY_OBJECT_PROPERTIES_OBJECT_ID, &wszObjectID);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_PROPERTIES_OBJECT_ID");
    }

    // Get the list of property keys for the property values the caller wants to retrieve from the specified object
    if (hr == S_OK)
    {
        hr = pParams->GetIPortableDeviceKeyCollectionValue(WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_KEYS, &pKeys);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_KEYS");
    }

    // CoCreate a collection to store the property values.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceValues,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceValues,
                              (VOID**) &pValues);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDeviceValues");
    }

    // Read the specified properties on the specified object and add the property values to the collection.
    if (hr == S_OK)
    {
        hr = GetPropertyValuesForObject(wszObjectID, pKeys, pValues);
        CHECK_HR(hr, "Failed to get property values for object '%ws'", wszObjectID);
    }

    // S_OK or S_FALSE can be returned from GetPropertyValuesForObject( ).
    // S_FALSE means that 1 or more property values could not be retrieved successfully.
    // The value for the specified property should be set to an error HRESULT of
    // the reason why the property could not be read.
    // (e.g. If the property being requested is not supported on the object then an error of
    // HRESULT_FROM_WIN32(ERROR_NOT_SUPPORTED) should be set as the value.
    if (SUCCEEDED(hr))
    {
        // Set the WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_VALUES value in the results.
        HRESULT hrTemp = S_OK;
        hrTemp = pResults->SetIPortableDeviceValuesValue(WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_VALUES, pValues);
        CHECK_HR(hrTemp, ("Failed to set WPD_PROPERTY_OBJECT_PROPERTIES_PROPERTY_VALUES"));

        if(FAILED(hrTemp))
        {
            hr = hrTemp;
        }
    }
```

 

 




