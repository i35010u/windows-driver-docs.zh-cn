---
Description: Messaging Functionality
title: 消息传送功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa1d8d1c8f854bec2a99d6af4a2347f720c53990
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519788"
---
# <a name="messaging-functionality"></a>消息传送功能


消息传递函数**WpdBaseDriver::DispatchWpdMessage**，处理消息到相应的驱动程序组件的分布。 如果已进行编程之前的 Windows，您可以将**DispatchWpdMessage**函数与类似于基于 Windows 的应用程序**WindowProc**函数。

**WpdBaseDriver::DispatchWpdMessage**函数会检查 WPD\_命令类别来确定它应在其中发送给定的消息。 随后将传递到相应的组件 （枚举、 属性、 资源或功能中找到的组件驱动程序） 此消息。

*PParams*自变量指向**IPortableDeviceValues**集合，其中包含给定命令的反序列化的参数。

*PResults*自变量指向的空集合**IPortableDeviceValues**函数填充给定命令后进行处理。

以下内容摘自示例驱动程序包含的代码**WpdBaseDriver::DispatchWpdMessage。**

```ManagedCPlusPlus
HRESULT WpdBaseDriver::DispatchWpdMessage(IPortableDeviceValues* pParams,
                                          IPortableDeviceValues* pResults)
{

    HRESULT     hr                  = S_OK;
    GUID        guidCommandCategory = {0};
    DWORD       dwCommandID         = 0;
    PROPERTYKEY CommandKey          = WPD_PROPERTY_NULL;

    if (hr == S_OK)
    {
        hr = pParams->GetGuidValue(WPD_PROPERTY_COMMON_COMMAND_CATEGORY, &guidCommandCategory);
        CHECK_HR(hr, "Failed to get WPD_PROPERTY_COMMON_COMMAND_CATEGORY from input parameters");
    }

    if (hr == S_OK)
    {
        hr = pParams->GetUnsignedIntegerValue(WPD_PROPERTY_COMMON_COMMAND_ID, &dwCommandID);
        CHECK_HR(hr, "Failed to get WPD_PROPERTY_COMMON_COMMAND_ID from input parameters");
    }

    // If WPD_PROPERTY_COMMON_COMMAND_CATEGORY or WPD_PROPERTY_COMMON_COMMAND_ID could not be extracted
    // properly then we should return E_INVALIDARG to the client.
    if (FAILED(hr))
    {
        hr = E_INVALIDARG;
        CHECK_HR(hr, "Failed to get WPD_PROPERTY_COMMON_COMMAND_CATEGORY or WPD_PROPERTY_COMMON_COMMAND_ID from input parameters");
    }

    if (hr == S_OK)
    {
        CommandKey.fmtid = guidCommandCategory;
        CommandKey.pid   = dwCommandID;

        if (CommandKey.fmtid == WPD_CATEGORY_OBJECT_ENUMERATION)
        {
            hr = m_ObjectEnum.DispatchWpdMessage(CommandKey, pParams, pResults);
        }
        else if (CommandKey.fmtid == WPD_CATEGORY_OBJECT_PROPERTIES)
        {
            hr = m_ObjectProperties.DispatchWpdMessage(CommandKey, pParams, pResults);
        }
        else if (CommandKey.fmtid == WPD_CATEGORY_OBJECT_RESOURCES)
        {
            hr = m_ObjectResources.DispatchWpdMessage(CommandKey, pParams, pResults);
        }
        else if (CommandKey.fmtid == WPD_CATEGORY_CAPABILITIES)
        {
            hr = m_Capabilities.DispatchWpdMessage(CommandKey, pParams, pResults);
        }
        else if (IsEqualPropertyKey(CommandKey, WPD_COMMAND_COMMON_GET_OBJECT_IDS_FROM_PERSISTENT_UNIQUE_IDS))
        {
            hr = OnGetObjectIDsFromPersistentUniqueIDs(pParams, pResults);
        }
        else
        {
            hr = E_NOTIMPL;
            CHECK_HR(hr, "Unknown command %ws.%d received",CComBSTR(CommandKey.fmtid), CommandKey.pid);
        }
    }

    HRESULT hrTemp = pResults->SetErrorValue(WPD_PROPERTY_COMMON_HRESULT, hr);
    CHECK_HR(hrTemp, ("Failed to set WPD_PROPERTY_COMMON_HRESULT"));

    // Set to a success code, to indicate that the message was received.
    // the return code for the actual command&#39;s results is stored in the
    // WPD_PROPERTY_COMMON_HRESULT property.
    hr = S_OK;

    return hr;
}
```

 

 




