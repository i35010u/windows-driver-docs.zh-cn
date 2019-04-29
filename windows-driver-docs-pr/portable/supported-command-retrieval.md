---
Description: 支持的命令检索
title: 支持的命令检索
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cee426cc7ae542818325e98cbf3411e368f2270a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376211"
---
# <a name="supported-command-retrieval"></a>支持的命令检索


当 WPD 程序调用**IPortableDeviceCapabilities::GetSupportedCommands**方法，此方法，反过来，触发调用**WpdCapabilities::OnGetSupportedCommands**中的方法示例驱动程序。 后一种方法创建**IPortableDeviceKeyCollection**驱动程序将支持的命令列表存储到其中的对象。 对于示例驱动程序，四个类别有 22 受支持的命令。

```ManagedCPlusPlus
const PROPERTYKEY g_SupportedCommands[] =
{
    // WPD_CATEGORY_OBJECT_ENUMERATION
    WPD_COMMAND_OBJECT_ENUMERATION_START_FIND,
    WPD_COMMAND_OBJECT_ENUMERATION_FIND_NEXT,
    WPD_COMMAND_OBJECT_ENUMERATION_END_FIND,

    // WPD_CATEGORY_OBJECT_PROPERTIES
    WPD_COMMAND_OBJECT_PROPERTIES_GET_SUPPORTED,
    WPD_COMMAND_OBJECT_PROPERTIES_GET,
    WPD_COMMAND_OBJECT_PROPERTIES_GET_ALL,
    WPD_COMMAND_OBJECT_PROPERTIES_SET,
    WPD_COMMAND_OBJECT_PROPERTIES_GET_ATTRIBUTES,
    WPD_COMMAND_OBJECT_PROPERTIES_DELETE,

    // WPD_CATEGORY_OBJECT_RESOURCES
    WPD_COMMAND_OBJECT_RESOURCES_GET_SUPPORTED,
    WPD_COMMAND_OBJECT_RESOURCES_OPEN,
    WPD_COMMAND_OBJECT_RESOURCES_READ,
    WPD_COMMAND_OBJECT_RESOURCES_CLOSE,
    WPD_COMMAND_OBJECT_RESOURCES_GET_ATTRIBUTES,

    // WPD_CATEGORY_CAPABILITIES
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_COMMANDS,
    WPD_COMMAND_CAPABILITIES_GET_COMMAND_OPTIONS,
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FUNCTIONAL_CATEGORIES,
    WPD_COMMAND_CAPABILITIES_GET_FUNCTIONAL_OBJECTS,
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_CONTENT_TYPES,
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FORMATS,
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FORMAT_PROPERTIES,
    WPD_COMMAND_CAPABILITIES_GET_FIXED_PROPERTY_ATTRIBUTES,
};
```

中的以下节选*WpdCapabilities.cpp*文件包含的代码**OnGetSupportedCommands**方法。

```ManagedCPlusPlus
HRESULT WpdCapabilities::OnGetSupportedCommands(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr = S_OK;
    CComPtr<IPortableDeviceKeyCollection> pCommands;
    UNREFERENCED_PARAMETER(pParams);

    // CoCreate a collection to store the supported commands.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceKeyCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceKeyCollection,
                              (VOID**) &pCommands);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDeviceKeyCollection");
    }

    // Add the supported commands to the collection.
    if (hr == S_OK)
    {
        for (DWORD dwIndex = 0; dwIndex < ARRAYSIZE(g_SupportedCommands); dwIndex++)
        {
            hr = pCommands->Add(g_SupportedCommands[dwIndex]);
            CHECK_HR(hr, "Failed to add supported command at index %d", dwIndex);
            if (FAILED(hr))
            {
                break;
            }
        }
    }

    // Set the WPD_PROPERTY_CAPABILITIES_SUPPORTED_COMMANDS value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_SUPPORTED_COMMANDS, pCommands);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_SUPPORTED_COMMANDS");
    }

    return hr;
}
```

 

 




