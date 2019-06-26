---
title: 内容保护 DDI
description: 内容保护 DDI
ms.assetid: 770e0fce-d3b5-4599-8165-eadf3f23f9dc
keywords:
- 保护视频内容 WDK Windows 7 显示，内容保护 DDI
- 保护视频内容 WDK Windows Server 2008 R2 显示，内容保护 DDI
- WDK Windows 7 显示、 内容保护 DDI 的视频内容
- WDK Windows Server 2008 R2 显示、 内容保护 DDI 的视频内容
- 显示视频内容 WDK Windows Server 2008 R2，请保护
- 显示内容保护 DDI WDK Windows 7
- 显示内容保护 DDI WDK Windows Server 2008 R2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa4f599fd0e76c2815aad9fd1c4039a71e0ae4e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363071"
---
# <a name="content-protection-ddi"></a>内容保护 DDI


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

内容保护 DDI 是扩展[Direct3D 版本 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/index)来保护视频。 内容保护 DDI 包含，此部分所述的入口点。

### <a name="span-idrequiredcontentprotectionddifunctionsspanspan-idrequiredcontentprotectionddifunctionsspanrequired-content-protection-ddi-functions"></a><span id="required_content_protection_ddi_functions"></span><span id="REQUIRED_CONTENT_PROTECTION_DDI_FUNCTIONS"></span>所需内容保护 DDI 函数

如果在用户模式显示驱动程序中实现内容保护，该驱动程序必须支持以下内容保护 DDI 函数：

-   [ **CreateAuthenticatedChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createauthenticatedchannel)函数创建 Direct3D 运行时和驱动程序可以使用它来设置和查询保护的通道。

-   [ **AuthenticatedChannelKeyExchange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_authenticatedchannelkeyexchange)函数协商的会话密钥。

-   [ **QueryAuthenticatedChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_queryauthenticatedchannel)函数将查询功能和状态信息的已经过身份验证的通道。

-   [ **ConfigureAuthenticatedChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_configureauthenicatedchannel)函数设置身份验证的通道中的状态。

-   [ **DestroyAuthenticatedChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroyauthenticatedchannel)函数释放资源的经过身份验证的通道。

-   [ **CreateCryptoSession** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createcryptosession)函数创建 Direct3D 运行时使用管理会话密钥的加密会话，并执行加密操作输入和输出受保护的内存。

-   [ **CryptoSessionKeyExchange** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_cryptosessionkeyexchange)函数协商的会话密钥。

-   [ **DestroyCryptoSession** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_destroycryptosession)函数释放资源的加密会话。

### <a name="span-idcontentprotectioncapabilitiesspanspan-idcontentprotectioncapabilitiesspancontent-protection-capabilities"></a><span id="content_protection_capabilities"></span><span id="CONTENT_PROTECTION_CAPABILITIES"></span>内容保护功能

如果它支持每个上述所需的内容保护 DDI 函数，用户模式显示驱动程序只报告内容保护功能。 以下[ **D3DDDICAPS\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_d3dddicaps_type)值由 Direct3D 运行时，用于检索用户模式显示驱动程序支持的内容保护功能有关的信息。 运行时设置这些 D3DDDICAPS\_值中的类型**类型**的成员[ **D3DDDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的*pData*驱动程序的参数[ **GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数运行时调用的时点**GetCaps**。

<span id="D3DDDICAPS_GETCONTENTPROTECTIONCAPS"></span><span id="d3dddicaps_getcontentprotectioncaps"></span>D3DDDICAPS\_GETCONTENTPROTECTIONCAPS  
在运行时提供一个指向[ **DDICONTENTPROTECTIONCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_ddicontentprotectioncaps)结构特定的加密和解码该驱动程序应使用的组合。 该驱动程序返回一个指向描述对加密的驱动程序的内容保护功能的填充 D3DCONTENTPROTECTIONCAPS 结构和解码组合。 有关 D3DCONTENTPROTECTIONCAPS 详细信息，请参阅 DirectX SDK 文档。

<span id="D3DDDICAPS_GETCERTIFICATESIZE"></span><span id="d3dddicaps_getcertificatesize"></span>D3DDDICAPS\_GETCERTIFICATESIZE  
该驱动程序为一个数字，指定的大小，以字节为单位用于通道或加密类型的驱动程序的证书提供一个指针。 Direct3D 运行时则使用此大小来分配缓冲区来存放在运行时接收时运行时调用的证书信息[ **GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)与 D3DDDICAPS\_GETCERTIFICATE 时。

<span id="D3DDDICAPS_GETCERTIFICATE"></span><span id="d3dddicaps_getcertificate"></span>D3DDDICAPS\_GETCERTIFICATE  
在运行时提供一个指向[ **DDICERTIFICATEINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_ddicertificateinfo)结构，它描述了该驱动程序应检索的证书。

为经过身份验证的通道，该驱动程序使用的现有[OPM](opm-features.md)证书，这是由 Microsoft 签名的根的 X.509 证书。

应用程序可查询驱动程序的证书，以确定以下信息：

-   该驱动程序是否受信任。

-   是否已吊销该驱动程序。

-   驱动程序的公钥。 应用程序使用驱动程序的公钥来建立身份验证的通道用于进行身份验证的会话密钥。

调用[ **GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)与 D3DDDICAPS\_getcertificate 时设置失败，如果调用 Direct3D 9 身份验证通道，因为此通道不支持的证书或身份验证。

对于加密会话中，驱动程序将返回其证书以给定的加密类型。 根据加密类型和使用密钥交换，证书可能会或可能不会使用。 还有可能不同的加密类型可以使用不同的证书。

### <a name="span-idoptionalcontentprotectionddifunctionsspanspan-idoptionalcontentprotectionddifunctionsspanoptional-content-protection-ddi-functions"></a><span id="optional_content_protection_ddi_functions"></span><span id="OPTIONAL_CONTENT_PROTECTION_DDI_FUNCTIONS"></span>可选内容保护 DDI 函数

该驱动程序可以根据需要支持以下内容保护 DDI 函数：

-   [ **EncryptionBlt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_encryptionblt)函数受保护的图面中读取加密的数据。

-   [ **GetPitch** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getpitch)函数检索的受保护的图面音调。

-   [ **StartSessionKeyRefresh** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_startsessionkeyrefresh)函数返回的随机数字的解码器/应用程序和驱动程序/硬件随后可用于执行异或运算 (XOR) 与会话键。

-   [ **FinishSessionKeyRefresh** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_finishsessionkeyrefresh)函数指示从该点在时间中的所有缓冲区，将都使用更新后的会话密钥值。

-   [ **GetEncryptionBltKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getencryptionbltkey)函数将返回用于对数据进行解密的密钥的驱动程序[ **EncryptionBlt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_encryptionblt)函数将返回。

-   [ **DecryptionBlt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_decryptionblt)函数将数据写入到受保护的图面。

### <a name="span-idcontentprotectedresourcesspanspan-idcontentprotectedresourcesspan-content-protected-resources"></a><span id="content_protected_resources"></span><span id="CONTENT_PROTECTED_RESOURCES"></span> 内容受保护的资源

以下[ **D3DDDI\_RESOURCEFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags)标志由 Direct3D 运行时用于受保护的内容。 运行时设置这些 D3DDDI\_RESOURCEFLAGS 标志在**标志**的成员[ **D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构*pResource*驱动程序的参数[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数运行时调用的时点**CreateResource**.

<span id="RestrictedContent"></span><span id="restrictedcontent"></span><span id="RESTRICTEDCONTENT"></span>**RestrictedContent**  
该资源可能包含受保护的内容。 应用程序可能会或可能不具有显式启用内容保护之前应用程序创建一个资源。 该驱动程序应确保在运行时将资源分配放置在可以保护的内存池。 该驱动程序应允许可锁定的受保护资源的创建。 但是，该驱动程序应显式失败的调用其[**锁**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lock)函数来启用内容保护锁定这些图面。

<span id="RestrictSharedAccess"></span><span id="restrictsharedaccess"></span><span id="RESTRICTSHAREDACCESS"></span>**RestrictSharedAccess**  
只有特定的进程应允许对共享资源的访问。

该驱动程序应限制对此资源的共享的访问。 在运行时只能调用驱动程序的[ **OpenResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)函数来显示设备打开此资源 (**hDevice**) 中创建了该资源的进程或通过这些设备的已显式授予访问权限通过身份验证的通道。

 

 





