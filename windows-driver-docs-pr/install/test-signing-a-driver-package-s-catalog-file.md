---
title: 对驱动程序包的目录文件进行测试签名
description: 对驱动程序包的目录文件进行测试签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d603f0a372a2b6e8b8bde532db5133dee20bb94a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826781"
---
# <a name="test-signing-a-driver-packages-catalog-file"></a>对驱动程序包的目录文件进行测试签名

创建或更新 [驱动程序包](driver-packages.md)的 [编录文件](catalog-files.md)后，可以通过 [**SignTool**](../devtest/signtool.md)对该目录文件进行签名。 签名后，如果修改了驱动程序包的任何组件，则存储在目录文件中的数字签名将会失效。

对编录文件进行数字签名时，SignTool 会将数字签名保存在目录文件中。 SignTool 不会更改驱动程序包的组件。 但是，由于目录文件包含驱动程序包的组件的哈希值，因此，只要这些组件将哈希到相同的值，就会保留目录文件中的数字签名。

SignTool 还可以向数字签名添加时间戳。 时间戳允许确定创建签名的时间，并在必要时支持更灵活的证书吊销选项。

以下命令行说明了如何运行 SignTool 来执行以下操作：

- 对 *toastpkg.inf* 示例 [驱动程序包](driver-packages.md)的 *tstamd64.cat* 目录文件进行测试签名。 有关如何创建此 [目录文件](catalog-files.md) 的详细信息，请参阅 [为 Test-Signing 驱动程序包创建编录文件](creating-a-catalog-file-for-test-signing-a-driver-package.md)。

- 使用 Contoso.com (测试 PrivateCertStore 中的) 证书来测试签名。 有关如何创建此证书的详细信息，请参阅 [创建测试证书](creating-test-certificates.md)。

- 通过时间戳颁发机构 (TSA) 来标记数字签名。

若要对 *tstamd64.cat* 目录文件进行测试签名，请运行以下命令行：

```cpp
Signtool sign /v /fd sha256 /s PrivateCertStore /n Contoso.com(Test) /t http://timestamp.digicert.com tstamd64.cat
```

其中：

- **Sign** 命令将 SignTool 配置为对指定的编录文件 tstamd64.cat 进行签名。

- **/V** 选项启用详细操作，其中，SignTool 显示成功执行和警告消息。

- **/Fd** 选项指定用于创建文件签名的文件摘要算法。 默认值为 SHA1。

- **/S** 选项指定包含测试证书的证书存储 (*PrivateCertStore)* 的名称。

- **/N** 选项指定在指定的证书存储中安装的 (*Contoso.com (测试) # B3* 的证书的名称。

- **/T** 选项指定了 `http://timestamp.digicert.com` 用于对数字签名进行时间戳的 TSA () 的 URL。

   >[!IMPORTANT]
   >包含时间戳会提供密钥吊销所需的信息，以防签名者的代码签名私钥泄漏。

- *tstamd64.cat* 指定将进行数字签名的目录文件的名称。

有关 SignTool 及其命令行参数的详细信息，请参阅 [**SignTool**](../devtest/signtool.md)。

有关对驱动程序包的目录文件进行测试签名的详细信息，请参阅对 [编录文件进行测试签名](test-signing-a-catalog-file.md)。
