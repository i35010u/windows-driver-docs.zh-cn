---
title: 使用 SPC 对目录文件进行签名
description: 使用 SPC 对目录文件进行签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e824d2d24312318cdab6493a9c8923d2df28378
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806239"
---
# <a name="signing-a-catalog-file-with-an-spc"></a>使用 SPC 对目录文件进行签名

使用以下 [**SignTool**](../devtest/signtool.md)命令通过 [软件发行者证书 (SPC)](software-publisher-certificate.md)对内核模式 [驱动程序包](driver-packages.md)的 [目录文件](catalog-files.md)进行签名。 对于64位版本的 Windows Vista 和更高版本的 Windows，没有 [WHQL 版本签名](whql-release-signature.md) 的内核模式驱动程序包必须使用 SPC 签名进行签名，以符合 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md) 和 [PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)。

```cpp
SignTool sign /v /ac CrossCertificateFile /s SPCCertificateStore /n SPCCertificateName /t http://timestamp.digicert.com CatalogFileName.cat
```

其中：

- **Sign** 命令将 SignTool 配置为对编录文件 *CatalogFileName.cat* 进行签名。

- **/V** verbose 选项将 SignTool 配置为打印执行和警告消息。

- **/Ac** *CrossCertificateFile* 选项指定与 *SPCCertificateName* 指定的软件发行者证书 (SPC) 相关联的交叉证书 *.cer* 文件。

- **/S** *SPCCertificateStore* 选项指定保存 *SPCCertificateName* 指定的软件发行者证书的证书存储区的名称。 如 [软件发行者证书 (SPC)](software-publisher-certificate.md)中所述，证书信息必须包含在 *.pfx* 文件中，并且必须将 *.pfx* 文件中的信息添加到本地计算机的 "个人" 证书存储中。 个人证书存储由选项 **/s my** 来指定。

- **/N** *SPCCertificateName* 选项指定 *SPCCertificateStore* 证书存储区中的证书名称。

- **/T** `http://timestamp.digicert.com` 选项提供 VeriSign 提供的公开可用的时间戳服务器的 URL。

- *CatalogFileName.cat* 是目录文件的名称。

例如，下面的命令用名为 "contoso.com" 的 SPC 在个人 "my" 证书存储和相应的交叉证书 *Rsacertsvrcross* 中对 *Tstamd64.cat* 目录文件进行签名。 签名由服务以时间戳 [https://timestamp.digicert.com](https://timestamp.digicert.com) 。 在此示例中，目录文件位于运行命令的同一目录中。

```cpp
SignTool sign /v /ac c:\lab\rsacertsrvcross.cer /s my /n contoso.com /t http://timestamp.digicert.com tstamd64.cat
```
