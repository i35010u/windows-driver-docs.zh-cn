---
title: 内容保护 DDI
description: 内容保护 DDI
ms.assetid: 770e0fce-d3b5-4599-8165-eadf3f23f9dc
keywords:
- 保护视频内容 WDK Windows 7 显示，内容保护 DDI
- 保护视频内容 WDK Windows Server 2008 R2 显示，内容保护 DDI
- 视频内容 WDK Windows 7 显示，内容保护 DDI
- 视频内容 WDK Windows Server 2008 R2 显示，内容保护 DDI
- 视频内容 WDK Windows Server 2008 R2 显示，保护
- 内容保护 DDI WDK Windows 7 显示
- 内容保护 DDI WDK Windows Server 2008 R2 显示器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a474587ad8988ba53756d0501556ca72d27d9553
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839046"
---
# <a name="content-protection-ddi"></a>内容保护 DDI


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

内容保护 DDI 是用于保护视频的[Direct3D 版本 9 ddi](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/index)的扩展。 内容保护 DDI 包含本部分中描述的入口点。

### <a name="span-idrequired_content_protection_ddi_functionsspanspan-idrequired_content_protection_ddi_functionsspanrequired-content-protection-ddi-functions"></a><span id="required_content_protection_ddi_functions"></span><span id="REQUIRED_CONTENT_PROTECTION_DDI_FUNCTIONS"></span>必需内容保护 DDI 函数

如果在用户模式显示驱动程序中实现内容保护，则驱动程序必须支持以下内容保护 DDI 函数：

-   [**CreateAuthenticatedChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createauthenticatedchannel)函数创建一个通道，Direct3D 运行时和驱动程序可以使用该通道来设置和查询保护。

-   [**AuthenticatedChannelKeyExchange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_authenticatedchannelkeyexchange)函数协商会话密钥。

-   [**QueryAuthenticatedChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_queryauthenticatedchannel)函数在经过身份验证的通道上查询功能和状态信息。

-   [**ConfigureAuthenticatedChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_configureauthenicatedchannel)函数在经过身份验证的通道内设置状态。

-   [**DestroyAuthenticatedChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyauthenticatedchannel)函数可为经过身份验证的通道释放资源。

-   [**CreateCryptoSession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createcryptosession)函数将创建一个加密会话，Direct3D 运行时使用该会话来管理会话密钥，并对受保护内存执行加密操作。

-   [**CryptoSessionKeyExchange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_cryptosessionkeyexchange)函数协商会话密钥。

-   [**DestroyCryptoSession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_destroycryptosession)函数释放加密会话的资源。

### <a name="span-idcontent_protection_capabilitiesspanspan-idcontent_protection_capabilitiesspancontent-protection-capabilities"></a><span id="content_protection_capabilities"></span><span id="CONTENT_PROTECTION_CAPABILITIES"></span>内容保护功能

仅当内容保护功能支持上述每个必需内容保护 DDI 函数时，用户模式显示驱动程序才会报告该功能。 Direct3D 运行时使用以下[**D3DDDICAPS\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type)值来检索有关用户模式显示驱动程序支持的内容保护功能的信息。 运行时将这些 D3DDDICAPS 设置\_类型[ **\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的**类型**成员中的值，在运行时调用时，驱动程序的[**GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数的*pData*参数指向**GETCAPS**.

<span id="D3DDDICAPS_GETCONTENTPROTECTIONCAPS"></span><span id="d3dddicaps_getcontentprotectioncaps"></span>D3DDDICAPS\_GETCONTENTPROTECTIONCAPS  
运行时为驱动程序应使用的特定加密和解码组合提供一个指向[**DDICONTENTPROTECTIONCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_ddicontentprotectioncaps)结构的指针。 驱动程序将返回一个指向填充的 D3DCONTENTPROTECTIONCAPS 结构的指针，该结构描述了驱动程序的加密和解码组合的内容保护功能。 有关 D3DCONTENTPROTECTIONCAPS 的详细信息，请参阅 DirectX SDK 文档。

<span id="D3DDDICAPS_GETCERTIFICATESIZE"></span><span id="d3dddicaps_getcertificatesize"></span>D3DDDICAPS\_GETCERTIFICATESIZE  
驱动程序提供一个指向数字的指针，该数字指定用于通道或加密类型的驱动程序证书的大小（以字节为单位）。 然后，在运行时使用 D3DDDICAPS\_GETCERTIFICATE 时出错调用[**GetCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)时，Direct3D 运行时将使用此大小分配一个缓冲区来保存运行时收到的证书信息。

<span id="D3DDDICAPS_GETCERTIFICATE"></span><span id="d3dddicaps_getcertificate"></span>D3DDDICAPS\_GETCERTIFICATE 时出错  
运行时提供一个指向[**DDICERTIFICATEINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_ddicertificateinfo)结构的指针，该结构描述了驱动程序应检索的证书。

对于经过身份验证的通道，驱动程序使用现有的[OPM](opm-features.md)证书，该证书是由 Microsoft 进行了身份验证的 x.509 证书。

应用程序可以查询驱动程序的证书来确定以下信息：

-   驱动程序是否受信任。

-   驱动程序是否已吊销。

-   驱动程序的公钥。 应用程序使用驱动程序的公钥为用于身份验证的经过身份验证的通道建立会话密钥。

如果对使用 D3DDDICAPS\_GETCERTIFICATE 时出错集的调用[**GetCaps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps) ，则对它的调用将失败，因为该通道不支持证书或身份验证。

对于加密会话，驱动程序会针对给定的加密类型返回其证书。 根据所使用的加密类型和密钥交换，可以使用证书，也可以不使用。 不同的加密类型也可以使用不同的证书。

### <a name="span-idoptional_content_protection_ddi_functionsspanspan-idoptional_content_protection_ddi_functionsspanoptional-content-protection-ddi-functions"></a><span id="optional_content_protection_ddi_functions"></span><span id="OPTIONAL_CONTENT_PROTECTION_DDI_FUNCTIONS"></span>可选内容保护 DDI 函数

该驱动程序可以选择支持以下内容保护 DDI 函数：

-   [**EncryptionBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_encryptionblt)函数从受保护的图面读取加密的数据。

-   [**GetPitch**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getpitch)函数检索受保护图面的间距。

-   [**StartSessionKeyRefresh**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_startsessionkeyrefresh)函数返回一个随机数，解码器/应用程序和驱动程序/硬件随后可以使用该随机数来执行带会话密钥的排除或操作（XOR）。

-   [**FinishSessionKeyRefresh**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_finishsessionkeyrefresh)函数指示该时间点的所有缓冲区都将使用更新的会话密钥值。

-   [**GetEncryptionBltKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getencryptionbltkey)函数返回用于解密驱动程序的[**EncryptionBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_encryptionblt)函数返回的数据的键。

-   [**DecryptionBlt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decryptionblt)函数将数据写入受保护的图面。

### <a name="span-idcontent_protected_resourcesspanspan-idcontent_protected_resourcesspan-content-protected-resources"></a><span id="content_protected_resources"></span><span id="CONTENT_PROTECTED_RESOURCES"></span>受内容保护的资源

对于受保护的内容，Direct3D 运行时使用以下[**D3DDDI\_RESOURCEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags)标志。 运行时在[**D3DDDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的**flags**成员中设置这些 D3DDDI\_RESOURCEFLAGS 标志，驱动程序[**pResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数的*CREATERESOURCE*参数指向运行时调用**CreateResource**。

<span id="RestrictedContent"></span><span id="restrictedcontent"></span><span id="RESTRICTEDCONTENT"></span>**RestrictedContent**  
资源可能包含受保护的内容。 在应用程序创建资源之前，应用程序可能会也可能不会显式启用内容保护。 驱动程序应确保运行时将资源分配放置在可保护的内存池中。 驱动程序应该允许创建受锁定保护的资源。 但是，当启用内容保护时，驱动程序应显式地将对其[**lock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_lock)函数的调用锁定以锁定这些图面。

<span id="RestrictSharedAccess"></span><span id="restrictsharedaccess"></span><span id="RESTRICTSHAREDACCESS"></span>**RestrictSharedAccess**  
应只允许特定进程访问共享资源。

驱动程序应限制对此资源的共享访问。 运行时只能调用驱动程序的[**OpenResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)函数，以使用显示设备（**hDevice**）在创建资源的进程内或通过通过身份验证沟.

 

 





