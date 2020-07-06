---
Description: 驱动程序功能
title: 驱动程序功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd4e0ef946c35f2b8a6cb29f7c44033db4cbf2f2
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968584"
---
# <a name="driver-capabilities"></a>驱动程序功能


*WpdCapabilities*和*WpdCapabilities*文件包含用于检索支持的命令、命令选项、函数类别等的命令处理程序。

当基于 Windows 的应用程序调用**IPortableDeviceCapabilities**接口中的方法之一时，此调用反过来会触发**WpdCapabilities**类中的八个命令处理程序之一。 下表标识了**IPortableDeviceCapabilities**方法到**WpdCapabilities**命令处理程序的映射。

IPortableDeviceCapabilities 方法 * * * * *： **WpdCapabilities 事件处理程序**

IPortableDeviceCapabilities：： GetCommandOptions * * * *： **OnGetCommandOptions**

IPortableDeviceCapabilities：： GetFixedPropertyAttributes * * * *： **OnGetFixedPropertyAttributes**

IPortableDeviceCapabilities：： GetFunctionalCategories * * * *： **OnGetFunctionalCategories**

IPortableDeviceCapabilities：： GetFunctionalObjects * * * *： **OnGetFunctionalObjects**

IPortableDeviceCapabilities：： GetSupportedCommands * * * *： **OnGetSupportedCommands**

IPortableDeviceCapabilities：： GetSupportedContentTypes * * * *： **OnGetSupportedContentTypes**

IPortableDeviceCapabilities：： GetSupportedFormatProperties * * * *： **OnGetSupportedFormatProperties**

IPortableDeviceCapabilities：： GetSupportedFormats * * * *： **OnGetSupportedFormats**

IPortableDeviceCapabilities：： GetSupportedEvents * * * *： **OnGetSupportedEvents**

IPortableDeviceCapabilities：： GetEventOptions * * * *： **OnGetEventOptions**


 

WpdCapabilities 命令处理程序由**WpdCapabilities：:D ispatchmessage**方法调用。 以下摘自示例驱动程序的代码包含**WpdCapabilities：:D ispatchmessage**的代码。

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

 

 




