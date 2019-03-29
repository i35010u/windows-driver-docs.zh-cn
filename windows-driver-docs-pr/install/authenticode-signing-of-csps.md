---
title: 对第三方 CSP 进行验证码签名
description: 第三方验证码签名的自定义加密服务提供商 (Csp) 已与 Windows Vista 开始提供，并且已经返回移植到 Windows XP SP3 和 Windows Server 2003 SP2 截至 2013 年 5 月，通过该下载内容。
ms.assetid: DBAA575A-F0B5-4725-A7B1-D6EA84977212
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6dc171573b04401fd293800dd12012ec496b535
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566017"
---
# <a name="authenticode-signing-of-third-party-csps"></a>对第三方 CSP 进行验证码签名


通过第三方验证码签名的自定义加密服务提供商 (Csp) 已被 Windows Vista 开始提供，并返回已移植到 Windows XP SP3 和 Windows Server 2003 SP2 截至 2013 年 5 月， [此下载](http://support.microsoft.com/kb/2836198).

因此，Microsoft 将无法再登录的 Csp，并且已停用手动签名服务的 CSP。 发送到电子邮件和 Cspcspsign@microsoft.com或cecspsig@microsoft.com进行签名将不再由处理 Microsoft。

相反，所有第三方 Csp 可以现在是自签名按照以下步骤：

1.  购买代码签名证书从证书颁发机构 (CA) 为其 Microsoft 也会发出交叉证书。 [内核模式代码签名的交叉证书](cross-certificates-for-kernel-mode-code-signing.md)主题提供了一系列 Microsoft 还提供交叉证书和相应的交叉证书的 Ca。 请注意，这些是唯一交叉证书链接到"Microsoft 代码验证根"将启用 Windows 运行第三方 Csp 的 Microsoft 发放的。
2.  从 CA 和匹配的交叉证书的证书后，可以使用[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)登录所有 CSP 二进制文件。
3.  SignTool 纳入最新版本的 Visual Studio。 它还包含在 WDK 版本 7.0 和更高版本。 请注意，附带了早期版本的 WDK SignTool 交叉证书与不兼容，并且不能用于签名二进制文件的位置。

**请注意**  从 Windows 8 开始，它不再是一项要求 Csp 必须进行签名。

 

您可以签名二进制文件从命令行中，或在 Visual Studio 2012 和更高版本的一个集成的生成步骤签名。

为命令[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)是：

```cpp
signtool.exe sign /ac <cross-certificate_from_ms> /sha1 <sha1_hash> /t <timestamp_server> /d <”optional_description_in_double_quotes”> <binary_file.ext>
```

-   &lt;跨 certificate_from_ca&gt;是从 Microsoft 下载交叉证书文件
-   &lt;sha1_hash&gt;是对应于代码签名证书的 SHA1 指纹
-   &lt;timestamp_server&gt;是使用的服务器添加时间戳签名的操作
-   &lt;"optional_description_in_double_quotes"&gt;的可选友好名称说明
-   &lt;binary_file.ext&gt;是要签名的文件

例如：

```cpp
signtool.exe sign /ac certificate.cer /sha1 553e39af9e0ea8c9edcd802abbf103166f81fa50 /t "http://timestamp.verisign.com/scripts/timstamp.dll" /d "My Cryptographic Service Provider" csp.dll
```

**请注意**  不需要包括资源 ID \#666 在 CSP DLL 中或在注册表中，因为针对较旧的 CSP 签名所需的签名。

 

## <a name="additional-help-and-support"></a>更多帮助和支持


请查阅[故障排除和支持](https://msdn.microsoft.com/hh361695)更多帮助和支持页。

您还可以检查[Windows 桌面应用程序安全](http://social.msdn.microsoft.com/Forums/home?forum=windowssecurity)论坛以获得帮助。

 

 





