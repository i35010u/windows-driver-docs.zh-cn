---
description: 读取资源数据
title: 读取资源数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de7cb750d6f76e3a5c764b8c1eca8b7d50113d99
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968788"
---
# <a name="reading-resource-data"></a>读取资源数据


在应用程序检索到 **istream** 对象后，它可以通过使用 **IStream：： read** 或 **istream：： write** 方法执行所需的读取或写入操作。  (在示例驱动程序中，只支持读取操作) 。 当应用程序调用 **IStream：： Read** 方法时，此方法将触发对设备驱动程序的 **WpdObjectResources：： OnReadResource** 方法的调用，该方法执行实际的读取操作。

**WpdObjectResources：： OnReadResource**方法将请求的字节数读入目标缓冲区，然后用已传输的字节数更新资源上下文。

```ManagedCPlusPlus
HRESULT WpdObjectResources::OnReadResource(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT                   hr                 = S_OK;
    LPWSTR                    wszResourceContext = NULL;
    DWORD                     dwNumBytesToRead   = 0;
    DWORD                     dwNumBytesRead     = 0;
    BYTE*                     pBuffer            = NULL;
    DWORD                     cbBuffer           = 0;
    WpdObjectResourceContext* pResourceContext   = NULL;
    ContextMap*               pContextMap        = NULL;

    // Get the enumeration context identifier for this enumeration operation.  We will
    // need this to look up the specific enumeration context in the client context map.
    hr = pParams->GetStringValue(WPD_PROPERTY_OBJECT_RESOURCES_CONTEXT, &wszResourceContext);
    if (hr != S_OK)
    {
        hr = E_INVALIDARG;
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_RESOURCES_CONTEXT");
    }

    // Get the number of bytes to read
    if (hr == S_OK)
    {
        hr = pParams->GetUnsignedIntegerValue(WPD_PROPERTY_OBJECT_RESOURCES_NUM_BYTES_TO_READ, &dwNumBytesToRead);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_RESOURCES_NUM_BYTES_TO_READ");
    }

    // Get the destination buffer
    if (hr == S_OK)
    {
        hr = pParams->GetBufferValue(WPD_PROPERTY_OBJECT_RESOURCES_DATA, &pBuffer, &cbBuffer);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_RESOURCES_DATA");
    }

    // Get the client context map so we can retrieve the resource context for this resource
    // operation using the WPD_PROPERTY_OBJECT_RESOURCES_CONTEXT property value obtained above.
    if (hr == S_OK)
    {
        hr = pParams->GetIUnknownValue(PRIVATE_SAMPLE_DRIVER_CLIENT_CONTEXT_MAP, (IUnknown**)&pContextMap);
        CHECK_HR(hr, "Failed to get PRIVATE_SAMPLE_DRIVER_CLIENT_CONTEXT_MAP");
    }

    if (hr == S_OK)
    {
        pResourceContext = (WpdObjectResourceContext*)pContextMap->GetContext(wszResourceContext);
        if (pResourceContext == NULL)
        {
            hr = E_INVALIDARG;
            CHECK_HR(hr, "Missing resource context");
        }
    }

    // Read the next chunk of data for this request
    if (hr == S_OK)
    {
        hr = ReadDataFromResource(pResourceContext, pBuffer, dwNumBytesToRead, &dwNumBytesRead);
        CHECK_HR(hr, "Failed to read %d bytes from resource", dwNumBytesToRead);
    }

    if (hr == S_OK)
    {
        hr = pResults->SetBufferValue(WPD_PROPERTY_OBJECT_RESOURCES_DATA, pBuffer, dwNumBytesRead);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_OBJECT_RESOURCES_DATA");
    }

    if (hr == S_OK)
    {
        hr = pResults->SetUnsignedIntegerValue(WPD_PROPERTY_OBJECT_RESOURCES_NUM_BYTES_READ, dwNumBytesRead);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_OBJECT_RESOURCES_NUM_BYTES_READ");
    }

    // Free the memory.  CoTaskMemFree ignores NULLs so no need to check.
    CoTaskMemFree(wszResourceContext);

    // Free the memory.  CoTaskMemFree ignores NULLs so no need to check.
    CoTaskMemFree(pBuffer);

    SAFE_RELEASE(pContextMap);

    return hr;
}
```

 

 




