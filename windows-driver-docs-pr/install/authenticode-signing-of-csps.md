---
title: 对第三方 CSP 进行验证码签名
description: 自定义加密服务提供程序的第三方验证码签名 (Csp) 已从 Windows Vista 开始提供，并已通过此下载返回到2013到的 Windows XP SP3 和 Windows Server 2003 SP2。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfe8f53376e062332b865e39d1cb91b92bf3ac20
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792851"
---
# <a name="authenticode-signing-of-third-party-csps"></a>对第三方 CSP 进行验证码签名

自定义加密服务提供程序的第三方验证码签名 (Csp) 已从 Windows Vista 开始提供，并已通过 [此下载](https://support.microsoft.com/help/2836198)返回到2013到的 WINDOWS XP SP3 和 windows SERVER 2003 SP2。

因此，Microsoft 将不再对 Csp 进行签名，并且手动 CSP 签名服务已停用。 cspsign@microsoft.comMicrosoft 将不再处理发送到或要签名的电子邮件和 csp cecspsig@microsoft.com 。

相反，所有第三方 Csp 现在都可以通过执行以下步骤自签名：

1. 从证书颁发机构购买一个代码签名证书， (CA) ，Microsoft 还颁发一个交叉证书。 " [内核模式代码签名的交叉证书](cross-certificates-for-kernel-mode-code-signing.md) " 主题提供了一个 ca 列表，其中 Microsoft 还提供了交叉证书和相应的交叉证书。 请注意，这些是与 Microsoft 颁发的 "Microsoft 代码验证根" 链接的唯一交叉证书，这会使 Windows 运行第三方 Csp。
2. 获得 CA 颁发的证书和匹配的交叉证书后，可以使用 [**SignTool**](../devtest/signtool.md) 对所有 CSP 二进制文件进行签名。
3. SignTool 包含在最新版本的 Visual Studio 中。 它还包含在 WDK 版本7.0 和更高版本中。 请注意，早期版本的 WDK 附带的 SignTool 与交叉证书不兼容，不能用于对二进制文件进行签名。

>[!NOTE]
>从 Windows 8 开始，不再需要 Csp 必须签名。

你可以从命令行对二进制文件进行签名，或在 Visual Studio 2012 和更高版本中作为集成生成步骤签名。

[**SignTool**](../devtest/signtool.md)的命令为：

```cpp
signtool.exe sign /ac <cross-certificate_from_ms> /sha1 <sha1_hash> /t <timestamp_server> /d <”optional_description_in_double_quotes”> <binary_file.ext>
```

- <跨 certificate_from_ca> 是从 Microsoft 下载的交叉证书文件
- <sha1_hash> 是对应于代码签名证书的 SHA1 指纹
- <timestamp_server> 是用于对签名操作进行时间戳的服务器
- < "optional_description_in_double_quotes" > 是可选友好名称描述
- <binary_file> 是要签名的文件

例如：

```cpp
signtool.exe sign /ac certificate.cer /sha1 553e39af9e0ea8c9edcd802abbf103166f81fa50 /t "http://timestamp.digicert.com" /d "My Cryptographic Service Provider" csp.dll
```

>[!NOTE]
>不需要 \# 在 CSP DLL 中包含资源 ID 666，或在注册表中包含签名，这是较旧的 CSP 签名所需的。

## <a name="additional-help-and-support"></a>其他帮助和支持

有关更多帮助和支持，请参阅 [故障排除和支持](https://msdn.microsoft.com/hh361695) 页。

你还可以查看 [Windows 桌面论坛的应用程序安全性](https://social.msdn.microsoft.com/Forums/home?forum=windowssecurity) 以获得帮助。
