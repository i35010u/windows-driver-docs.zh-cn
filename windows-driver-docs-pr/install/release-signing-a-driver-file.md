---
title: 对驱动程序文件进行发布签名
description: 对驱动程序文件进行发布签名
ms.assetid: 3da0377d-57cf-4bd4-b3ce-6ba4ebbc3ceb
keywords:
- 公开发布的版本驱动程序签名 WDK，驱动程序文件
- 签名 WDK 的驱动程序文件版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21cfc1d62b2b9e0bf5a3d210bd5ca164c089a13c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375715"
---
# <a name="release-signing-a-driver-file"></a>对驱动程序文件进行发布签名


使用以下**SignTool** 64 位版本的 Windows Vista 和更高版本的 Windows 必须具有嵌入的 SPC 签名。

```cpp
SignTool sign /v /ac CrossCertificateFile /s SPCCertificateStore /n SPCCertificateName /t http://timestamp.verisign.com/scripts/timstamp.dll DriverFileName.sys
```

其中：

-   **符号**命令将配置 SignTool 将在文件中嵌入签名*DriverFileName.sys*。

-   **/V**详细选项配置 SignTool 打印执行消息和警告消息。

-   **/Ac** *CrossCertificateFile*选项指定交叉证书 *.cer*与由指定的 SPC 相关联的文件*SPCCertificateName*。

-   **/S** *SPCCertificateStore*选项指定的个人证书存储用于保存 SPC，指定的名称*SPCCertificateName*。 如中所述[软件发布者证书 (SPC)](software-publisher-certificate.md)，将证书信息必须包含在 *.pfx*文件和中的信息 *.pfx*文件必须为添加到本地计算机的个人证书存储中。 选项指定的个人证书存储 **/s 我**。

-   **/N** *SPCCertificateName*选项指定在证书的名称*SPCCertificateStore*证书存储区。

-   **/T**  * http://timestamp.verisign.com/scripts/timstamp.dll *选项提供 VeriSign 提供的公开可用的时间戳服务器的 URL。

-   *DriverFileName.sys*是驱动程序文件的名称。

以下命令将嵌入在签名*Toaster.sys* ，它是"my"证书存储区和相应的交叉证书从个人中名为"contoso.com"的证书生成*Rsacertsvrcross.cer*。 此外，该签名是时间戳服务加盖时间戳 http://timestamp.verisign.com/scripts/timstamp.dll。 在此示例中， *Toaster.sys*处于*amd64*在其中运行命令的目录下的子目录。

```cpp
SignTool sign /v /ac c:\lab\rsacertsrvcross.cer /s my /n contoso.com /t http://timestamp.verisign.com/scripts/timstamp.dll amd64\toaster.sys
```

 

 





