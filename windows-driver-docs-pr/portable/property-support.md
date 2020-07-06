---
Description: 属性支持
title: 属性支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 445700819101499437251fbaff795a6730994a74
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85967858"
---
# <a name="property-support"></a>属性支持


*WpdObjectProperties*和*WpdObjectProperties*文件包含用于在设备上设置和检索对象属性的成员函数。

当 Windows 应用程序调用**IPortableDeviceProperties**接口中的五种方法之一时，此调用反过来会触发**WpdObjectProperty**类中的五个命令处理程序之一。 下表标识了应用程序方法到**WpdObjectProperties**驱动程序方法的映射。

IPortableDeviceProperties 方法 * * * * *： **WpdObjectProperties 命令处理程序**

IPortableDeviceProperties：:D e) * * * *： **OnDelete**

IPortableDeviceProperties：： GetPropertyAttributes * * * *： **OnGetPropertyAttributes**

IPortableDeviceProperties：： GetSupportedProperties * * * *： **OnGetSupportedProperties**

IPortableDeviceProperties：： GetValues * * * *： **OnGetPropertyValues 或 OnGetAllPropertyValues**

IPortableDeviceProperties：： SetValues * * * *： **OnSetPropertyValues**


 

WpdObjectProperties 命令处理程序由**WpdObjectProperty：:D ispatchwpdmessage**方法调用。 示例驱动程序的以下摘录包含用于 WpdObjectProperty 的代码 **：:D ispatchwpdmessage：**

```ManagedCPlusPlus
HRESULT WpdObjectProperties::DispatchWpdMessage(
    const PROPERTYKEY&     Command,
    IPortableDeviceValues* pParams,
    IPortableDeviceValues* pResults)
{
    HRESULT hr = S_OK;

    if (hr == S_OK)
    {
        if (Command.fmtid != WPD_CATEGORY_OBJECT_PROPERTIES)
        {
            hr = E_INVALIDARG;
            CHECK_HR(hr, "This object does not support this command category %ws",CComBSTR(Command.fmtid));
        }
    }

    if (hr == S_OK)
    {
        if (IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_PROPERTIES_GET_SUPPORTED))
        {
            hr = OnGetSupportedProperties(pParams, pResults);
            CHECK_HR(hr, "Failed to get supported properties");
        }
        else if(IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_PROPERTIES_GET))
        {
            hr = OnGetPropertyValues(pParams, pResults);
            if(FAILED(hr))
            {
                CHECK_HR(hr, "Failed to get properties");
            }
        }
        else if(IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_PROPERTIES_GET_ALL))
        {
            hr = OnGetAllPropertyValues(pParams, pResults);
            if(FAILED(hr))
            {
                CHECK_HR(hr, "Failed to get all properties");
            }
        }
        else if(IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_PROPERTIES_SET))
        {
            hr = OnSetPropertyValues(pParams, pResults);
            if(FAILED(hr))
            {
                CHECK_HR(hr, "Failed to set properties");
            }
        }
        else if(IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_PROPERTIES_GET_ATTRIBUTES))
        {
            hr = OnGetPropertyAttributes(pParams, pResults);
            if(FAILED(hr))
            {
                CHECK_HR(hr, "Failed to get property attributes");
            }
        }
        else if(IsEqualPropertyKey(Command, WPD_COMMAND_OBJECT_PROPERTIES_DELETE))
        {
            hr = OnDeleteProperties(pParams, pResults);
            if(FAILED(hr))
            {
                CHECK_HR(hr, "Failed to delete properties");
            }
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

 

 




