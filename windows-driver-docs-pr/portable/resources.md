---
Description: 资源
title: 资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5baec576ec1941551f33e4962626cd1c13e5fbaa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376214"
---
# <a name="resources"></a>资源


*WpdObjectResources.cpp*并*WpdObjectResources.h*文件包含打开或关闭给定的资源、 读取资源的内容、 检索的特性的成员函数支持的资源，并检索给定对象支持的资源。

对于示例驱动程序，是位于文档文件夹对象内的单个资源 （示例自述文件文本文件）。

当基于 Windows 的应用程序调用中的方法之一**IPortableDeviceResources**接口，此调用，反过来，触发一个 WpdObjectResources 类中的多个命令处理程序。 下表列出了应用程序方法添加到 WpdObjectResource 方法的映射。

| WpdObjectResources 命令处理程序           | 描述                                                                                                                            |
|----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| WpdObjectResources::OnCloseResource          | 调用以响应关闭操作上**IStream**对象的**OnOpenResource**返回。                                    |
| WpdObjectResources::OnGetResourceAttributes。 | 调用以响应应用程序调用**IPortableDeviceResources::GetResourceAttributes**方法。                          |
| WpdObjectResources::OnGetSupportedResources  | 调用以响应应用程序调用**IPortableDeviceResources::GetSuportedResources**方法。                           |
| WpdObjectResources::OnOpenResource           | 调用以响应应用程序调用**IPortableDeviceResources::GetStream**方法。                                      |
| WpdObjectResources::OnReadResource           | 调用以响应应用程序调用**IStream::Read**方法**IStream**对象**OnOpenResource**返回。 |

 

通过调用 WpdObjectResources 命令处理程序**WpdObjectResources::DispatchWpdMessage**方法。 以下内容摘自示例驱动程序包含的代码**WpdObjectResources::DispatchWpdMessage**。

```ManagedCPlusPlus
HRESULT WpdObjectResources::DispatchWpdMessage(
    const PROPERTYKEY&     Command,
    IPortableDeviceValues* pParams,
    IPortableDeviceValues* pResults)
{
    HRESULT hr = S_OK;

    if (hr == S_OK)
    {
        if (Command.fmtid != WPD_CATEGORY_OBJECT_RESOURCES)
        {
            hr = E_INVALIDARG;
            CHECK_HR(hr, "This object does not support this command category %ws",CComBSTR(Command.fmtid));
        }
    }

    if (hr == S_OK)
    {
        if (IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_RESOURCES_GET_SUPPORTED))
        {
            hr = OnGetSupportedResources(pParams, pResults);
            CHECK_HR(hr, "Failed to get supported resources");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_RESOURCES_OPEN))
        {
            hr = OnOpenResource(pParams, pResults);
            CHECK_HR(hr, "Failed to open resource");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_RESOURCES_READ))
        {
            hr = OnReadResource(pParams, pResults);
            CHECK_HR(hr, "Failed to read resource");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_RESOURCES_CLOSE))
        {
            hr = OnCloseResource(pParams, pResults);
            CHECK_HR(hr, "Failed to close resource");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_RESOURCES_GET_ATTRIBUTES))
        {
            hr = OnGetResourceAttributes(pParams, pResults);
            CHECK_HR(hr, "Failed to get resource attributes");
        }
        else
        {
            hr = E_NOTIMPL;
            CHECK_HR(hr, "This object does not support this command id %d", Command.pid);
        }
    }
    return hr;
}
```

 

 




