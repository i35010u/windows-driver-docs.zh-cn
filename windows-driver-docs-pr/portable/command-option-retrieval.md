---
Description: 命令-选项检索
title: 命令-选项检索
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71fdeca565a37e86ad21543b95badb75cf0246e3
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349920"
---
# <a name="command-option-retrieval"></a>命令-选项检索


当 WPD 程序调用**IPortableDeviceCapabilities::GetCommandOptions**方法，此方法，反过来，触发调用**WpdCapabilities::OnGetCommandOptions**示例中的方法驱动程序。 后一种方法创建**IPortableDeviceValues**对象到其中的驱动程序会存储任何支持的选项。 因为示例驱动程序不支持命令选项，此方法返回的集合为空。

```ManagedCPlusPlus
HRESULT WpdCapabilities::OnGetCommandOptions(
    IPortableDeviceValues*  pParams,
    IPortableDeviceValues*  pResults)
{
    HRESULT     hr      = S_OK;
    PROPERTYKEY Command = WPD_PROPERTY_NULL;
    CComPtr<IPortableDeviceValues> pOptions;

    // First get ALL parameters for this command.  If we cannot get ALL parameters
    // then E_INVALIDARG should be returned and no further processing should occur.

    // Get the command whose options have been requested
    if (hr == S_OK)
    {
        hr = pParams->GetKeyValue(WPD_PROPERTY_CAPABILITIES_COMMAND, &Command);
        CHECK_HR(hr, "Missing value for WPD_PROPERTY_CAPABILITIES_COMMAND");
    }

    // CoCreate a collection to store the command options.
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceValues,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceValues,
                              (VOID**) &pOptions);
        CHECK_HR(hr, "Failed to CoCreateInstance CLSID_PortableDeviceValues");
    }

    // Add command options to the collection
    if (hr == S_OK)
    {
        // If your driver supports command options, then they should be added here
        // to the command options collection 'pOptions'.
    }

    // Set the WPD_PROPERTY_CAPABILITIES_COMMAND_OPTIONS value in the results.
    if (hr == S_OK)
    {
        hr = pResults->SetIUnknownValue(WPD_PROPERTY_CAPABILITIES_COMMAND_OPTIONS, pOptions);
        CHECK_HR(hr, "Failed to set WPD_PROPERTY_CAPABILITIES_COMMAND_OPTIONS");
    }

    return hr;
}
```

 

 




