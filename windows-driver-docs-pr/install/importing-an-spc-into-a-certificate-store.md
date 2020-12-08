---
title: 将 SPC 导入证书存储
description: 将 SPC 导入证书存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 903208d2db439be49078d2ece071f69888d64c1f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840697"
---
# <a name="importing-an-spc-into-a-certificate-store"></a>将 SPC 导入证书存储


个人信息交换 (。已创建 *pfx*) 文件，用于存储 [ (SPC)](software-publisher-certificate.md) 及其私钥和公钥的软件发行者证书，则必须将 *.pfx* 文件导入到签名计算机上的个人证书存储区中。 有关 *.pfx* 文件的详细信息，请参阅 [个人信息交换 ( .pfx) 文件](personal-information-exchange---pfx--files.md)。

若要将 *.pfx* 文件导入到本地个人证书存储中，请执行以下操作：

1.  启动 Windows 资源管理器，选择并按住 (或右键单击该 *.pfx* 文件) ，然后选择 "打开" 以打开证书导入向导。

2.  按照证书导入向导中的步骤将代码签名证书导入到个人证书存储区中。

证书和私钥现可供 SignTool 使用。

从 Windows Vista 开始，将 *.pfx* 文件导入到本地个人证书存储中的另一种方法是使用 [CertUtil](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732443(v=ws.10)) 命令行实用程序。 以下命令行示例使用 CertUtil 将 *abc* 文件导入到个人证书存储中：

```cpp
certutil -user -p pfxpassword -importPFX abc.pfx
```

其中：

-   **-User** 选项指定 "当前用户" 的个人存储。

-   **-P** 选项指定 *.pfx* 文件 (*pfxpassword*) 的密码。

-   **-ImportPFX** 选项指定 *.pfx* 文件 (的名称 *) 。*

一旦将 *.pfx* 文件导入到签名计算机上的个人证书存储中，就可以使用 [**SignTool**](../devtest/signtool.md) 对 [驱动程序包](driver-packages.md)进行发布签名。

