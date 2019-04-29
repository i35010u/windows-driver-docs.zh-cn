---
Description: 关闭资源
title: 关闭资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 338a3dc252b900fe66163ba75dbf6c69ad146924
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378184"
---
# <a name="closing-a-resource"></a>关闭资源


应用程序通过使用完成读取或写入操作后给定**IStream**对象，它通过调用关闭流**IStream::Release**或**IStream::Commit**（若要保存更改资源的写入请求）。 在应用程序级别触发器的关闭请求**WpdObjectResources::OnCloseResource**驱动程序的方法。

主要工作**WpdObjectResources::OnCloseResource**方法是从客户端上下文映射中删除资源的上下文数据并释放关联的任何内存。

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

 

 




