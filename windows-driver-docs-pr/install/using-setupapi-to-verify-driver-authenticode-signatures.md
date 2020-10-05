---
title: 使用 SetupAPI 验证驱动程序验证码签名
description: 使用 SetupAPI 验证驱动程序验证码签名
ms.assetid: 2019d77d-2d98-4bae-8d9d-aa41e47f3811
keywords:
- Setupapi.log 函数 WDK，验证签名
- Authenticode 签名 WDK
- 签名 WDK，Authenticode
- 数字签名 WDK，Authenticode
- 验证验证码签名
- 检查 Authenticode 签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bef01cf96873fe824f2d09a42a64bca6593f636d
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732723"
---
# <a name="using-setupapi-to-verify-driver-authenticode-signatures"></a>使用 SetupAPI 验证驱动程序验证码签名





你可以使用以下过程来验证驱动程序是否具有有效的验证码 [数字签名](digital-signatures.md)。 从 Microsoft Windows Server 2003 开始支持这些过程。

### <a name="to-determine-whether-a-driver-has-a-valid-authenticode-signature"></a>确定驱动程序是否具有有效的 Authenticode 签名

检查 DNF_AUTHENTICODE_SIGNED 标志。

如果驱动程序具有有效的 Authenticode 签名，则 Windows 将此标志设置为驱动程序节点[**SP_DRVINSTALL_PARAMS**](/windows/win32/api/setupapi/ns-setupapi-sp_drvinstall_params)结构的**Flags**成员。  (还应注意，如果驱动程序具有 [WHQL 版本签名](whql-release-signature.md)（如果它是系统提供的驱动程序）或具有 Authenticode 签名，则 Windows 将设置 DNF_INF_IS_SIGNED 标志。 ) 

### <a name="to-verify-that-an-inf-file-has-a-valid-authenticode-signature"></a>验证 INF 文件是否具有有效的 Authenticode 签名

1.  调用 [INF 文件处理函数](inf-file-processing-functions.md) **SetupVerifyInfFile**。

2.  检查函数返回的错误代码。

    如果 INF 文件不是系统提供的，并且没有有效的 WHQL 数字签名，但它具有有效的 Authenticode 签名，则 **SetupVerifyInfFile** 将返回 **FALSE** ，且 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 返回以下错误代码之一：

    <a href="" id="error-authenticode-trusted-publisher"></a>ERROR_AUTHENTICODE_TRUSTED_PUBLISHER  
    指示发布服务器受信任，因为发行者的证书安装在 " [受信任的发行者" 证书存储](trusted-publishers-certificate-store.md)中。

    <a href="" id="error-authenticode-trust-not-established"></a>ERROR_AUTHENTICODE_TRUST_NOT_ESTABLISHED  
    指示由于不在受信任的发布者证书存储中安装发布服务器的签名证书，无法自动建立信任。 但是，这并不一定表示出现了错误。 相反，它指示调用方必须应用调用方特定的策略以在发布服务器中建立信任。

如果 INF 文件具有有效的 Authenticode 签名，则 **SetupVerifyInfFile** 还会在 SP_INF_SIGNER_INFO 输出结构中返回以下信息：

-   **DigitalSigner**成员设置为签名者的名称。

-   **CatalogFile**成员设置为相应的已签名目录文件的完整路径。

但请注意， **SetupVerifyInfFile** 不返回 **DigitalSignerVersion** 成员中的版本。

### <a name="to-verify-that-a-file-has-a-valid-authenticode-signature"></a>验证文件是否具有有效的 Authenticode 签名

使用 SPQ_SCAN_USE_CALLBACK_SIGNERINFO 标志调用 Setupapi.log 函数 **SetupScanFileQueue** 。

**SetupScanFileQueue** 将 SPFILENOTIFY_QUEUESCAN_SIGNERINFO 请求发送到调用方的回调例程，并传递指向 FILEPATHS_SIGNERINFO 结构的指针。 如果使用有效的验证码签名对文件进行签名，则在调用文件的回调例程之前，函数会将错误代码设置为相应的 ERROR_AUTHENTICODE_Xxx 值。 函数还在 FILEPATHS_SIGNERINFO 结构中设置以下信息：

-   **DigitalSigner**成员设置为签名者的名称。

-   **CatalogFile**成员设置为相应的已签名目录文件的完整路径。

但请注意，版本不是在 **版本** 成员中设置的。

**SetupScanFileQueue** 按照本主题中前面所述的 **SetupVerifyInfFile**设置 ERROR_AUTHENTICODE_Xxx 错误代码。

