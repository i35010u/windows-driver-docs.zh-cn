---
title: 对驱动程序文件进行发布签名
description: 对驱动程序文件进行发布签名
ms.assetid: 3da0377d-57cf-4bd4-b3ce-6ba4ebbc3ceb
keywords:
- 公共版本驱动程序签名 WDK, 驱动程序文件
- 驱动程序文件版本签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 086bae5bf2b76aca3bc3031f88a131087ab340d2
ms.sourcegitcommit: 2231d322eb4e9597ad7f537a4aa82b83422bd46a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70020636"
---
# <a name="release-signing-a-driver-file"></a>对驱动程序文件进行发布签名


使用适用于64位版本的 Windows Vista 和更高版本 Windows 的**SignTool**必须具有嵌入的 SPC 签名。

```cpp
SignTool sign /v /ac CrossCertificateFile /s SPCCertificateStore /n SPCCertificateName /t http://timestamp.digicert.com DriverFileName.sys
```

其中：

-   **Sign**命令将 SignTool 配置为在*DriverFileName*文件中嵌入签名。

-   **/V** verbose 选项将 SignTool 配置为打印执行和警告消息。

-   **/Ac** *CrossCertificateFile*选项指定与*SPCCertificateName*指定的 SPC 关联的交叉证书 *.cer*文件。

-   **/S** *SPCCertificateStore*选项指定保存*SPCCertificateName*指定的 SPC 的个人证书存储的名称。 如[软件发行者证书 (SPC)](software-publisher-certificate.md)中所述, 证书信息必须包含在 *.pfx*文件中, 并且必须将 *.pfx*文件中的信息添加到本地计算机的 "个人" 证书存储中。 个人证书存储由选项 **/s my**来指定。

-   **/N** *SPCCertificateName*选项指定*SPCCertificateStore*证书存储区中的证书名称。

-   **/T**  *http://timestamp.digicert.com 选项提供 VeriSign 提供的公开可用的时间戳服务器的 URL。

-   *DriverFileName*是驱动程序文件的名称。

下面的命令将在 Toaster 中嵌入一个签名, 该签名是从个人 "my" 证书存储中名为 "contoso.com" 的证书和相应的交叉证书*Rsacertsvrcross*生成的 *。* 此外, 签名由时间戳服务 http://timestamp.digicert.com 标记为时间戳。 在此示例中, *Toaster*位于运行命令的目录下的*amd64*子目录中。

```cpp
SignTool sign /v /ac c:\lab\rsacertsrvcross.cer /s my /n contoso.com /t http://timestamp.digicert.com amd64\toaster.sys
```

 

 





