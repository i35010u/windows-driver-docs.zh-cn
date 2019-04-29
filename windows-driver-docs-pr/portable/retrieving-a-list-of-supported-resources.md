---
Description: 检索支持的资源的列表
title: 检索支持的资源的列表
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98ff05f45b7dfb4c46fe67a5f9c761453c43e0ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376225"
---
# <a name="retrieving-a-list-of-supported-resources"></a>检索支持的资源的列表


当应用程序需要检索给定对象支持的资源的列表时，它将调用**IPortableDeviceResources::GetSupportedResources**方法并传入一个字符串，指定对象的标识符中的问题。 此 API 调用，进而触发**WpdObjectResources::OnGetSupportedResources**命令处理程序中的示例驱动程序。 此方法创建**IPortableDeviceKeyCollection**对象支持的每个资源的 PROPERTYKEY 值复制到该命令。

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

 

 




