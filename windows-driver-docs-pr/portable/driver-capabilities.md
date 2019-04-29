---
Description: 驱动程序功能
title: 驱动程序功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5616504930a48c3c1f0dfc72deb75ee432e8d460
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378233"
---
# <a name="driver-capabilities"></a>驱动程序功能


*WpdCapabilities.cpp*并*WpdCapabilities.h*文件包含的命令处理程序检索受支持的命令、 命令选项，函数类别等。

当基于 Windows 的应用程序调用中的方法之一**IPortableDeviceCapabilities**接口，此调用，进而触发中的八个命令处理程序之一**WpdCapabilities**类。 下表列出了的映射**IPortableDeviceCapabilities**方法添加到**WpdCapabilities**命令处理程序。

|                                                               |                                    |
|---------------------------------------------------------------|------------------------------------|
| **IPortableDeviceCapabilities 方法**                        | **WpdCapabilities 事件处理程序**  |
| **IPortableDeviceCapabilities::GetCommandOptions**            | **OnGetCommandOptions**            |
| **IPortableDeviceCapabilities::GetFixedPropertyAttributes**   | **OnGetFixedPropertyAttributes**   |
| **IPortableDeviceCapabilities::GetFunctionalCategories**      | **OnGetFunctionalCategories**      |
| **IPortableDeviceCapabilities::GetFunctionalObjects**         | **OnGetFunctionalObjects**         |
| **IPortableDeviceCapabilities::GetSupportedCommands**         | **OnGetSupportedCommands**         |
| **IPortableDeviceCapabilities::GetSupportedContentTypes**     | **OnGetSupportedContentTypes**     |
| **IPortableDeviceCapabilities::GetSupportedFormatProperties** | **OnGetSupportedFormatProperties** |
| **IPortableDeviceCapabilities::GetSupportedFormats**          | **OnGetSupportedFormats**          |
| **IPortableDeviceCapabilities::GetSupportedEvents**           | **OnGetSupportedEvents**           |
| **IPortableDeviceCapabilities::GetEventOptions**              | **OnGetEventOptions**              |

 

通过调用 WpdCapabilities 命令处理程序**WpdCapabilities::DispatchMessage**方法。 以下内容摘自示例驱动程序包含的代码**WpdCapabilities::DispatchMessage**。

```ManagedCPlusPlus
HRESULT WpdCapabilities::DispatchWpdMessage(const PROPERTYKEY&      Command,
                                            IPortableDeviceValues*  pParams,
                                            IPortableDeviceValues*  pResults)
{
    HRESULT hr = S_OK;

    if (hr == S_OK)
    {
        if (Command.fmtid != WPD_CATEGORY_CAPABILITIES)
        {
            hr = E_INVALIDARG;
            CHECK_HR(hr, "This object does not support this command category %ws",CComBSTR(Command.fmtid));
        }
    }

    if (hr == S_OK)
    {
        if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_COMMANDS))
        {
            hr = OnGetSupportedCommands(pParams, pResults);
            CHECK_HR(hr, "Failed to get supported commands");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_COMMAND_OPTIONS))
        {
            hr = OnGetCommandOptions(pParams, pResults);
            CHECK_HR(hr, "Failed to get command options");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FUNCTIONAL_CATEGORIES))
        {
            hr = OnGetFunctionalCategories(pParams, pResults);
            CHECK_HR(hr, "Failed to get functional categories");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_FUNCTIONAL_OBJECTS))
        {
            hr = OnGetFunctionalObjects(pParams, pResults);
            CHECK_HR(hr, "Failed to get functional objects");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_CONTENT_TYPES))
        {
            hr = OnGetSupportedContentTypes(pParams, pResults);
            CHECK_HR(hr, "Failed to get supported content types");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FORMATS))
        {
            hr = OnGetSupportedFormats(pParams, pResults);
            CHECK_HR(hr, "Failed to get supported formats");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FORMAT_PROPERTIES))
        {
            hr = OnGetSupportedFormatProperties(pParams, pResults);
            CHECK_HR(hr, "Failed to get supported format properties");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_FIXED_PROPERTY_ATTRIBUTES))
        {
            hr = OnGetFixedPropertyAttributes(pParams, pResults);
            CHECK_HR(hr, "Failed to get fixed property attributes");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_EVENTS))
        {
            hr = OnGetSupportedEvents(pParams, pResults);
            CHECK_HR(hr, "Failed to get supported events");
        }
        else if (IsEqualPropertyKey(Command, WPD_COMMAND_CAPABILITIES_GET_EVENT_OPTIONS))
        {
            hr = OnGetEventOptions(pParams, pResults);
            CHECK_HR(hr, "Failed to get event options");
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

 

 




