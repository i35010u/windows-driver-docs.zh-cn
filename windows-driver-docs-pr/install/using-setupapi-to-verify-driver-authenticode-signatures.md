---
title: 使用 SetupAPI 来验证驱动程序验证码签名
description: 使用 SetupAPI 来验证驱动程序验证码签名
ms.assetid: 2019d77d-2d98-4bae-8d9d-aa41e47f3811
keywords:
- 安装程序 Api 函数 WDK，验证签名
- 验证码签名 WDK
- 签名 WDK，验证码
- 数字签名 WDK，验证码
- 验证 Authenticode 签名
- 检查验证码签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6710e892a5dae0827394540786ae5bba00e6e19d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519241"
---
# <a name="using-setupapi-to-verify-driver-authenticode-signatures"></a>使用 SetupAPI 来验证驱动程序验证码签名





您可以使用以下过程验证驱动程序包含有效的验证码[数字签名](digital-signatures.md)。 从 Microsoft Windows Server 2003 支持这些过程。

### <a name="to-determine-whether-a-driver-has-a-valid-authenticode-signature"></a>若要确定驱动程序是否包含有效的 Authenticode 签名

检查 DNF_AUTHENTICODE_SIGNED 标志。

Windows 驱动程序包含有效的 Authenticode 签名，如果设置此标志**标志**驱动程序节点的成员[ **SP_DRVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553290)结构。 (此外请注意，Windows，如果该驱动程序设置 DNF_INF_IS_SIGNED 标志[WHQL 版本签名](whql-release-signature.md)，如果系统提供的驱动程序，或如果它包含验证码签名。)

### <a name="to-verify-that-an-inf-file-has-a-valid-authenticode-signature"></a>若要验证的 INF 文件具有有效的 Authenticode 签名

1.  调用[INF 文件处理函数](inf-file-processing-functions.md) **SetupVerifyInfFile**。

2.  检查函数返回的错误代码。

    INF 文件不是系统提供，并且没有有效的 WHQL 数字签名，但它具有一个有效的 Authenticode 签名，如果**SetupVerifyInfFile**返回**FALSE**和[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)返回以下错误代码之一：

    <a href="" id="error-authenticode-trusted-publisher"></a>ERROR_AUTHENTICODE_TRUSTED_PUBLISHER  
    指示由于发布服务器的证书安装在发布服务器是受信任[受信任的发行者证书存储区](trusted-publishers-certificate-store.md)。

    <a href="" id="error-authenticode-trust-not-established"></a>ERROR_AUTHENTICODE_TRUST_NOT_ESTABLISHED  
    表示由于发布服务器的签名证书未安装受信任的发行者证书存储中不能自动建立信任。 但是，这不一定表示出现错误。 相反，它表示调用方必须应用特定于调用方的策略中发布服务器建立信任。

INF 文件具有有效的 Authenticode 签名，如果**SetupVerifyInfFile**也 SP_INF_SIGNER_INFO 输出结构中会返回以下信息：

-   **DigitalSigner**成员设置为签名者的名称。

-   **CatalogFile**成员设置为相应的签名的编录文件的完整路径。

但是，请注意， **SetupVerifyInfFile**不会返回中的版本**DigitalSignerVersion**成员。

### <a name="to-verify-that-a-file-has-a-valid-authenticode-signature"></a>若要验证文件具有有效的 Authenticode 签名

调用安装程序 Api 函数**SetupScanFileQueue**使用 SPQ_SCAN_USE_CALLBACK_SIGNERINFO 标志。

**SetupScanFileQueue**将 SPFILENOTIFY_QUEUESCAN_SIGNERINFO 请求发送到调用方的回调例程，并将指针传递给 FILEPATHS_SIGNERINFO 结构。 如果文件已签名使用有效的 Authenticode 签名，该函数设置的错误代码为适当的 ERROR_AUTHENTICODE_Xxx 值的文件调用回调例程之前。 函数还将 FILEPATHS_SIGNERINFO 结构中设置的以下信息：

-   **DigitalSigner**成员设置为签名者的名称。

-   **CatalogFile**成员设置为相应的签名的编录文件的完整路径。

但是，请注意版本中未设置**版本**成员。

**SetupScanFileQueue** ERROR_AUTHENTICODE_Xxx 错误代码设置相同的方式，如本主题中前面所述**SetupVerifyInfFile**。

 

 





