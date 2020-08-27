---
description: 检索资源特性
title: 检索资源特性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8aaf0561202d4117346d45d09b307dd75aa8555e
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969462"
---
# <a name="retrieving-resource-attributes"></a>检索资源特性


当应用程序需要检索给定资源支持的属性列表时，它会调用 **IPortableDeviceResources：： GetResourceAttributes** 方法，并传递一个字符串，该字符串指定了相关资源的标识符。 此 API 调用反过来会触发示例驱动程序中的 **WpdObjectResources：： OnGetResourceAttributes** 命令处理程序。 此方法将创建一个 **IPortableDeviceValues** 对象，该对象将为资源支持的每个属性插入 PROPERTYKEY/PROPVARIANT 对。

```ManagedCPlusPlus
HRESULT WpdObjectResources::OnGetResourceAttributes(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT     hr          = S_OK;
    LPWSTR      wszObjectID = NULL;
    PROPERTYKEY Key         = WPD_PROPERTY_NULL;
    CComPtr<IPortableDeviceValues>  pAttributes;

    if (hr == S_OK)
    {
        hr = pParams->GetStringValue(WPD_PROPERTY_OBJECT_RESOURCES_OBJECT_ID, &wszObjectID);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_RESOURCES_OBJECT_ID");
    }

    if (hr == S_OK)
    {
        hr = pParams->GetKeyValue(WPD_PROPERTY_OBJECT_RESOURCES_RESOURCE_KEYS, &Key);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_RESOURCES_RESOURCE_KEYS");
    }

    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceValues,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceValues,
                              (VOID**) &pAttributes);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDeviceValues");
    }

    if (hr == S_OK)
    {
        hr = GetResourceAttributesForObject(wszObjectID, Key, pAttributes);
        CHECK_HR(hr, "Failed to get resource attributes");
    }

    if (SUCCEEDED(hr))
    {
        HRESULT hrTemp = S_OK;

        hrTemp = pResults->SetIPortableDeviceValuesValue(WPD_PROPERTY_OBJECT_RESOURCES_RESOURCE_ATTRIBUTES, pAttributes);
        CHECK_HR(hrTemp, ("Failed to set WPD_PROPERTY_OBJECT_RESOURCES_RESOURCE_ATTRIBUTES"));

        if(FAILED(hrTemp))
        {
            hr = hrTemp;
        }
    }

    // Free the memory.  CoTaskMemFree ignores NULLs so no need to check.
    CoTaskMemFree(wszObjectID);

    return hr;
}
```

 

 




