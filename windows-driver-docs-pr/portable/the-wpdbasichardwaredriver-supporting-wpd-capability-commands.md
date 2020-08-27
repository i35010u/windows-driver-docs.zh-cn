---
description: 支持 (WpdBasicHardwareDriver 示例) 的功能命令
title: 支持 (WpdBasicHardwareDriver 示例) 的功能命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 956140d9fba7f680d1c2edf6da5cc36d9743f265
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969450"
---
# <a name="support-for-capability-commands-wpdbasichardwaredriver-sample"></a>支持 (WpdBasicHardwareDriver 示例) 的功能命令


示例驱动程序支持十个功能命令。 这些命令最初由 **WpdCapabilities：:D ispatchmessage** 方法进行处理，该方法反过来会调用相应的命令处理程序。 在*WpdCapabilities*文件中可以找到**DispatchMessage**方法和单个处理程序。

下表中的信息介绍了每个受支持的属性命令，以及在处理给定命令时 **DispatchMessage** 调用的处理程序的名称。

| Command                                                            | Handler                        | 说明                                                                                                                                     |
|--------------------------------------------------------------------|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 支持的 \_ 命令               | OnGetSupportedCommands         | 当应用程序尝试检索设备支持的一组命令时发出。                                           |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 命令 \_ 选项                  | OnGetCommandOptions            | 当应用程序尝试检索给定命令支持的选项时发出。                                              |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 受支持的 \_ 功能 \_ 类别 | OnGetFunctionalCategories      | 当应用程序尝试检索设备支持的功能类别集时发出。                              |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 功能 \_ 对象               | OnGetFunctionalObjects         | 当应用程序尝试检索给定功能类别所支持的一组功能对象时发出。                |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 受支持的 \_ 内容 \_ 类型         | OnGetSupportedContentTypes     | 当应用程序尝试检索给定功能类别所支持的内容类型时发出。                            |
| WPD \_ 命令 \_ 功能 \_ 获得 \_ 支持的 \_ 格式                | OnGetSupportedFormats          | 当应用程序尝试检索给定内容类型支持的一组格式时发出。                                  |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 支持的 \_ 格式 \_ 属性     | OnGetSupportedFormatProperties | 当应用程序尝试检索给定格式支持的属性集时发出。                                     |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 固定 \_ 属性 \_ 特性       | OnGetFixedPropertyAttributes   | 当应用程序尝试检索与给定格式的所有对象 (或固定) 相同的属性属性集时发出。 |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 事件 \_ 选项                    | OnGetEventOptions              | 当应用程序尝试检索与给定事件关联的选项时发出。                                             |
| WPD \_ 命令 \_ 功能 \_ 获取 \_ 支持的 \_ 事件                 | OnGetEventOptions              | 当应用程序尝试检索设备支持的一组事件时发出。                                               |

 

对于示例驱动程序，代码在与以下命令相关联的处理程序中保持不变：

-   WPD \_ 命令 \_ 功能 \_ 获取 \_ 命令 \_ 选项
-   WPD \_ 命令 \_ 功能 \_ 获取 \_ 支持的 \_ 格式 \_ 属性
-   WPD \_ 命令 \_ 功能 \_ 获取 \_ 固定 \_ 属性 \_ 特性
-   WPD \_ 命令 \_ 功能 \_ 获取 \_ 支持的 \_ 格式 \_ 属性

但是，为以下处理程序修改了代码：

-   WPD \_ 命令 \_ 功能 \_ 获取 \_ 支持的 \_ 命令
-   WPD \_ 命令 \_ 功能 \_ 获取 \_ 受支持的 \_ 功能 \_ 类别
-   WPD \_ 命令 \_ 功能 \_ 获取 \_ 功能 \_ 对象
-   WPD \_ 命令 \_ 功能 \_ 获取 \_ 受支持的 \_ 内容 \_ 类型
-   WPD \_ 命令 \_ 功能 \_ 获得 \_ 支持的 \_ 格式
-   WPD \_ 命令 \_ 功能 \_ 获取 \_ 支持的 \_ 事件
-   WPD \_ 命令 \_ 功能 \_ 获取 \_ 事件 \_ 选项

## <a name="span-idwpd_command_capabilities_get_supported_commandsspanspan-idwpd_command_capabilities_get_supported_commandsspanwpd_command_capabilities_get_supported_commands"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_COMMANDS"></span><span id="wpd_command_capabilities_get_supported_commands"></span>WPD \_ 命令 \_ 功能 \_ 获取 \_ 支持的 \_ 命令


驱动程序调用 **WpdObjectCapabilities：： OnGetSupportedCommands** 处理程序来响应 WPD \_ 命令功能 " \_ \_ 获取支持的命令" \_ \_ 命令。 然后，处理程序返回支持的命令的标识符数组。

尽管不需要修改处理程序，但需要更新出现在 *WpdCapabilities* 文件开头的支持命令的数组。 这些修改引起删除命令的对象资源类别，因为传感器设备和驱动程序都不支持资源：

```cpp
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

    // WPD_CATEGORY_CAPABILITIES
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_COMMANDS,
    WPD_COMMAND_CAPABILITIES_GET_COMMAND_OPTIONS,
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FUNCTIONAL_CATEGORIES,
    WPD_COMMAND_CAPABILITIES_GET_FUNCTIONAL_OBJECTS,
    WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_EVENTS,  
    WPD_COMMAND_CAPABILITIES_GET_EVENT_OPTIONS,
};
```

## <a name="span-idwpd_command_capabilities_get_supported_functional_categoriesspanspan-idwpd_command_capabilities_get_supported_functional_categoriesspanwpd_command_capabilities_get_supported_functional_categories"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FUNCTIONAL_CATEGORIES"></span><span id="wpd_command_capabilities_get_supported_functional_categories"></span>WPD \_ 命令 \_ 功能 \_ 获取 \_ 受支持的 \_ 功能 \_ 类别


驱动程序调用 **WpdObjectCapabilities：： OnGetFunctionalCategories** 处理程序来响应 WPD \_ 命令功能 " \_ \_ 获取支持 \_ 的 \_ 功能 \_ 类别" 命令。 然后，处理程序返回支持的类别的标识符数组。

尽管不需要修改处理程序，但需要更新出现在 *WpdCapabilities* 文件开头的支持类别的数组。 这些修改引起删除存储类别，并将其替换为传感器类别：

```cpp
const GUID g_SupportedFunctionalCategories[] =
{
    WPD_FUNCTIONAL_CATEGORY_DEVICE,
    FUNCTIONAL_CATEGORY_SENSOR_SAMPLE, // Our sensor's functional category  
};
```

示例驱动程序定义了一个自定义功能类别 GUID (功能 \_ 类别 \_ 传感器 \_ 示例) 描述传感器功能对象。

## <a name="span-idwpd_command_capabilities_get_functional_objectsspanspan-idwpd_command_capabilities_get_functional_objectsspanwpd_command_capabilities_get_functional_objects"></a><span id="WPD_COMMAND_CAPABILITIES_GET_FUNCTIONAL_OBJECTS"></span><span id="wpd_command_capabilities_get_functional_objects"></span>WPD \_ 命令 \_ 功能 \_ 获取 \_ 功能 \_ 对象


驱动程序调用 **WpdObjectCapabilities：： OnGetFunctionalObjects** 处理程序来响应 WPD \_ 命令 \_ 功能 \_ 获取 \_ 功能 \_ 对象命令。 然后，处理程序返回受支持的功能对象的标识符数组。

对 **OnGetFunctionalObjects** 处理程序的修改包含删除对存储对象的支持，而不包括在 WpdBasicHardwareDriver 中，并且添加了对传感器对象的支持：

```cpp
HRESULT WpdCapabilities::OnGetFunctionalObjects(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr                     = S_OK;
    GUID    guidFunctionalCategory = GUID_NULL;
    CComPtr<IPortableDevicePropVariantCollection> pFunctionalObjects;

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the functional category whose functional object identifiers have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORY, &guidFunctionalCategory);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORY");
    }

    // CoCreate a collection to store the supported functional object identifiers.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDevicePropVariantCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDevicePropVariantCollection,
                              (VOID**) &pFunctionalObjects);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDevicePropVariantCollection");
    }

    // Add the supported functional object identifiers for the specified functional
    // category to the collection.
    if (hr == S_OK)
    {
        PROPVARIANT pv = {0};
        PropVariantInit(&pv);
        // Don't call PropVariantClear, since we did not allocate the memory for these object identifiers

        // Add WPD_DEVICE_OBJECT_ID to the functional object identifiers collection
        if (hr == S_OK)
        {
           
            if ((guidFunctionalCategory  == WPD_FUNCTIONAL_CATEGORY_DEVICE) ||
                (guidFunctionalCategory  == WPD_FUNCTIONAL_CATEGORY_ALL))
            {
                pv.vt       = VT_LPWSTR;
                pv.pwszVal  = WPD_DEVICE_OBJECT_ID;
                hr = pFunctionalObjects->Add(&pv);
                CHECK_HR(hr, "Failed to add device object ID");
            }
        }

        // Add FUNCTIONAL_CATEGORY_SENSOR_SAMPLE to the functional object 
        // identifiers collection
        if (hr == S_OK)
        {
            if ((guidFunctionalCategory  == FUNCTIONAL_CATEGORY_SENSOR_SAMPLE) ||
                (guidFunctionalCategory  == WPD_FUNCTIONAL_CATEGORY_ALL))
            {
                pv.vt       = VT_LPWSTR;
                pv.pwszVal  = SENSOR_OBJECT_ID;
                hr = pFunctionalObjects->Add(&pv);
                CHECK_HR(hr, "Failed to add sensor object ID");
            }
        }
    }

    // Set the WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_OBJECTS value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_OBJECTS, pFunctionalObjects);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_OBJECTS");
    }

    return hr;
}
```

## <a name="span-idwpd_command_capabilities_get_supported_content_typesspanspan-idwpd_command_capabilities_get_supported_content_typesspanwpd_command_capabilities_get_supported_content_types"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_CONTENT_TYPES"></span><span id="wpd_command_capabilities_get_supported_content_types"></span>WPD \_ 命令 \_ 功能 \_ 获取 \_ 受支持的 \_ 内容 \_ 类型


驱动程序调用 **WpdObjectCapabilities：： OnGetSupportedContentTypes** 处理程序来响应 WPD \_ 命令功能 " \_ \_ 获取支持 \_ 的 \_ 内容 \_ 类型" 命令。 由于传感器设备不支持任何内容类型，因此此处理程序返回一个空集合。

对 **OnGetSupportedContentTypes** 处理程序的修改包含删除 WpdHelloWorldSample 驱动程序中的代码，将文档和文件夹内容类型添加到返回的集合：

```cpp
HRESULT WpdCapabilities::OnGetSupportedContentTypes(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr                     = S_OK;
    GUID    guidFunctionalCategory = GUID_NULL;
    CComPtr<IPortableDevicePropVariantCollection> pContentTypes;

    // First get ALL parameters for this command. If we cannot get ALL parameters
    // then E_INVALIDARG should be returned 
    // and no further processing should occur.

    // Get the functional category whose supported content types 
    // have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORY, 
                                   &guidFunctionalCategory);
        CHECK_HR(hr, 
                 "Missing value for 
                  WPD_PROPERTY_CAPABILITIES_FUNCTIONAL_CATEGORY");
    }

    // CoCreate a collection to store the supported content types.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDevicePropVariantCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDevicePropVariantCollection,
                              (VOID**) &pContentTypes);
        CHECK_HR(hr, 
                 "Failed to CoCreate CLSID_PortableDevicePropVariantCollection");
    }

    // Set the WPD_PROPERTY_CAPABILITIES_CONTENT_TYPES value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_CONTENT_TYPES, 
                                        pContentTypes);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_CONTENT_TYPES");
    }

    return hr;
}
```

## <a name="span-idwpd_command_capabilities_get_supported_formatsspanspan-idwpd_command_capabilities_get_supported_formatsspanwpd_command_capabilities_get_supported_formats"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FORMATS"></span><span id="wpd_command_capabilities_get_supported_formats"></span>WPD \_ 命令 \_ 功能 \_ 获得 \_ 支持的 \_ 格式


驱动程序调用 **WpdObjectCapabilities：： OnGetSupportedFormats** 处理程序来响应 WPD \_ 命令功能 " \_ \_ 获取支持的格式" \_ \_ 命令。 由于传感器设备不支持任何内容类型，因此不支持任何格式。 因此，此处理程序还会返回一个空集合。

对 **OnGetSupportedContentTypes** 处理程序的修改涉及到删除 WpdHelloWorldSample 驱动程序中将文本格式添加到集合的代码。 文档内容类型支持文本格式：

```cpp
HRESULT WpdCapabilities::OnGetSupportedFormats(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr              = S_OK;
    GUID    guidContentType = GUID_NULL;
    CComPtr<IPortableDevicePropVariantCollection> pFormats;

    // First get ALL parameters for this command. If we cannot get ALL parameters
    // then E_INVALIDARG should be returned 
    // and no further processing should occur.

    // Get the content type whose supported formats have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_CAPABILITIES_CONTENT_TYPE, 
                                   &guidContentType);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_CAPABILITIES_CONTENT_TYPE");
    }

    // CoCreate a collection to store the supported formats.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDevicePropVariantCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDevicePropVariantCollection,
                              (VOID**) &pFormats);
        CHECK_HR(hr, "Failed to CoCreate CLSID_PortableDevicePropVariantCollection");
    }

    // Set the WPD_PROPERTY_CAPABILITIES_FORMATS value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_FORMATS, 
                                        pFormats);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_FORMATS");
    }

    return hr;
}
```

## <a name="span-idwpd_command_capabilities_get_supported_eventsspanspan-idwpd_command_capabilities_get_supported_eventsspanwpd_command_capabilities_get_supported_events"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_EVENTS"></span><span id="wpd_command_capabilities_get_supported_events"></span>WPD \_ 命令 \_ 功能 \_ 获取 \_ 支持的 \_ 事件


驱动程序调用 **WpdObjectCapabilities：： OnGetSupportedEvents** 处理程序来响应 WPD \_ 命令功能 " \_ \_ 获取支持的事件" \_ \_ 命令。 由于传感器设备支持自定义的传感器读取更新事件 (事件 \_ 感应器 \_ 读取 \_ 更新的事件) ，因此有必要更新源文件。

第一次修改涉及到添加一个 g \_ SupportedEvents 数组，其中包含一个受支持事件的标识符：

```cpp
const GUID g_SupportedEvents[] =
{
    EVENT_SENSOR_READING_UPDATED,
};
```

第二次修改到 **OnGetSupportedEvents** 处理程序，涉及添加填充支持的事件集合的代码：

```cpp
HRESULT WpdCapabilities::OnGetSupportedEvents(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr = S_OK;
    CComPtr<IPortableDevicePropVariantCollection> pEvents;
    UNREFERENCED_PARAMETER(pParams);

    // CoCreate a collection to store the supported events.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDevicePropVariantCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDevicePropVariantCollection,
                              (VOID**) &pEvents);
        CHECK_HR(hr, 
                 "Failed to CoCreate CLSID_PortableDevicePropVariantCollection");
    }

    // Add the supported events to the collection.
    if (hr == S_OK)
    {
        // populate the supported events collection
        for (DWORD dwIndex = 0; dwIndex < ARRAYSIZE(g_SupportedEvents); dwIndex++)
        {
            PROPVARIANT pv = {0};
            PropVariantInit(&pv);
            // Don't call PropVariantClear, 
            // since we did not allocate the memory for these GUIDs

            pv.vt    = VT_CLSID;
            pv.puuid = (GUID*) &g_SupportedEvents[dwIndex];

            hr = pEvents->Add(&pv);
            CHECK_HR(hr, "Failed to add supported event at index %d", dwIndex);
            if (FAILED(hr))
            {
                break;
            }
        }
    }

    // Set the WPD_PROPERTY_CAPABILITIES_SUPPORTED_EVENTS value in the results.
    if (hr == S_OK)
    {
        hr = pResults-> 
             SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_SUPPORTED_EVENTS, 
                              pEvents);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_SUPPORTED_EVENTS");
    }

    return hr;
}
```

## <a name="span-idwpd_command_capabilities_get_event_optionsspanspan-idwpd_command_capabilities_get_event_optionsspanwpd_command_capabilities_get_event_options"></a><span id="WPD_COMMAND_CAPABILITIES_GET_EVENT_OPTIONS"></span><span id="wpd_command_capabilities_get_event_options"></span>WPD \_ 命令 \_ 功能 \_ 获取 \_ 事件 \_ 选项


驱动程序调用 **WpdObjectCapabilities：： OnGetEventOptions** 处理程序来响应 WPD \_ 命令 \_ 功能 \_ 获取 \_ 事件 \_ 选项命令。 由于传感器设备支持读取更新事件（这是一个广播事件），因此有必要添加一个标志，指示此选项 (WPD \_ 事件 \_ 选项 \_ 是 \_ 广播 \_ 事件) 为 **TRUE**：

```cpp
HRESULT WpdCapabilities::OnGetEventOptions(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT hr    = S_OK;
    GUID    Event = GUID_NULL;
    CComPtr<IPortableDeviceValues> pOptions;

    // First get ALL parameters for this command. If we cannot get ALL parameters
    // then E_INVALIDARG should be returned 
    // and no further processing should occur.

    // Get the event whose options have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_CAPABILITIES_EVENT, &Event);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_CAPABILITIES_EVENT");
    }

    // CoCreate a collection to store the event options.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceValues,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceValues,
                              (VOID**) &pOptions);
        CHECK_HR(hr, "Failed to CoCreateInstance CLSID_PortableDeviceValues");
    }

    // Add event options to the collection
    if (hr == S_OK)
    {
        //  Check for the events we support
        if (Event == EVENT_ SENSOR_READING_UPDATED)
        {
            // These events are broadcast events
            hr = pOptions->SetBoolValue(WPD_EVENT_OPTION_IS_BROADCAST_EVENT, 
                                        TRUE);
            CHECK_HR(hr, "Failed to set WPD_EVENT_OPTION_IS_BROADCAST_EVENT");
        }
    }

    // Set the WPD_PROPERTY_CAPABILITIES_EVENT_OPTIONS value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_EVENT_OPTIONS, 
                                        pOptions);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_EVENT_OPTIONS");
    }

    return hr;
}
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





