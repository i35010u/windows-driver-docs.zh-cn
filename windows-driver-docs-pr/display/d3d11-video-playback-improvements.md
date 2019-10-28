---
title: Direct3D 11 视频播放改进
description: 由于在主流应用中采用了 Microsoft Direct3D 10 技术的广泛采用，某些应用程序开发人员希望将所有内容视为相同。
ms.assetid: BB32F074-16E8-46E4-B9CF-6AEBE331B549
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4aefec16b91c6be2880a841816eefdef0d69302
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839769"
---
# <a name="direct3d-11-video-playback-improvements"></a>Direct3D 11 视频播放改进


由于在主流应用中采用了 Microsoft Direct3D 10 技术的广泛采用，某些应用程序开发人员希望将所有内容视为相同。 当通过 Direct3D 10 或 11 Api 处理全部二维和三维内容时，在 Microsoft Direct3D 9 API 上处理视频非常有挑战性。 由于 Windows 8 在 Microsoft Direct3D 11 上引入了视频，因此应用程序可以使用单个 API 来执行所有的图形操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">最小 Windows 显示器驱动程序模型（WDDM）版本</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">最大 Windows 版本</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">驱动程序实现-仅限完整图形和呈现</td>
<td align="left">所有 WDDM 1.2 驱动程序都是必需的，支持 Microsoft Direct3D 10、10.1-、11或11.1 的硬件（或更高版本）</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit">WHCK</a>要求和测试</td>
<td align="left"><p><strong>Device ¦ DX11 视频解码 FeatureLevel 9</strong></p>
<p><strong>Device ¦ DX11 VideoProcessing</strong></p></td>
</tr>
</tbody>
</table>

 

以下是使用 Direct3D 11 的主要优点：

-   Direct3D 11 视频简化了 Microsoft 媒体基础和 Microsoft DirectX 技术之间的互操作性。
-   使用多个 Api 更难进行编程，因此在 Direct3D 11 上使用视频可简化编程体验，并使应用更有效率。 API 在使用解码和处理的视频方面提供了更大的灵活性。
-   用于 stereoscopic 3-d 视频的 Direct3D 11 API 解压缩立体声帧转换为左对齐和右对齐图像。
-   它在解码和视频处理功能中具有 DirectX 视频加速（DXVA）2.0 和 DXVA 的奇偶校验。
-   它在会话0中适用于转码方案。

## <a name="span-iddirect3d_11_video_device_driver_interfaces__ddis_spanspan-iddirect3d_11_video_device_driver_interfaces__ddis_spanspan-iddirect3d_11_video_device_driver_interfaces__ddis_spandirect3d11-video-device-driver-interfaces-ddis"></a><span id="Direct3D_11_video_device_driver_interfaces__DDIs_"></span><span id="direct3d_11_video_device_driver_interfaces__ddis_"></span><span id="DIRECT3D_11_VIDEO_DEVICE_DRIVER_INTERFACES__DDIS_"></span>Direct3D 11 视频设备驱动程序接口（DDIs）


这些设备驱动程序接口（DDIs）是适用于 Windows 8 的新的或更新的：

-   [*CalcPrivateCryptoSessionSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatecryptosessionsize)
-   [*CalcPrivateAuthenticatedChannelSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivateauthenticatedchannelsize)
-   [*CalcPrivateVideoDecoderOutputViewSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideodecoderoutputviewsize)
-   [*CalcPrivateVideoDecoderSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideodecodersize)
-   [*CalcPrivateVideoProcessorEnumSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideoprocessorenumsize)
-   [*CalcPrivateVideoProcessorInputViewSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideoprocessorinputviewsize)
-   [*CalcPrivateVideoProcessorOutputViewSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideoprocessoroutputviewsize)
-   [*CalcPrivateVideoProcessorSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideoprocessorsize)
-   [*CheckFormatSupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkformatsupport)
-   [*CheckVideoDecoderFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_checkvideodecoderformat)
-   [*CheckVideoProcessorFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_checkvideoprocessorformat)
-   [*ConfigureAuthenticatedChannel （D3D11\_1）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_configureauthenticatedchannel)
-   [*CreateAuthenticatedChannel （D3D11\_1）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createauthenticatedchannel)
-   [*CreateCryptoSession*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createcryptosession)
-   [*CreateResource2*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2)
-   [*CreateVideoDecoder*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideodecoder)
-   [*CreateVideoDecoderOutputView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideodecoderoutputview)
-   [*CreateVideoProcessor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideoprocessor)
-   [*CreateVideoProcessorEnum*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideoprocessorenum)
-   [*CreateVideoProcessorInputView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideoprocessorinputview)
-   [*CreateVideoProcessorOutputView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideoprocessoroutputview)
-   [*CryptoSessionGetHandle*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_cryptosessiongethandle)
-   [*DecryptionBlt （D3D11\_1）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_decryptionblt)
-   [*DestroyAuthenticatedChannel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyauthenticatedchannel)
-   [*DestroyCryptoSession*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroycryptosession)
-   [*DestroyVideoDecoder*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideodecoder)
-   [*DestroyVideoDecoderOutputView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideodecoderoutputview)
-   [*DestroyVideoProcessor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideoprocessor)
-   [*DestroyVideoProcessorEnum*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideoprocessorenum)
-   [*DestroyVideoProcessorInputView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideoprocessorinputview)
-   [*DestroyVideoProcessorOutputView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideoprocessoroutputview)
-   [*EncryptionBlt （D3D11\_1）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_encryptionblt)
-   [*FinishSessionKeyRefresh*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_finishsessionkeyrefresh)
-   [*GetCaptureHandle*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcapturehandle)
-   [*Getcertificate 时出错*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcertificate)
-   [*GetCertificateSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcertificatesize)
-   [*GetContentProtectionCaps*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcontentprotectioncaps)
-   [*GetCryptoKeyExchangeType*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcryptokeyexchangetype)
-   [*GetEncryptionBltKey*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getencryptionbltkey)
-   [*GetVideoDecoderBufferInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderbufferinfo)
-   [*GetVideoDecoderBufferTypeCount*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderbuffertypecount)
-   [*GetVideoDecoderConfig*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderconfig)
-   [*GetVideoDecoderConfigCount*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderconfigcount)
-   [*GetVideoDecoderProfile*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderprofile)
-   [*GetVideoDecoderProfileCount*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderprofilecount)
-   [*GetVideoProcessorCaps*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideoprocessorcaps)
-   [*GetVideoProcessorCustomRate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideoprocessorcustomrate)
-   [*GetVideoProcessorFilterRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideoprocessorfilterrange)
-   [*GetVideoProcessorRateConversionCaps*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideoprocessorrateconversioncaps)
-   [*NegotiateAuthenticatedChannelKeyExchange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_negotiateauthenticatedchannelkeyexchange)
-   [*NegotiateCryptoSessionKeyExchange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_negotiatecryptosessionkeyeschange)
-   [*QueryAuthenticatedChannel （D3D11\_1）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_queryauthenticatedchannel)
-   [*RetrieveSubObject （D3D11\_1）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_retrievesubobject)
-   [*StartSessionKeyRefresh*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_startsessionkeyrefresh)
-   [*VideoDecoderBeginFrame*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecoderbeginframe)
-   [*VideoDecoderEndFrame*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecoderendframe)
-   [*VideoDecoderExtension*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecoderextension)
-   [*VideoDecoderGetHandle*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecodergethandle)
-   [*VideoDecoderSubmitBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecodersubmitbuffers)
-   [*VideoProcessorBlt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorblt)
-   [*VideoProcessorGetOutputExtension*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorgetoutputextension)
-   [*VideoProcessorGetStreamExtension*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorgetstreamextension)
-   [*VideoProcessorInputViewReadAfterWriteHazard*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorinputviewreadafterwritehazard)
-   [*VideoProcessorSetOutputAlphaFillMode*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputalphafillmode)
-   [*VideoProcessorSetOutputBackgroundColor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputbackgroundcolor)
-   [*VideoProcessorSetOutputColorSpace*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputcolorspace)
-   [*VideoProcessorSetOutputConstriction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputconstriction)
-   [*VideoProcessorSetOutputExtension*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputextension)
-   [*VideoProcessorSetOutputStereoMode*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputstereomode)
-   [*VideoProcessorSetOutputTargetRect*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputtargetrect)
-   [*VideoProcessorSetStreamAlpha*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamalpha)
-   [*VideoProcessorSetStreamAutoProcessingMode*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamautoprocessingmode)
-   [*VideoProcessorSetStreamColorSpace*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamcolorspace)
-   [*VideoProcessorSetStreamDestRect*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamdestrect)
-   [*VideoProcessorSetStreamExtension*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamextension)
-   [*VideoProcessorSetStreamFilter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamfilter)
-   [*VideoProcessorSetStreamFrameFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamframeformat)
-   [*VideoProcessorSetStreamLumaKey*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamlumakey)
-   [*VideoProcessorSetStreamOutputRate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamoutputrate)
-   [*VideoProcessorSetStreamPalette*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreampalette)
-   [*VideoProcessorSetStreamPixelAspectRatio*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreampixelaspectratio)
-   [*VideoProcessorSetStreamRotation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamrotation)
-   [*VideoProcessorSetStreamSourceRect*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamsourcerect)
-   [*VideoProcessorSetStreamStereoFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamstereoformat)
-   [**D3D10\_DDI\_资源\_绑定\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_resource_bind_flag)
-   [**D3D10\_DDI\_资源\_杂项\_标志**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_resource_misc_flag)
-   [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)
-   [**D3D11\_1DDI\_视频\_处理器\_ALPHA\_填充\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_alpha_fill_mode)
-   [**D3D11\_1DDI\_视频\_处理器\_自动\_流\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_auto_stream_caps)
-   [**D3D11\_1DDI\_视频\_处理器\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_caps)
-   [**D3D11\_1DDI\_视频\_处理器\_颜色\_空间**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_color_space)
-   [**D3D11\_1DDI\_视频\_处理器\_内容\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_content_desc)
-   [**D3D11\_1DDI\_视频\_处理器\_转换\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_conversion_caps)
-   [**D3D11\_1DDI\_视频\_处理器\_自定义\_速率**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_custom_rate)
-   [**D3D11\_1DDI\_视频\_处理器\_设备\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_device_caps)
-   [**D3D11\_1DDI\_视频\_处理器\_功能\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_feature_caps)
-   [**D3D11\_1DDI\_视频\_处理器\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_filter)
-   [**D3D11\_1DDI\_视频\_处理器\_筛选器\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_filter_caps)
-   [**D3D11\_1DDI\_视频\_处理器\_筛选器\_范围**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_filter_range)
-   [**D3D11\_1DDI\_视频\_处理器\_格式\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_format_caps)
-   [**D3D11\_1DDI\_视频\_处理器\_格式\_支持**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_format_support)
-   [**D3D11\_1DDI\_视频\_处理器\_ITELECINE\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_itelecine_caps)
-   [**D3D11\_1DDI\_视频\_处理器\_输出\_速率**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_output_rate)
-   [**D3D11\_1DDI\_视频\_处理器\_速率\_转换\_大写字母**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_rate_conversion_caps)
-   [**D3D11\_1DDI\_视频\_处理器\_旋转**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_rotation)
-   [**D3D11\_1DDI\_视频\_处理器\_立体声\_CAP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_stereo_caps)
-   [**D3D11\_1DDI\_视频\_处理器\_立体声\_翻转\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_stereo_flip_mode)
-   [**D3D11\_1DDI\_视频\_处理器\_立体声\_格式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_stereo_format)
-   [**D3D11\_1DDI\_视频\_处理器\_流**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_stream)
-   [**D3D11\_1DDI\_视频\_使用情况**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_usage)
-   [**D3D11\_1DDI\_VIDEODEVICEFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_videodevicefuncs)
-   [**D3D11\_1DDIARG\_CREATEAUTHENTICATEDCHANNEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createauthenticatedchannel)
-   [**D3D11\_1DDIARG\_CREATECRYPTOSESSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createcryptosession)
-   [**D3D11\_1DDIARG\_CREATEVIDEODECODER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideodecoder)
-   [**D3D11\_1DDIARG\_CREATEVIDEODECODEROUTPUTVIEW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideodecoderoutputview)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideoprocessor)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSORENUM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideoprocessorenum)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSORINPUTVIEW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideoprocessorinputview)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSOROUTPUTVIEW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideoprocessoroutputview)
-   [**D3D11\_1DDIARG\_\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_signature_entry)
-   [**D3D11\_1DDIARG\_阶段\_IO\_签名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_stage_io_signatures)
-   [**D3D11\_1DDIARG\_镶嵌\_IO\_签名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_tessellation_io_signatures)
-   [**D3D11\_1DDIARG\_VIDEODECODERBEGINFRAME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_videodecoderbeginframe)
-   [**D3D11\_1DDIARG\_VIDEODECODEREXTENSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_videodecoderextension)
-   [**D3D11\_DDI\_着色器\_最小\_精度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_ddi_shader_min_precision)
-   [**D3D11\_DDI\_着色器\_MIN\_精度\_支持\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_ddi_shader_min_precision_support_data)
-   [**D3D11\_DDI\_视频\_解码器\_缓冲区\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_ddi_video_decoder_buffer_type)
-   [**D3D11DDI\_HANDLETYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11ddi_handletype)
-   [**D3D11DDIARG\_CREATEDEFERREDCONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext)
-   [**D3D11DDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)
-   [**D3DDDI\_RESOURCEFLAGS2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags2)
-   [**D3DDDIARG\_CREATERESOURCE2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)
-   [**DXVAHDDDI\_旋转**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_rotation)
-   [**DXVAHDDDI\_流\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_stream_state)
-   [**DXVAHDDDI\_流\_状态\_旋转\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_stream_state_rotation_data)
-   [**DXVAHDDDI\_VPDEVCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)
-   [**FORMATOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_formatop)

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


所有 Windows 8 硬件上都需要 Direct3D 11 API 支持。

有关硬件设备实现此功能时必须满足的要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)，了解设备上的**¦ DX11 视频解码 FeatureLevel 9** **和¦ DX11 VideoProcessing。**

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)，了解 Windows 8 中添加的功能。

 

 





