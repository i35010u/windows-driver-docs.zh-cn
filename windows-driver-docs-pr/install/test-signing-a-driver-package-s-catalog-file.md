---
title: 对驱动程序包的目录文件进行测试签名
description: 对驱动程序包的目录文件进行测试签名
ms.assetid: 8cc54f57-bac3-45a1-b780-48626943b446
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b571acb71206973608a8a9ecb051abc3f70fbfa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339574"
---
# <a name="test-signing-a-driver-packages-catalog-file"></a>对驱动程序包的目录文件进行测试签名


之后[编录文件](catalog-files.md)有关[驱动程序包](driver-packages.md)创建或更新目录文件可以通过签名[ **SignTool**](https://msdn.microsoft.com/library/windows/hardware/ff551778)。 签名之后，目录文件中存储的数字签名会失效，如果驱动程序包的任何组件进行了修改。

当进行数字签名目录文件，SignTool 将保存编录文件中的数字签名。 SignTool 不更改驱动程序包的组件。 但是，由于目录文件包含的驱动程序包的组件的哈希的值，目录文件中的数字签名被维护，只要组件哈希处理为相同的值。

SignTool 还可以向数字签名添加时间戳。 时间戳，您可以确定创建的签名时，并支持更灵活的证书吊销选项，如有必要。

下面的命令行显示了如何运行 SignTool 将执行以下操作：

-   测试签名*tstamd64.cat*的编录文件*ToastPkg*示例[驱动程序包](driver-packages.md)。 详细了解如何为这[编录文件](catalog-files.md)已创建，请参见[测试签名的驱动程序包创建编录文件](creating-a-catalog-file-for-test-signing-a-driver-package.md)。

-   将从 PrivateCertStore Contoso.com(Test) 证书用于测试签名。 有关如何创建此证书的详细信息，请参阅[创建测试证书](creating-test-certificates.md)。

-   时间戳的时间戳颁发机构 (TSA) 通过数字签名。

对测试签名*tstamd64.cat*目录文件，请运行以下命令行：

```cpp
Signtool sign /v /s PrivateCertStore /n Contoso.com(Test) /t http://timestamp.verisign.com/scripts/timstamp.dll tstamd64.cat
```

其中：

-   **登录**命令配置指定的目录文件进行签名的 SignTool tstamd64.cat。

-   **/V**选项启用详细的操作，在其中 SignTool 显示成功执行消息和警告消息。

-   **/S**选项指定的证书存储区的名称 (*PrivateCertStore)* 包含的测试证书。

-   **/N**选项指定的证书名称 (*Contoso.com(Test))* 安装指定的证书存储区中。

-   **/T**选项指定 TSA 的 URL (*http://timestamp.verisign.com/scripts/timstamp.dll*) 这将时间戳的数字签名。
    **重要**  泄露密钥吊销签名者的代码签名的私钥的情况下包括时间戳提供所需的信息。

     

-   *tstamd64.cat*指定将对其进行数字签名的编录文件的名称。

有关 SignTool 及其命令行参数的详细信息，请参阅[ **SignTool**](https://msdn.microsoft.com/library/windows/hardware/ff551778)。

详细了解测试签名驱动程序包的目录文件，请参阅[测试签名目录文件](test-signing-a-catalog-file.md)。

 

 





