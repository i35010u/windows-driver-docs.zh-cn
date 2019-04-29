---
Description: 对功能命令 （WpdBasicHardwareDriver 示例） 的支持
title: 对功能命令 （WpdBasicHardwareDriver 示例） 的支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33c40f06cebbc17e6d45918cb502b4e4fc6b2930
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387301"
---
# <a name="support-for-capability-commands-wpdbasichardwaredriver-sample"></a>对功能命令 （WpdBasicHardwareDriver 示例） 的支持


示例驱动程序支持十个功能命令。 这些命令处理最初由**WpdCapabilities::DispatchMessage**方法，反过来，将调用相应的命令处理程序。 **DispatchMessage**方法和单个处理程序中找到*WpdCapabilities.cpp*文件。

下表中的信息描述了每个受支持的属性命令处理程序的名称以及该**DispatchMessage**处理给定的命令时调用。

| Command                                                            | 处理程序                        | 描述                                                                                                                                     |
|--------------------------------------------------------------------|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| WPD\_命令\_功能\_获取\_支持\_命令               | OnGetSupportedCommands         | 应用程序尝试检索的设备支持的命令集时，发出。                                           |
| WPD\_命令\_功能\_获取\_命令\_选项                  | OnGetCommandOptions            | 应用程序尝试检索受给定命令的选项时，发出。                                              |
| WPD\_命令\_功能\_获取\_支持\_功能\_类别 | OnGetFunctionalCategories      | 应用程序尝试检索的设备支持的功能类别组时，发出。                              |
| WPD\_命令\_功能\_获取\_功能\_对象               | OnGetFunctionalObjects         | 应用程序尝试检索受给定功能分类的函数对象的组时，发出。                |
| WPD\_命令\_功能\_获取\_支持\_内容\_类型         | OnGetSupportedContentTypes     | 应用程序尝试检索给定功能分类支持的内容类型时，发出。                            |
| WPD\_命令\_功能\_获取\_支持\_格式                | OnGetSupportedFormats          | 当应用程序尝试检索组的支持给定的内容类型的格式时发出。                                  |
| WPD\_命令\_功能\_获取\_支持\_格式\_属性     | OnGetSupportedFormatProperties | 应用程序尝试检索给定格式支持的属性集时，发出。                                     |
| WPD\_命令\_功能\_获取\_FIXED\_属性\_属性       | OnGetFixedPropertyAttributes   | 当应用程序尝试检索的属性完全相同 （或固定） 的属性集时，发出针对给定格式的所有对象。 |
| WPD\_命令\_功能\_获取\_事件\_选项                    | OnGetEventOptions              | 应用程序尝试检索与给定的事件相关联的选项时，发出。                                             |
| WPD\_命令\_功能\_获取\_支持\_事件                 | OnGetEventOptions              | 当应用程序尝试检索一组支持的设备的事件时发出。                                               |

 

示例驱动程序，该代码仍然保持不变以与以下命令相关联的处理程序：

-   WPD\_命令\_功能\_获取\_命令\_选项
-   WPD\_命令\_功能\_获取\_支持\_格式\_属性
-   WPD\_命令\_功能\_获取\_FIXED\_属性\_属性
-   WPD\_命令\_功能\_获取\_支持\_格式\_属性

但是，在代码中修改以下处理程序：

-   WPD\_命令\_功能\_获取\_支持\_命令
-   WPD\_命令\_功能\_获取\_支持\_功能\_类别
-   WPD\_命令\_功能\_获取\_功能\_对象
-   WPD\_命令\_功能\_获取\_支持\_内容\_类型
-   WPD\_命令\_功能\_获取\_支持\_格式
-   WPD\_命令\_功能\_获取\_支持\_事件
-   WPD\_命令\_功能\_获取\_事件\_选项

## <a name="span-idwpdcommandcapabilitiesgetsupportedcommandsspanspan-idwpdcommandcapabilitiesgetsupportedcommandsspanwpdcommandcapabilitiesgetsupportedcommands"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_COMMANDS"></span><span id="wpd_command_capabilities_get_supported_commands"></span>WPD\_命令\_功能\_获取\_支持\_命令


驱动程序调用**WpdObjectCapabilities::OnGetSupportedCommands**处理程序以响应 WPD\_命令\_功能\_获取\_支持\_命令的命令。 处理程序，反过来，返回有关受支持的命令标识符的数组。

虽然它已不需要修改该处理程序，已更新的开头显示的受支持的命令数组所要*WpdCapabilities.cpp*文件。 这些修改需要执行删除的对象资源类别的命令，因为传感器设备和驱动程序都不支持资源：

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

## <a name="span-idwpdcommandcapabilitiesgetsupportedfunctionalcategoriesspanspan-idwpdcommandcapabilitiesgetsupportedfunctionalcategoriesspanwpdcommandcapabilitiesgetsupportedfunctionalcategories"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FUNCTIONAL_CATEGORIES"></span><span id="wpd_command_capabilities_get_supported_functional_categories"></span>WPD\_命令\_功能\_获取\_支持\_功能\_类别


驱动程序调用**WpdObjectCapabilities::OnGetFunctionalCategories**处理程序以响应 WPD\_命令\_功能\_获取\_支持\_功能\_类别命令。 处理程序，反过来，返回有关受支持的类别的标识符的数组。

虽然它已不需要修改该处理程序，已更新的开头显示的受支持的类别数组所要*WpdCapabilities.cpp*文件。 删除存储类别并将它替换传感器类别，需要执行以下修改：

```cpp
const GUID g_SupportedFunctionalCategories[] =
{
    WPD_FUNCTIONAL_CATEGORY_DEVICE,
    FUNCTIONAL_CATEGORY_SENSOR_SAMPLE, // Our sensor's functional category  
};
```

示例驱动程序定义自定义功能类别 GUID (功能\_类别\_传感器\_示例) 来描述传感器功能对象。

## <a name="span-idwpdcommandcapabilitiesgetfunctionalobjectsspanspan-idwpdcommandcapabilitiesgetfunctionalobjectsspanwpdcommandcapabilitiesgetfunctionalobjects"></a><span id="WPD_COMMAND_CAPABILITIES_GET_FUNCTIONAL_OBJECTS"></span><span id="wpd_command_capabilities_get_functional_objects"></span>WPD\_命令\_功能\_获取\_功能\_对象


驱动程序调用**WpdObjectCapabilities::OnGetFunctionalObjects**处理程序以响应 WPD\_命令\_功能\_获取\_功能\_对象的命令。 处理程序，反过来，返回受支持的功能对象的标识符的数组。

对修改**OnGetFunctionalObjects**包含不再支持的存储对象，这不会包括在 WpdBasicHardwareDriver，以及增加对传感器对象支持的处理程序：

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

## <a name="span-idwpdcommandcapabilitiesgetsupportedcontenttypesspanspan-idwpdcommandcapabilitiesgetsupportedcontenttypesspanwpdcommandcapabilitiesgetsupportedcontenttypes"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_CONTENT_TYPES"></span><span id="wpd_command_capabilities_get_supported_content_types"></span>WPD\_命令\_功能\_获取\_支持\_内容\_类型


驱动程序调用**WpdObjectCapabilities::OnGetSupportedContentTypes**处理程序以响应 WPD\_命令\_功能\_获取\_支持\_内容\_类型命令。 因为传感器设备不支持的所有内容类型，此处理程序返回一个空集合。

对修改**OnGetSupportedContentTypes**处理程序包含 WpdHelloWorldSample 驱动程序的文档和文件夹的内容类型添加到返回的集合中删除代码：

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

## <a name="span-idwpdcommandcapabilitiesgetsupportedformatsspanspan-idwpdcommandcapabilitiesgetsupportedformatsspanwpdcommandcapabilitiesgetsupportedformats"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_FORMATS"></span><span id="wpd_command_capabilities_get_supported_formats"></span>WPD\_命令\_功能\_获取\_支持\_格式


驱动程序调用**WpdObjectCapabilities::OnGetSupportedFormats**处理程序以响应 WPD\_命令\_功能\_获取\_支持\_格式命令。 传感器设备不支持的所有内容类型，因为存在会被不受支持的格式。 因此，此处理程序也会返回一个空集合。

对修改**OnGetSupportedContentTypes**处理程序需要在添加到集合中的文本格式的 WpdHelloWorldSample 驱动程序中删除该代码。 文档内容类型已支持文本格式：

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

## <a name="span-idwpdcommandcapabilitiesgetsupportedeventsspanspan-idwpdcommandcapabilitiesgetsupportedeventsspanwpdcommandcapabilitiesgetsupportedevents"></a><span id="WPD_COMMAND_CAPABILITIES_GET_SUPPORTED_EVENTS"></span><span id="wpd_command_capabilities_get_supported_events"></span>WPD\_命令\_功能\_获取\_支持\_事件


驱动程序调用**WpdObjectCapabilities::OnGetSupportedEvents**处理程序以响应 WPD\_命令\_功能\_获取\_支持\_事件命令。 因为传感器设备支持自定义传感器读数已更新的事件 (事件\_传感器\_读取\_更新)，需要更新的源文件。

第一次修改涉及到添加 g\_SupportedEvents 数组，其中包含一个支持事件的标识符：

```cpp
const GUID g_SupportedEvents[] =
{
    EVENT_SENSOR_READING_UPDATED,
};
```

第二个修改为**OnGetSupportedEvents**处理程序中，涉及到添加填充支持的事件集合的代码：

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

## <a name="span-idwpdcommandcapabilitiesgeteventoptionsspanspan-idwpdcommandcapabilitiesgeteventoptionsspanwpdcommandcapabilitiesgeteventoptions"></a><span id="WPD_COMMAND_CAPABILITIES_GET_EVENT_OPTIONS"></span><span id="wpd_command_capabilities_get_event_options"></span>WPD\_命令\_功能\_获取\_事件\_选项


驱动程序调用**WpdObjectCapabilities::OnGetEventOptions**处理程序以响应 WPD\_命令\_功能\_获取\_事件\_选项命令。 传感器设备支持更新读取事件，它是广播的事件，因为它是需要添加一个标志，指示，此选项 (WPD\_事件\_选项\_IS\_广播\_事件) 是 **，则返回 TRUE**:

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





