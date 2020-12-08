---
title: Direct3D 11 视频播放改进
description: 由于在主流应用中采用了 Microsoft Direct3D 10 技术的广泛采用，某些应用程序开发人员希望将所有内容视为相同。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e879bc4ebc17a4f3547ac9fc776295dd9444152
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838507"
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
<td align="left">最小 Windows 显示器驱动程序模型 (WDDM) 版本</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">最大 Windows 版本</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">驱动程序实现-仅限完整图形和呈现</td>
<td align="left">所有 WDDM 1.2 驱动程序都是必需的，其中包含支持 Microsoft Direct3D 10、10.1、11或11.1 的硬件 (或更高版本) </td>
</tr>
<tr class="even">
<td align="left"><a href="/windows-hardware/test/hlk/windows-hardware-lab-kit">WHCK</a> 要求和测试</td>
<td align="left"><p><strong>Device ¦ DX11 视频解码 FeatureLevel 9</strong></p>
<p><strong>Device ¦ DX11 VideoProcessing</strong></p></td>
</tr>
</tbody>
</table>

 

以下是使用 Direct3D 11 的主要优点：

-   Direct3D 11 视频简化了 Microsoft 媒体基础和 Microsoft DirectX 技术之间的互操作性。
-   使用多个 Api 更难进行编程，因此在 Direct3D 11 上使用视频可简化编程体验，并使应用更有效率。 API 在使用解码和处理的视频方面提供了更大的灵活性。
-   用于 stereoscopic 3-d 视频的 Direct3D 11 API 解压缩立体声帧转换为左对齐和右对齐图像。
-   它在解码和视频处理功能中具有 DirectX 视频加速 (DXVA) 2.0 和 DXVA 的奇偶校验。
-   它在会话0中适用于转码方案。

## <a name="span-iddirect3d_11_video_device_driver_interfaces__ddis_spanspan-iddirect3d_11_video_device_driver_interfaces__ddis_spanspan-iddirect3d_11_video_device_driver_interfaces__ddis_spandirect3d-11-video-device-driver-interfaces-ddis"></a><span id="Direct3D_11_video_device_driver_interfaces__DDIs_"></span><span id="direct3d_11_video_device_driver_interfaces__ddis_"></span><span id="DIRECT3D_11_VIDEO_DEVICE_DRIVER_INTERFACES__DDIS_"></span>Direct3D 11 视频设备驱动程序接口 (DDIs) 


这些设备驱动程序接口 (适用于 Windows 8 的新的或更新的 DDIs) ：

-   [*CalcPrivateCryptoSessionSize*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatecryptosessionsize)
-   [*CalcPrivateAuthenticatedChannelSize*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivateauthenticatedchannelsize)
-   [*CalcPrivateVideoDecoderOutputViewSize*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideodecoderoutputviewsize)
-   [*CalcPrivateVideoDecoderSize*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideodecodersize)
-   [*CalcPrivateVideoProcessorEnumSize*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideoprocessorenumsize)
-   [*CalcPrivateVideoProcessorInputViewSize*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideoprocessorinputviewsize)
-   [*CalcPrivateVideoProcessorOutputViewSize*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideoprocessoroutputviewsize)
-   [*CalcPrivateVideoProcessorSize*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideoprocessorsize)
-   [*CheckFormatSupport*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkformatsupport)
-   [*CheckVideoDecoderFormat*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_checkvideodecoderformat)
-   [*CheckVideoProcessorFormat*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_checkvideoprocessorformat)
-   [*ConfigureAuthenticatedChannel (D3D11 \_ 1)*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_configureauthenticatedchannel)
-   [*CreateAuthenticatedChannel (D3D11 \_ 1)*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createauthenticatedchannel)
-   [*CreateCryptoSession*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createcryptosession)
-   [*CreateResource2*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2)
-   [*CreateVideoDecoder*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideodecoder)
-   [*CreateVideoDecoderOutputView*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideodecoderoutputview)
-   [*CreateVideoProcessor*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideoprocessor)
-   [*CreateVideoProcessorEnum*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideoprocessorenum)
-   [*CreateVideoProcessorInputView*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideoprocessorinputview)
-   [*CreateVideoProcessorOutputView*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideoprocessoroutputview)
-   [*CryptoSessionGetHandle*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_cryptosessiongethandle)
-   [*DecryptionBlt (D3D11 \_ 1)*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_decryptionblt)
-   [*DestroyAuthenticatedChannel*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyauthenticatedchannel)
-   [*DestroyCryptoSession*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroycryptosession)
-   [*DestroyVideoDecoder*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideodecoder)
-   [*DestroyVideoDecoderOutputView*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideodecoderoutputview)
-   [*DestroyVideoProcessor*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideoprocessor)
-   [*DestroyVideoProcessorEnum*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideoprocessorenum)
-   [*DestroyVideoProcessorInputView*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideoprocessorinputview)
-   [*DestroyVideoProcessorOutputView*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideoprocessoroutputview)
-   [*EncryptionBlt (D3D11 \_ 1)*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_encryptionblt)
-   [*FinishSessionKeyRefresh*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_finishsessionkeyrefresh)
-   [*GetCaptureHandle*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcapturehandle)
-   [*Getcertificate 时出错*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcertificate)
-   [*GetCertificateSize*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcertificatesize)
-   [*GetContentProtectionCaps*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcontentprotectioncaps)
-   [*GetCryptoKeyExchangeType*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcryptokeyexchangetype)
-   [*GetEncryptionBltKey*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getencryptionbltkey)
-   [*GetVideoDecoderBufferInfo*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderbufferinfo)
-   [*GetVideoDecoderBufferTypeCount*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderbuffertypecount)
-   [*GetVideoDecoderConfig*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderconfig)
-   [*GetVideoDecoderConfigCount*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderconfigcount)
-   [*GetVideoDecoderProfile*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderprofile)
-   [*GetVideoDecoderProfileCount*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderprofilecount)
-   [*GetVideoProcessorCaps*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideoprocessorcaps)
-   [*GetVideoProcessorCustomRate*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideoprocessorcustomrate)
-   [*GetVideoProcessorFilterRange*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideoprocessorfilterrange)
-   [*GetVideoProcessorRateConversionCaps*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideoprocessorrateconversioncaps)
-   [*NegotiateAuthenticatedChannelKeyExchange*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_negotiateauthenticatedchannelkeyexchange)
-   [*NegotiateCryptoSessionKeyExchange*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_negotiatecryptosessionkeyeschange)
-   [*QueryAuthenticatedChannel (D3D11 \_ 1)*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_queryauthenticatedchannel)
-   [*RetrieveSubObject (D3D11 \_ 1)*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_retrievesubobject)
-   [*StartSessionKeyRefresh*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_startsessionkeyrefresh)
-   [*VideoDecoderBeginFrame*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecoderbeginframe)
-   [*VideoDecoderEndFrame*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecoderendframe)
-   [*VideoDecoderExtension*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecoderextension)
-   [*VideoDecoderGetHandle*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecodergethandle)
-   [*VideoDecoderSubmitBuffers*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecodersubmitbuffers)
-   [*VideoProcessorBlt*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorblt)
-   [*VideoProcessorGetOutputExtension*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorgetoutputextension)
-   [*VideoProcessorGetStreamExtension*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorgetstreamextension)
-   [*VideoProcessorInputViewReadAfterWriteHazard*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorinputviewreadafterwritehazard)
-   [*VideoProcessorSetOutputAlphaFillMode*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputalphafillmode)
-   [*VideoProcessorSetOutputBackgroundColor*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputbackgroundcolor)
-   [*VideoProcessorSetOutputColorSpace*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputcolorspace)
-   [*VideoProcessorSetOutputConstriction*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputconstriction)
-   [*VideoProcessorSetOutputExtension*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputextension)
-   [*VideoProcessorSetOutputStereoMode*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputstereomode)
-   [*VideoProcessorSetOutputTargetRect*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputtargetrect)
-   [*VideoProcessorSetStreamAlpha*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamalpha)
-   [*VideoProcessorSetStreamAutoProcessingMode*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamautoprocessingmode)
-   [*VideoProcessorSetStreamColorSpace*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamcolorspace)
-   [*VideoProcessorSetStreamDestRect*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamdestrect)
-   [*VideoProcessorSetStreamExtension*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamextension)
-   [*VideoProcessorSetStreamFilter*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamfilter)
-   [*VideoProcessorSetStreamFrameFormat*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamframeformat)
-   [*VideoProcessorSetStreamLumaKey*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamlumakey)
-   [*VideoProcessorSetStreamOutputRate*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamoutputrate)
-   [*VideoProcessorSetStreamPalette*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreampalette)
-   [*VideoProcessorSetStreamPixelAspectRatio*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreampixelaspectratio)
-   [*VideoProcessorSetStreamRotation*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamrotation)
-   [*VideoProcessorSetStreamSourceRect*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamsourcerect)
-   [*VideoProcessorSetStreamStereoFormat*](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamstereoformat)
-   [**D3D10 \_ DDI \_ 资源 \_ 绑定 \_ 标志**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_resource_bind_flag)
-   [**D3D10 \_ DDI \_ 资源 \_ 杂项 \_ 标志**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_resource_misc_flag)
-   [**D3D10DDIARG \_ CREATEDEVICE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ ALPHA \_ 填充 \_ 模式**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_alpha_fill_mode)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 自动 \_ 流 \_ 帽**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_auto_stream_caps)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ cap**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_caps)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 颜色 \_ 空间**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_color_space)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 内容 \_ DESC**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_content_desc)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 转换 \_ cap**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_conversion_caps)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 自定义 \_ 速率**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_custom_rate)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 设备 \_ cap**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_device_caps)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 功能 \_ 上限**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_feature_caps)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 筛选器**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_filter)
-   [**D3D11 \_ 1DDI \_ VIDEO \_ PROCESSOR \_ FILTER \_ cap**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_filter_caps)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 筛选 \_ 范围**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_filter_range)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 格式 \_ 上限**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_format_caps)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 格式 \_ 支持**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_format_support)
-   [**D3D11 \_ 1DDI \_ VIDEO \_ PROCESSOR \_ ITELECINE \_ cap**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_itelecine_caps)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 输出 \_ 速率**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_output_rate)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 速率 \_ 转换 \_ 上限**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_rate_conversion_caps)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 旋转**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_rotation)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 立体声 \_ cap**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_stereo_caps)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 立体声 \_ 翻转 \_ 模式**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_stereo_flip_mode)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 立体声 \_ 格式**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_stereo_format)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 处理器 \_ 流**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_stream)
-   [**D3D11 \_ 1DDI \_ 视频 \_ 使用情况**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_usage)
-   [**D3D11 \_ 1DDI \_ VIDEODEVICEFUNCS**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_videodevicefuncs)
-   [**D3D11 \_ 1DDIARG \_ CREATEAUTHENTICATEDCHANNEL**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createauthenticatedchannel)
-   [**D3D11 \_ 1DDIARG \_ CREATECRYPTOSESSION**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createcryptosession)
-   [**D3D11 \_ 1DDIARG \_ CREATEVIDEODECODER**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideodecoder)
-   [**D3D11 \_ 1DDIARG \_ CREATEVIDEODECODEROUTPUTVIEW**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideodecoderoutputview)
-   [**D3D11 \_ 1DDIARG \_ CREATEVIDEOPROCESSOR**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideoprocessor)
-   [**D3D11 \_ 1DDIARG \_ CREATEVIDEOPROCESSORENUM**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideoprocessorenum)
-   [**D3D11 \_ 1DDIARG \_ CREATEVIDEOPROCESSORINPUTVIEW**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideoprocessorinputview)
-   [**D3D11 \_ 1DDIARG \_ CREATEVIDEOPROCESSOROUTPUTVIEW**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideoprocessoroutputview)
-   [**D3D11 \_ 1DDIARG \_ 签名 \_ 条目**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_signature_entry)
-   [**D3D11 \_ 1DDIARG \_ 暂存 \_ IO \_ 签名**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_stage_io_signatures)
-   [**D3D11 \_ 1DDIARG \_ 镶嵌 \_ IO \_ 签名**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_tessellation_io_signatures)
-   [**D3D11 \_ 1DDIARG \_ VIDEODECODERBEGINFRAME**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_videodecoderbeginframe)
-   [**D3D11 \_ 1DDIARG \_ VIDEODECODEREXTENSION**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_videodecoderextension)
-   [**D3D11 \_ DDI \_ 着色器 \_ 最小 \_ 精度**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_ddi_shader_min_precision)
-   [**D3D11 \_ DDI \_ 着色器 \_ MIN \_ 精度 \_ 支持 \_ 数据**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_ddi_shader_min_precision_support_data)
-   [**D3D11 \_ DDI \_ 视频 \_ 解码器 \_ 缓冲区 \_ 类型**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_ddi_video_decoder_buffer_type)
-   [**D3D11DDI \_ HANDLETYPE**](/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11ddi_handletype)
-   [**D3D11DDIARG \_ CREATEDEFERREDCONTEXT**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext)
-   [**D3D11DDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)
-   [**D3DDDI \_ RESOURCEFLAGS2**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags2)
-   [**D3DDDIARG \_ CREATERESOURCE2**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)
-   [**DXVAHDDDI \_ 旋转**](/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_rotation)
-   [**DXVAHDDDI \_ 流 \_ 状态**](/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_stream_state)
-   [**DXVAHDDDI \_ 流 \_ 状态 \_ 旋转 \_ 数据**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_stream_state_rotation_data)
-   [**DXVAHDDDI \_ VPDEVCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)
-   [**FORMATOP**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_formatop)

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


所有 Windows 8 硬件上都需要 Direct3D 11 API 支持。

有关硬件设备实现此功能时必须满足的要求的信息，请参阅相关 [WHCK 文档](/windows-hardware/test/hlk/windows-hardware-lab-kit)，了解设备上的 **¦ DX11 视频解码 FeatureLevel 9** **和¦ DX11 VideoProcessing。**

请参阅 [WDDM 1.2 功能](wddm-v1-2-features.md) ，了解 Windows 8 中添加的功能。

 

