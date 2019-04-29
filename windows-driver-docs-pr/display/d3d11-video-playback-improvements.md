---
title: Direct3D 11 视频播放改进
description: 与更广泛采用的主流应用程序中的 Microsoft Direct3D 10 技术，某些应用程序开发人员希望将视为所有内容相同。
ms.assetid: BB32F074-16E8-46E4-B9CF-6AEBE331B549
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03c48a09e9d84ccf56214c00e21c2466ac89b8c4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376765"
---
# <a name="direct3d-11-video-playback-improvements"></a>Direct3D 11 视频播放改进


与更广泛采用的主流应用程序中的 Microsoft Direct3D 10 技术，某些应用程序开发人员希望将视为所有内容相同。 这是一个挑战通过 Direct3D 10 或 11 Api 处理所有的二维和三维内容时，如何使用 Microsoft Direct3D 9 API 上的视频。 因为 Windows 8 引入了 Microsoft Direct3D 11 的视频，应用程序可以使用单个 API 来执行所有图形操作。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">Windows 显示器驱动程序模型 (WDDM) 的最低版本</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">最大 Windows 版本</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">驱动程序实现 — 仅完全图形和呈现</td>
<td align="left">必须为所有 WDDM 1.2 驱动程序与 Microsoft Direct3D 10-，10.1、 11 或 11.1 支持的硬件 （或更高版本）</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit">WHCK</a>要求和测试</td>
<td align="left"><p><strong>Device.Graphics...DX11 视频解码 FeatureLevel 9</strong></p>
<p><strong>Device.Graphics...DX11 VideoProcessing</strong></p></td>
</tr>
</tbody>
</table>

 

以下是使用 Direct3D 11 的主要优点：

-   Direct3D 11 视频简化了 Microsoft Media Foundation 和 Microsoft DirectX 技术之间的互操作性。
-   使用多个 Api 是到程序中，更难，因此在 Direct3D 11 上使用视频简化了编程体验，并且使应用更高效。 该 API 提供了更灵活地使用已解码和已处理的视频。
-   立体三维视频在 Direct3D 11 API 对立体声帧解压缩到左侧和右侧眼映像。
-   它具有与 DirectX 视频加速 (DXVA) 2.0 和 DXVA HD 中解码和视频处理功能的奇偶校验。
-   它可在会话 0 用于转码方案中。

## <a name="span-iddirect3d11videodevicedriverinterfacesddisspanspan-iddirect3d11videodevicedriverinterfacesddisspanspan-iddirect3d11videodevicedriverinterfacesddisspandirect3d11-video-device-driver-interfaces-ddis"></a><span id="Direct3D_11_video_device_driver_interfaces__DDIs_"></span><span id="direct3d_11_video_device_driver_interfaces__ddis_"></span><span id="DIRECT3D_11_VIDEO_DEVICE_DRIVER_INTERFACES__DDIS_"></span>Direct3D 11 视频设备驱动程序接口 (DDIs)


这些设备驱动程序接口 (DDIs) 是新的或更新 Windows 8:

-   [*CalcPrivateCryptoSessionSize*](https://msdn.microsoft.com/library/windows/hardware/hh451606)
-   [*CalcPrivateAuthenticatedChannelSize*](https://msdn.microsoft.com/library/windows/hardware/hh451604)
-   [*CalcPrivateVideoDecoderOutputViewSize*](https://msdn.microsoft.com/library/windows/hardware/hh451608)
-   [*CalcPrivateVideoDecoderSize*](https://msdn.microsoft.com/library/windows/hardware/hh451610)
-   [*CalcPrivateVideoProcessorEnumSize*](https://msdn.microsoft.com/library/windows/hardware/hh451611)
-   [*CalcPrivateVideoProcessorInputViewSize*](https://msdn.microsoft.com/library/windows/hardware/hh451612)
-   [*CalcPrivateVideoProcessorOutputViewSize*](https://msdn.microsoft.com/library/windows/hardware/hh451613)
-   [*CalcPrivateVideoProcessorSize*](https://msdn.microsoft.com/library/windows/hardware/hh451614)
-   [*CheckFormatSupport*](https://msdn.microsoft.com/library/windows/hardware/ff539390)
-   [*CheckVideoDecoderFormat*](https://msdn.microsoft.com/library/windows/hardware/hh451615)
-   [*CheckVideoProcessorFormat*](https://msdn.microsoft.com/library/windows/hardware/hh451616)
-   [*ConfigureAuthenticatedChannel(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh451617)
-   [*CreateAuthenticatedChannel(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh451618)
-   [*CreateCryptoSession*](https://msdn.microsoft.com/library/windows/hardware/hh451619)
-   [*CreateResource2*](https://msdn.microsoft.com/library/windows/hardware/hh406287)
-   [*CreateVideoDecoder*](https://msdn.microsoft.com/library/windows/hardware/hh451620)
-   [*CreateVideoDecoderOutputView*](https://msdn.microsoft.com/library/windows/hardware/hh451621)
-   [*CreateVideoProcessor*](https://msdn.microsoft.com/library/windows/hardware/hh451622)
-   [*CreateVideoProcessorEnum*](https://msdn.microsoft.com/library/windows/hardware/hh451623)
-   [*CreateVideoProcessorInputView*](https://msdn.microsoft.com/library/windows/hardware/hh451624)
-   [*CreateVideoProcessorOutputView*](https://msdn.microsoft.com/library/windows/hardware/hh451625)
-   [*CryptoSessionGetHandle*](https://msdn.microsoft.com/library/windows/hardware/hh451626)
-   [*DecryptionBlt(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh451628)
-   [*DestroyAuthenticatedChannel*](https://msdn.microsoft.com/library/windows/hardware/hh451630)
-   [*DestroyCryptoSession*](https://msdn.microsoft.com/library/windows/hardware/hh451632)
-   [*DestroyVideoDecoder*](https://msdn.microsoft.com/library/windows/hardware/hh451634)
-   [*DestroyVideoDecoderOutputView*](https://msdn.microsoft.com/library/windows/hardware/hh451636)
-   [*DestroyVideoProcessor*](https://msdn.microsoft.com/library/windows/hardware/hh451638)
-   [*DestroyVideoProcessorEnum*](https://msdn.microsoft.com/library/windows/hardware/hh451639)
-   [*DestroyVideoProcessorInputView*](https://msdn.microsoft.com/library/windows/hardware/hh451642)
-   [*DestroyVideoProcessorOutputView*](https://msdn.microsoft.com/library/windows/hardware/hh451644)
-   [*EncryptionBlt(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh451646)
-   [*FinishSessionKeyRefresh*](https://msdn.microsoft.com/library/windows/hardware/hh451648)
-   [*GetCaptureHandle*](https://msdn.microsoft.com/library/windows/hardware/hh451650)
-   [*GetCertificate*](https://msdn.microsoft.com/library/windows/hardware/hh451652)
-   [*GetCertificateSize*](https://msdn.microsoft.com/library/windows/hardware/hh451654)
-   [*GetContentProtectionCaps*](https://msdn.microsoft.com/library/windows/hardware/hh451656)
-   [*GetCryptoKeyExchangeType*](https://msdn.microsoft.com/library/windows/hardware/hh451658)
-   [*GetEncryptionBltKey*](https://msdn.microsoft.com/library/windows/hardware/hh451660)
-   [*GetVideoDecoderBufferInfo*](https://msdn.microsoft.com/library/windows/hardware/hh451661)
-   [*GetVideoDecoderBufferTypeCount*](https://msdn.microsoft.com/library/windows/hardware/hh451663)
-   [*GetVideoDecoderConfig*](https://msdn.microsoft.com/library/windows/hardware/hh451665)
-   [*GetVideoDecoderConfigCount*](https://msdn.microsoft.com/library/windows/hardware/hh451668)
-   [*GetVideoDecoderProfile*](https://msdn.microsoft.com/library/windows/hardware/hh451670)
-   [*GetVideoDecoderProfileCount*](https://msdn.microsoft.com/library/windows/hardware/hh451672)
-   [*GetVideoProcessorCaps*](https://msdn.microsoft.com/library/windows/hardware/hh451674)
-   [*GetVideoProcessorCustomRate*](https://msdn.microsoft.com/library/windows/hardware/hh451676)
-   [*GetVideoProcessorFilterRange*](https://msdn.microsoft.com/library/windows/hardware/hh451689)
-   [*GetVideoProcessorRateConversionCaps*](https://msdn.microsoft.com/library/windows/hardware/hh451690)
-   [*NegotiateAuthenticatedChannelKeyExchange*](https://msdn.microsoft.com/library/windows/hardware/hh451691)
-   [*NegotiateCryptoSessionKeyExchange*](https://msdn.microsoft.com/library/windows/hardware/hh451692)
-   [*QueryAuthenticatedChannel(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh451694)
-   [*RetrieveSubObject(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh439849)
-   [*StartSessionKeyRefresh*](https://msdn.microsoft.com/library/windows/hardware/hh451696)
-   [*VideoDecoderBeginFrame*](https://msdn.microsoft.com/library/windows/hardware/hh451697)
-   [*VideoDecoderEndFrame*](https://msdn.microsoft.com/library/windows/hardware/hh451698)
-   [*VideoDecoderExtension*](https://msdn.microsoft.com/library/windows/hardware/hh451699)
-   [*VideoDecoderGetHandle*](https://msdn.microsoft.com/library/windows/hardware/hh451700)
-   [*VideoDecoderSubmitBuffers*](https://msdn.microsoft.com/library/windows/hardware/hh451701)
-   [*VideoProcessorBlt*](https://msdn.microsoft.com/library/windows/hardware/hh451703)
-   [*VideoProcessorGetOutputExtension*](https://msdn.microsoft.com/library/windows/hardware/hh451705)
-   [*VideoProcessorGetStreamExtension*](https://msdn.microsoft.com/library/windows/hardware/hh439773)
-   [*VideoProcessorInputViewReadAfterWriteHazard*](https://msdn.microsoft.com/library/windows/hardware/hh439775)
-   [*VideoProcessorSetOutputAlphaFillMode*](https://msdn.microsoft.com/library/windows/hardware/hh439778)
-   [*VideoProcessorSetOutputBackgroundColor*](https://msdn.microsoft.com/library/windows/hardware/dn459003)
-   [*VideoProcessorSetOutputColorSpace*](https://msdn.microsoft.com/library/windows/hardware/hh439782)
-   [*VideoProcessorSetOutputConstriction*](https://msdn.microsoft.com/library/windows/hardware/hh439784)
-   [*VideoProcessorSetOutputExtension*](https://msdn.microsoft.com/library/windows/hardware/hh439786)
-   [*VideoProcessorSetOutputStereoMode*](https://msdn.microsoft.com/library/windows/hardware/hh439788)
-   [*VideoProcessorSetOutputTargetRect*](https://msdn.microsoft.com/library/windows/hardware/hh439790)
-   [*VideoProcessorSetStreamAlpha*](https://msdn.microsoft.com/library/windows/hardware/hh439792)
-   [*VideoProcessorSetStreamAutoProcessingMode*](https://msdn.microsoft.com/library/windows/hardware/hh439794)
-   [*VideoProcessorSetStreamColorSpace*](https://msdn.microsoft.com/library/windows/hardware/hh439796)
-   [*VideoProcessorSetStreamDestRect*](https://msdn.microsoft.com/library/windows/hardware/dn459004)
-   [*VideoProcessorSetStreamExtension*](https://msdn.microsoft.com/library/windows/hardware/hh439800)
-   [*VideoProcessorSetStreamFilter*](https://msdn.microsoft.com/library/windows/hardware/hh439802)
-   [*VideoProcessorSetStreamFrameFormat*](https://msdn.microsoft.com/library/windows/hardware/hh439804)
-   [*VideoProcessorSetStreamLumaKey*](https://msdn.microsoft.com/library/windows/hardware/hh439805)
-   [*VideoProcessorSetStreamOutputRate*](https://msdn.microsoft.com/library/windows/hardware/hh439807)
-   [*VideoProcessorSetStreamPalette*](https://msdn.microsoft.com/library/windows/hardware/hh439809)
-   [*VideoProcessorSetStreamPixelAspectRatio*](https://msdn.microsoft.com/library/windows/hardware/hh439811)
-   [*VideoProcessorSetStreamRotation*](https://msdn.microsoft.com/library/windows/hardware/hh439813)
-   [*VideoProcessorSetStreamSourceRect*](https://msdn.microsoft.com/library/windows/hardware/hh439815)
-   [*VideoProcessorSetStreamStereoFormat*](https://msdn.microsoft.com/library/windows/hardware/hh439817)
-   [**D3D10\_DDI\_RESOURCE\_BIND\_FLAG**](https://msdn.microsoft.com/library/windows/hardware/ff541995)
-   [**D3D10\_DDI\_RESOURCE\_MISC\_FLAG**](https://msdn.microsoft.com/library/windows/hardware/ff542004)
-   [**D3D10DDIARG\_CREATEDEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff541664)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_ALPHA\_FILL\_MODE**](https://msdn.microsoft.com/library/windows/hardware/hh450963)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_AUTO\_STREAM\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/hh450966)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/hh450968)
-   [**D3D11\_1DDI\_视频\_处理器\_颜色\_空间**](https://msdn.microsoft.com/library/windows/hardware/hh450970)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_CONTENT\_DESC**](https://msdn.microsoft.com/library/windows/hardware/hh450972)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_CONVERSION\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/hh450975)
-   [**D3D11\_1DDI\_视频\_处理器\_自定义\_速率**](https://msdn.microsoft.com/library/windows/hardware/hh450977)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_DEVICE\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/hh450978)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_FEATURE\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/hh450980)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_FILTER**](https://msdn.microsoft.com/library/windows/hardware/hh450982)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_FILTER\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/hh450983)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_FILTER\_RANGE**](https://msdn.microsoft.com/library/windows/hardware/hh450985)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_FORMAT\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/hh450986)
-   [**D3D11\_1DDI\_视频\_处理器\_格式\_支持**](https://msdn.microsoft.com/library/windows/hardware/hh450987)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_ITELECINE\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/hh450988)
-   [**D3D11\_1DDI\_视频\_处理器\_输出\_速率**](https://msdn.microsoft.com/library/windows/hardware/hh450989)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_RATE\_CONVERSION\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/hh450990)
-   [**D3D11\_1DDI\_视频\_处理器\_旋转**](https://msdn.microsoft.com/library/windows/hardware/hh451019)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_STEREO\_CAPS**](https://msdn.microsoft.com/library/windows/hardware/hh451023)
-   [**D3D11\_1DDI\_视频\_处理器\_立体声\_FLIP\_模式**](https://msdn.microsoft.com/library/windows/hardware/hh451025)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_STEREO\_FORMAT**](https://msdn.microsoft.com/library/windows/hardware/hh451029)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_STREAM**](https://msdn.microsoft.com/library/windows/hardware/hh451033)
-   [**D3D11\_1DDI\_VIDEO\_USAGE**](https://msdn.microsoft.com/library/windows/hardware/hh451037)
-   [**D3D11\_1DDI\_VIDEODEVICEFUNCS**](https://msdn.microsoft.com/library/windows/hardware/hh406452)
-   [**D3D11\_1DDIARG\_CREATEAUTHENTICATEDCHANNEL**](https://msdn.microsoft.com/library/windows/hardware/hh406306)
-   [**D3D11\_1DDIARG\_CREATECRYPTOSESSION**](https://msdn.microsoft.com/library/windows/hardware/hh406308)
-   [**D3D11\_1DDIARG\_CREATEVIDEODECODER**](https://msdn.microsoft.com/library/windows/hardware/hh406310)
-   [**D3D11\_1DDIARG\_CREATEVIDEODECODEROUTPUTVIEW**](https://msdn.microsoft.com/library/windows/hardware/hh406312)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSOR**](https://msdn.microsoft.com/library/windows/hardware/hh406314)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSORENUM**](https://msdn.microsoft.com/library/windows/hardware/hh406316)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSORINPUTVIEW**](https://msdn.microsoft.com/library/windows/hardware/hh406318)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSOROUTPUTVIEW**](https://msdn.microsoft.com/library/windows/hardware/hh406320)
-   [**D3D11\_1DDIARG\_签名\_条目**](https://msdn.microsoft.com/library/windows/hardware/hh406322)
-   [**D3D11\_1DDIARG\_阶段\_IO\_签名**](https://msdn.microsoft.com/library/windows/hardware/hh406324)
-   [**D3D11\_1DDIARG\_分割\_IO\_签名**](https://msdn.microsoft.com/library/windows/hardware/hh406326)
-   [**D3D11\_1DDIARG\_VIDEODECODERBEGINFRAME**](https://msdn.microsoft.com/library/windows/hardware/hh406328)
-   [**D3D11\_1DDIARG\_VIDEODECODEREXTENSION**](https://msdn.microsoft.com/library/windows/hardware/hh406330)
-   [**D3D11\_DDI\_SHADER\_MIN\_PRECISION**](https://msdn.microsoft.com/library/windows/hardware/hh451059)
-   [**D3D11\_DDI\_着色器\_MIN\_精度\_支持\_数据**](https://msdn.microsoft.com/library/windows/hardware/hh451062)
-   [**D3D11\_DDI\_VIDEO\_DECODER\_BUFFER\_TYPE**](https://msdn.microsoft.com/library/windows/hardware/hh451066)
-   [**D3D11DDI\_HANDLETYPE**](https://msdn.microsoft.com/library/windows/hardware/ff542152)
-   [**D3D11DDIARG\_CREATEDEFERREDCONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff542044)
-   [**D3D11DDIARG\_CREATERESOURCE**](https://msdn.microsoft.com/library/windows/hardware/ff542062)
-   [**D3DDDI\_RESOURCEFLAGS2**](https://msdn.microsoft.com/library/windows/hardware/hh439286)
-   [**D3DDDIARG\_CREATERESOURCE2**](https://msdn.microsoft.com/library/windows/hardware/hh451074)
-   [**DXVAHDDDI\_ROTATION**](https://msdn.microsoft.com/library/windows/hardware/hh464119)
-   [**DXVAHDDDI\_STREAM\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff563068)
-   [**DXVAHDDDI\_STREAM\_STATE\_ROTATION\_DATA**](https://msdn.microsoft.com/library/windows/hardware/hh464120)
-   [**DXVAHDDDI\_VPDEVCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff563113)
-   [**FORMATOP**](https://msdn.microsoft.com/library/windows/hardware/ff566438)

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


所有 Windows 8 硬件上需要 Direct3D 11 API 支持。

有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**Device.Graphics...DX11 视频解码 FeatureLevel 9**并**Device.Graphics...DX11 VideoProcessing**。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)评审的 Windows 8 一起添加的功能。

 

 





