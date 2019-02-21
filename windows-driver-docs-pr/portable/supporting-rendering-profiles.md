---
Description: Supporting Rendering Profiles
title: 支持呈现配置文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f63bf4649bc0e378f0784a6e4a51c63f13c0b47
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541437"
---
# <a name="supporting-rendering-profiles"></a>支持呈现配置文件


音频或视频设备可能支持特定呈现配置文件。 例如，音频流式处理设备可能通过多个通道流式特定类型的特定比特率的内容。 内容类型、 流式处理比特率和通道计数称为*呈现配置文件*。

WPD 应用程序通常将从驱动程序检索呈现配置文件。 有关如何应用程序中检索呈现配置文件的详细信息，请参阅[呈现功能支持的设备中检索](https://go.microsoft.com/fwlink/p/?linkid=150363)WPD SDK 中的主题。

本主题介绍如何 WpdWudfSampleDriver 驱动程序实现中的流式处理的音频支持*Helpers.cpp*模块。

当应用程序请求的呈现配置文件时，该驱动程序会收到 WPD\_命令\_对象\_属性\_GET 命令与命令类别的 WPD\_类别\_对象\_属性和 WPD\_属性\_对象\_属性\_对象\_RenderingInformation 的 ID。 在示例驱动程序，此命令的回执触发 SetRenderingProfile 函数中调用*Helpers.cpp*模块。

```ManagedCPlusPlus
HRESULT SetRenderingProfiles(
    IPortableDeviceValues*          pValues)
{
    HRESULT hr = S_OK;
    CComPtr<IPortableDeviceValues> pPreferredProfile;
    CComPtr<IPortableDeviceValues> pProfile2;

    CComPtr<IPortableDeviceValuesCollection> pProfiles;

    if(pValues == NULL)
    {
        hr = E_POINTER;
        CHECK_HR(hr, ("Cannot have NULL parameter"));
        return hr;
    }

    // Create the collection to hold the profiles
    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceValuesCollection,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceValuesCollection,
                              (VOID**) &pProfiles);
        CHECK_HR(hr, "Failed to CoCreateInstance CLSID_PortableDeviceValuesCollection");
    }

    // Get the preferred audio profile
    if (hr == S_OK)
    {
        hr = GetPreferredAudioProfile(&pPreferredProfile);
        CHECK_HR(hr, "Failed to get preferred audio profile properties");
    }

    // Add the profile
    if (hr == S_OK)
    {
        hr = pProfiles->Add(pPreferredProfile);
        CHECK_HR(hr, "Failed to add preferred audio profile to profile collection");
    }

    // Get the second audio profile
    if (hr == S_OK)
    {
        hr = GetAudioProfile2(&pProfile2);
        CHECK_HR(hr, "Failed to get second audio profile properties");
    }

    // Add the profile
    if (hr == S_OK)
    {
        hr = pProfiles->Add(pProfile2);
        CHECK_HR(hr, "Failed to add second audio profile to profile collection");
    }

    // Set the WPD_RENDERING_INFORMATION_PROFILES
    if (hr == S_OK)
    {
        hr = pValues->SetIPortableDeviceValuesCollectionValue(WPD_RENDERING_INFORMATION_PROFILES, pProfiles);
        CHECK_HR(hr, "Failed to set WPD_RENDERING_INFORMATION_PROFILES");
    }

    return hr;
}
```

**SetRenderingProfiles**函数，又调用 GetPreferredAudioProfile helper 函数在 IPortableDeviceValues 对象中返回的实际配置文件信息。

```ManagedCPlusPlus
HRESULT GetPreferredAudioProfile(
    IPortableDeviceValues** ppProfile)
{
    HRESULT hr = S_OK;
    CComPtr<IPortableDeviceValues> pProfile;

    if(ppProfile == NULL)
    {
        hr = E_POINTER;
        CHECK_HR(hr, ("Cannot have NULL parameter"));
        return hr;
    }

    if (hr == S_OK)
    {
        hr = CoCreateInstance(CLSID_PortableDeviceValues,
                              NULL,
                              CLSCTX_INPROC_SERVER,
                              IID_IPortableDeviceValues,
                              (VOID**) &pProfile);
        CHECK_HR(hr, "Failed to CoCreateInstance CLSID_PortableDeviceValues");
    }

    // Set the value for WPD_OBJECT_FORMAT to indicate this profile applies to WMA objects
    if (hr == S_OK)
    {
        hr = pProfile->SetGuidValue(WPD_OBJECT_FORMAT, WPD_OBJECT_FORMAT_WMA);
        CHECK_HR(hr, "Failed to set WPD_OBJECT_FORMAT");
    }

    // Set the preferred value for WPD_MEDIA_TOTAL_BITRATE
    if (hr == S_OK)
    {
        hr = pProfile->SetUnsignedIntegerValue(WPD_MEDIA_TOTAL_BITRATE, 192000);
        CHECK_HR(hr, "Failed to set WPD_MEDIA_TOTAL_BITRATE");
    }

    // Set the preferred value for WPD_AUDIO_CHANNEL_COUNT
    if (hr == S_OK)
    {
        hr = pProfile->SetUnsignedIntegerValue(WPD_AUDIO_CHANNEL_COUNT, 2);
        CHECK_HR(hr, "Failed to set WPD_AUDIO_CHANNEL_COUNT");
    }

    // Set the preferred value for WPD_AUDIO_FORMAT_CODE
    if (hr == S_OK)
    {
        hr = pProfile->SetUnsignedIntegerValue(WPD_AUDIO_FORMAT_CODE, WAVE_FORMAT_MSAUDIO3);
        CHECK_HR(hr, "Failed to set WPD_AUDIO_FORMAT_CODE");
    }

    // Set the output result
    if (hr == S_OK)
    {
        hr = pProfile->QueryInterface(IID_PPV_ARGS(ppProfile));
        CHECK_HR(hr, "Failed to QI for IPortableDeviceValues");
    }

    return hr;
}
```

 

 




