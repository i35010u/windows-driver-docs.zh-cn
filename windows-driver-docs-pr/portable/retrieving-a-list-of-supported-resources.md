---
description: 检索支持的资源的列表
title: 检索支持的资源的列表
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd73fcd83b4710eac5fa07171f2685a61a4e5008
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969464"
---
# <a name="retrieving-a-list-of-supported-resources"></a>检索支持的资源的列表


当应用程序需要检索给定对象支持的资源列表时，它将调用 **IPortableDeviceResources：： GetSupportedResources** 方法并传递一个字符串，该字符串指定了相关对象的标识符。 此 API 调用反过来会触发示例驱动程序中的 **WpdObjectResources：： OnGetSupportedResources** 命令处理程序。 此方法创建 **IPortableDeviceKeyCollection** 命令，该命令为对象支持的每个资源复制 PROPERTYKEY 值。

```ManagedCPlusPlus
HRESULT WpdObjectResources::OnGetSupportedResources(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{

    HRESULT hr           = S_OK;
    LPWSTR  wszObjectID  = NULL;

    CComPtr<IPortableDeviceKeyCollection> pKeys;

    // Get the Object ID
    hr = pParams->GetStringValue(WPD_PROPERTY_OBJECT_RESOURCES_OBJECT_ID, &wszObjectID);
    if (hr != S_OK)
    {
        hr = E_INVALIDARG;
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_RESOURCES_OBJECT_ID");
    }

    // Create the collection to hold the resource keys
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceKeyCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceKeyCollection,
                              (VOID**) &pKeys);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDeviceKeyCollection");
    }

    if (hr == S_OK)
    {
        hr = GetSupportedResourcesForObject(wszObjectID, pKeys);
        CHECK_HR(hr, "Failed to get supported resources for object '%ws'", wszObjectID);
    }

    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_OBJECT_RESOURCES_RESOURCE_KEYS, pKeys);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_OBJECT_RESOURCES_RESOURCE_KEYS");
    }

    // Free the memory.  CoTaskMemFree ignores NULLs so no need to check.
    CoTaskMemFree(wszObjectID);

    return hr;
}
```

 

 




