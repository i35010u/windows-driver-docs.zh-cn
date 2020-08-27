---
description: 关闭资源
title: 关闭资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8051eebdfee8963b93de8f9a05a63b5ef3562dc
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969560"
---
# <a name="closing-a-resource"></a>关闭资源


在应用程序使用给定的 **IStream** 对象完成读取或写入操作后，它会通过调用 **Istream：： Release** 或 **IStream：： Commit** (关闭流，以便保存) 资源写入请求的更改。 应用程序级别的关闭请求会触发驱动程序的 **WpdObjectResources：： OnCloseResource** 方法。

**WpdObjectResources：： OnCloseResource**方法的主要工作是从客户端上下文映射中删除资源上下文数据，并释放任何关联的内存。

```ManagedCPlusPlus
HRESULT WpdObjectResources::OnCloseResource(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT     hr                 = S_OK;
    LPWSTR      wszResourceContext = NULL;
    ContextMap* pContextMap        = NULL;

    UNREFERENCED_PARAMETER(pResults);

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the resource context identifier for this resource operation.  We will
    // need this to look up the specific resource context in the client context map.
    hr = pParams->GetStringValue(WPD_PROPERTY_OBJECT_RESOURCES_CONTEXT, &wszResourceContext);
    if (hr != S_OK)
    {
        hr = E_INVALIDARG;
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_OBJECT_RESOURCES_CONTEXT");
    }

    // Get the client context map so we can retrieve the resource context for this resource
    // operation by using the WPD_PROPERTY_OBJECT_RESOURCES_CONTEXT property value obtained previously.
    if (hr == S_OK)
    {
        hr = pParams->GetIUnknownValue(PRIVATE_SAMPLE_DRIVER_CLIENT_CONTEXT_MAP, (IUnknown**)&pContextMap);
        CHECK_HR(hr, "Failed to get PRIVATE_SAMPLE_DRIVER_CLIENT_CONTEXT_MAP");
    }

    // Destroy any data, either allocated or associated, with the resource context and then remove it from the context map.
    // We no longer need to keep this context around because the resource operation has ended.
    if (hr == S_OK)
    {
        pContextMap->Remove(wszResourceContext);
    }

    // Free the memory.  CoTaskMemFree ignores NULLs so no need to check.
    CoTaskMemFree(wszResourceContext);

    SAFE_RELEASE(pContextMap);

    return hr;
}
```

 

 




