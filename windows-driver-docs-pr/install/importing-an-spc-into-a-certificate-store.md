---
title: 将 SPC 导入证书存储
description: 将 SPC 导入证书存储
ms.assetid: 4640b48c-e56f-4c6b-8943-f8b6fc3e37d7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35632ef0cc3d771ca3fbd743fcda68a1323711f5
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095709"
---
# <a name="importing-an-spc-into-a-certificate-store"></a>将 SPC 导入证书存储


个人信息交换 (。已创建*pfx*) 文件，用于存储 [ (SPC) ](software-publisher-certificate.md) 及其私钥和公钥的软件发行者证书，则必须将 *.pfx* 文件导入到签名计算机上的个人证书存储区中。 有关 *.pfx* 文件的详细信息，请参阅 [个人信息交换 ( .pfx) 文件](personal-information-exchange---pfx--files.md)。

若要将 *.pfx* 文件导入到本地个人证书存储中，请执行以下操作：

1.  启动 Windows 资源管理器，选择并按住 (或右键单击该 *.pfx* 文件) ，然后选择 "打开" 以打开证书导入向导。

2.  按照证书导入向导中的步骤将代码签名证书导入到个人证书存储区中。

证书和私钥现可供 SignTool 使用。

从 Windows Vista 开始，将 *.pfx* 文件导入到本地个人证书存储中的另一种方法是使用 [CertUtil](https://go.microsoft.com/fwlink/p/?linkid=168888) 命令行实用程序。 以下命令行示例使用 CertUtil 将 *abc* 文件导入到个人证书存储中：

```cpp
certutil -user -p pfxpassword -importPFX abc.pfx
```

其中：

-   **-User**选项指定 "当前用户" 的个人存储。

-   **-P**选项指定 *.pfx*文件 (*pfxpassword*) 的密码。

-   **-ImportPFX**选项指定 *.pfx*文件 (的名称 *) 。*

一旦将 *.pfx* 文件导入到签名计算机上的个人证书存储中，就可以使用 [**SignTool**](../devtest/signtool.md) 对 [驱动程序包](driver-packages.md)进行发布签名。

 

