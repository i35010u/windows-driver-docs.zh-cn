---
Description: 属性支持
title: 属性支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a36aaa31b751f6672e97906fe6d8aa6c90e9e8c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376236"
---
# <a name="property-support"></a>属性支持


*WpdObjectProperties.cpp*并*WpdObjectProperties.h*文件包含设置和检索设备上的对象属性的成员函数。

当 Windows 应用程序调用中的五个方法之一**IPortableDeviceProperties**接口，此调用，进而触发中的五个命令处理程序之一**WpdObjectProperty**类。 下表列出了应用程序的方法的映射**WpdObjectProperties**驱动程序的方法。

|                                                       |                                                   |
|-------------------------------------------------------|---------------------------------------------------|
| **IPortableDeviceProperties 方法**                  | **WpdObjectProperties 命令处理程序**           |
| **IPortableDeviceProperties::Delete**                 | **OnDelete**                                      |
| **IPortableDeviceProperties::GetPropertyAttributes**  | **OnGetPropertyAttributes**                       |
| **IPortableDeviceProperties::GetSupportedProperties** | **OnGetSupportedProperties**                      |
| **IPortableDeviceProperties::GetValues**              | **OnGetPropertyValues 或 OnGetAllPropertyValues** |
| **IPortableDeviceProperties::SetValues**              | **OnSetPropertyValues**                           |

 

通过调用 WpdObjectProperties 命令处理程序**WpdObjectProperty::DispatchWpdMessage**方法。 以下内容摘自示例驱动程序包含的代码**WpdObjectProperty::DispatchWpdMessage:**

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

 

 




