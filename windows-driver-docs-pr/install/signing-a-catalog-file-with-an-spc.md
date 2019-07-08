---
title: 使用 SPC 对目录文件进行签名
description: 使用 SPC 对目录文件进行签名
ms.assetid: 8fe1fc32-73c9-4c09-96bd-93effb35c061
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f291bc2a2f2973c7f250f5cb405e6bb60602b715
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373485"
---
# <a name="signing-a-catalog-file-with-an-spc"></a>使用 SPC 对目录文件进行签名


使用以下[ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)命令以登录[编录文件](catalog-files.md)的内核模式[驱动程序包](driver-packages.md)与[软件发行者证书 (SPC)](software-publisher-certificate.md)。 对于 64 位版本的 Windows Vista 和更高版本的 Windows，而没有内核模式驱动程序包[WHQL 版本签名](whql-release-signature.md)必须使用 SPC 签名签名，以符合同时[内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)并[PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)。

```cpp
SignTool sign /v /ac CrossCertificateFile /s SPCCertificateStore /n SPCCertificateName /t http://timestamp.verisign.com/scripts/timstamp.dll CatalogFileName.cat
```

其中：

-   **符号**命令将配置为对目录文件进行签名的 SignTool *CatalogFileName.cat*。

-   **/V**详细选项配置 SignTool 打印执行消息和警告消息。

-   **/Ac** *CrossCertificateFile*选项指定交叉证书 *.cer*是软件发布者证书 (SPC) 具有关联的文件通过指定*SPCCertificateName*。

-   **/S** *SPCCertificateStore*选项指定包含软件发行者证书由指定的证书存储名称*SPCCertificateName*. 如中所述[软件发布者证书 (SPC)](software-publisher-certificate.md)，将证书信息必须包含在 *.pfx*文件和中的信息 *.pfx*文件必须为添加到本地计算机的个人证书存储中。 选项指定的个人证书存储 **/s 我**。

-   **/N** *SPCCertificateName*选项指定在证书的名称*SPCCertificateStore*证书存储区。

-   **/T**  *http://timestamp.verisign.com/scripts/timstamp.dll* 选项提供 VeriSign 提供的公开可用的时间戳服务器的 URL。

-   *CatalogFileName.cat*目录文件的名称。

例如，以下命令符号*Tstamd64.cat* SPC 使用目录文件命名为"contoso.com"中的个人，"my"证书存储区和相应的交叉证书*Rsacertsvrcross.cer*. 该签名是由服务加盖时间戳 http://timestamp.verisign.com/scripts/timstamp.dll 。 在此示例中，目录文件是在其中运行该命令的相同目录中。

```cpp
SignTool sign /v /ac c:\lab\rsacertsrvcross.cer /s my /n contoso.com /t http://timestamp.verisign.com/scripts/timstamp.dll tstamd64.cat 
```

 

 





