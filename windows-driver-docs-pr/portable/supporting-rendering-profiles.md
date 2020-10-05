---
description: 支持呈现配置文件
title: 支持呈现配置文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c34db368980ac0435cf99dce3b976caf94238eb5
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732811"
---
# <a name="supporting-rendering-profiles"></a>支持呈现配置文件


音频或视频设备可能支持特定的渲染配置文件。 例如，音频流式处理设备可能会在多个通道上按特定比特率流式传输特定类型的内容。 内容类型、流式比特率和通道计数称为 *呈现配置文件*。

WPD 应用程序通常会从驱动程序中检索呈现配置文件。 有关应用程序如何检索呈现配置文件的详细信息，请参阅 WPD SDK 中的 [检索设备支持的呈现功能](/previous-versions//ms740263(v=vs.85)) 主题。

本主题介绍 WpdWudfSampleDriver 驱动程序如何实现对 *帮助程序 .cpp* 模块中音频流的支持。

当应用程序请求呈现配置文件时，驱动程序将接收 WPD \_ 命令 \_ 对象 \_ 属性 \_ GET 命令，其中包含 WPD 类别对象属性的命令类别 \_ \_ \_ 和 WPD \_ 属性 \_ 对象 \_ 属性 \_ 对象 \_ ID RenderingInformation。 在示例驱动程序中，此命令的接收将触发对 *SetRenderingProfile 模块中的* 函数的调用。

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

**SetRenderingProfiles**函数反过来调用 GetPreferredAudioProfile helper 函数，该函数将在 IPortableDeviceValues 对象中返回实际的配置文件信息。

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

 

