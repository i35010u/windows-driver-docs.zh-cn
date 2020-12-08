---
title: 对驱动程序文件进行发布签名
description: 对驱动程序文件进行发布签名
keywords:
- 公共版本驱动程序签名 WDK，驱动程序文件
- 驱动程序文件版本签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c9a5b2e49ac42cce2d44da2e0932fcb6e82e1db
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833485"
---
# <a name="release-signing-a-driver-file"></a>对驱动程序文件进行发布签名


使用以下 [**SignTool**](../devtest/signtool.md) 命令将软件发行者证书嵌入驱动程序文件 [ (SPC)](software-publisher-certificate.md) 签名。 为了符合 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)，64位版本的 windows Vista 和更高版本的 windows 的 *引导启动驱动程序* 必须具有嵌入的 SPC 签名。

```cpp
SignTool sign /v /ac CrossCertificateFile /s SPCCertificateStore /n SPCCertificateName /t http://timestamp.digicert.com DriverFileName.sys
```

其中：

- **Sign** 命令将 SignTool 配置为在文件 *DriverFileName.sys* 中嵌入签名。

- **/V** verbose 选项将 SignTool 配置为打印执行和警告消息。

- **/Ac** *CrossCertificateFile* 选项指定与 *SPCCertificateName* 指定的 SPC 关联的交叉证书 *.cer* 文件。

- **/S** *SPCCertificateStore* 选项指定保存 *SPCCertificateName* 指定的 SPC 的个人证书存储的名称。 如 [软件发行者证书 (SPC)](software-publisher-certificate.md)中所述，证书信息必须包含在 *.pfx* 文件中，并且必须将 *.pfx* 文件中的信息添加到本地计算机的 "个人" 证书存储中。 个人证书存储由选项 **/s my** 来指定。

- **/N** *SPCCertificateName* 选项指定 *SPCCertificateStore* 证书存储区中的证书名称。

- **/T**  * https://timestamp.digicert.com 选项提供 DigiCert 提供的公开可用的时间戳服务器的 URL。

- *DriverFileName.sys* 是驱动程序文件的名称。

以下命令在从个人 "我的" 证书存储中名为 "contoso.com" 的证书和相应的交叉证书 *Rsacertsvrcross* 生成的 *Toaster.sys* 中嵌入签名。 此外，签名由时间戳服务标记为时间戳 https://timestamp.digicert.com 。 在此示例中， *Toaster.sys* 位于运行命令的目录下的 *amd64* 子目录中。

```cpp
SignTool sign /v /ac c:\lab\rsacertsrvcross.cer /s my /n contoso.com /t http://timestamp.digicert.com amd64\toaster.sys
```
