---
description: 资源
title: 资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82ebf424826888130bd352f3c769ae4b442c77c9
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969466"
---
# <a name="resources"></a>资源


*WpdObjectResources*和*WpdObjectResources*文件包含成员函数，这些函数可以打开或关闭给定的资源，读取资源的内容，检索资源支持的属性，并检索给定对象支持的资源。

对于示例驱动程序，有一个资源 (文档文件夹对象中的示例自述文件) 。

当基于 Windows 的应用程序调用 **IPortableDeviceResources** 接口中的方法之一时，此调用反过来会触发 WpdObjectResources 类中的多个命令处理程序之一。 下表标识了应用程序方法与 WpdObjectResource 方法之间的映射。

| WpdObjectResources 命令处理程序           | 说明                                                                                                                            |
|----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| WpdObjectResources::OnCloseResource          | 调用以响应**OnOpenResource**返回的**IStream**对象上的关闭操作。                                    |
| WpdObjectResources::OnGetResourceAttributes. | 在响应调用 **IPortableDeviceResources：： GetResourceAttributes** 方法的应用程序时调用。                          |
| WpdObjectResources::OnGetSupportedResources  | 在响应调用 **IPortableDeviceResources：： GetSuportedResources** 方法的应用程序时调用。                           |
| WpdObjectResources::OnOpenResource           | 在响应调用 **IPortableDeviceResources：： system.resources.resourcemanager.getstream** 方法的应用程序时调用。                                      |
| WpdObjectResources::OnReadResource           | 在响应**OnOpenResource**返回的**istream**对象上调用**istream：： Read**方法的应用程序时调用。 |

 

WpdObjectResources 命令处理程序由 **WpdObjectResources：:D ispatchwpdmessage** 方法调用。 以下摘自示例驱动程序的代码包含 **WpdObjectResources：:D ispatchwpdmessage**的代码。

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

 

 




