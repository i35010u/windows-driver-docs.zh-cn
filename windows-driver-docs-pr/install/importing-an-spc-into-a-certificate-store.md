---
title: 将 SPC 导入证书存储
description: 将 SPC 导入证书存储
ms.assetid: 4640b48c-e56f-4c6b-8943-f8b6fc3e37d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22b26a4e5451b969171e9f18671c1d4c1313274b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385930"
---
# <a name="importing-an-spc-into-a-certificate-store"></a>将 SPC 导入证书存储


一次个人信息交换 (。*pfx*) 文件创建用于存储[软件发布者证书 (SPC)](software-publisher-certificate.md)及其专用和公共密钥， *.pfx*文件必须在导入个人证书存储签名的计算机。 有关详细信息 *.pfx*文件，请参阅[个人信息交换 (.pfx) 文件](personal-information-exchange---pfx--files.md)。

若要导入 *.pfx*文件到本地的个人证书存储中，执行以下操作：

1.  启动 Windows 资源管理器，然后双击 *.pfx*文件以打开证书导入向导。

2.  按照证书导入向导导入个人证书存储的代码签名证书中的过程。

现可 signtool 若要使用的证书和私钥。

从 Windows Vista 中，一种方法来导入 *.pfx*到本地的个人证书存储的文件是与[CertUtil](https://go.microsoft.com/fwlink/p/?linkid=168888)命令行实用程序。 下面的命令行示例使用 CertUtil 来导入*abc.pfx*的个人证书存储到文件：

```cpp
certutil -user -p pfxpassword -importPFX abc.pfx
```

其中：

-   **-用户**选项指定"当前用户"个人存储区。

-   **-P**选项指定的密码 *.pfx*文件 (*pfxpassword*)。

-   **-ImportPFX**选项指定的名称 *.pfx*文件 (*abc.pfx*)。

一次 *.pfx*文件导入到签名的计算机上的个人证书存储，则可以使用[ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)发行登录[驱动程序包](driver-packages.md)。

 

 





