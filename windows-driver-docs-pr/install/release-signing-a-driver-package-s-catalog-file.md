---
title: 对驱动程序包的目录文件进行发布签名
description: 对驱动程序包的目录文件进行发布签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a29bf9a2216ade0ab14417f4c978d7e101622509
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785137"
---
# <a name="release-signing-a-driver-packages-catalog-file"></a>对驱动程序包的目录文件进行发布签名

创建或更新 [驱动程序包](driver-packages.md)的 [编录文件](catalog-files.md)后，即可通过 [**SignTool**](../devtest/signtool.md)对该目录文件进行签名。 签名后，如果修改了驱动程序包的任何组件，则存储在目录文件中的数字签名将会失效。

对编录文件进行数字签名时，SignTool 会将数字签名保存在目录文件中。 SignTool 不会更改驱动程序包的组件。 但是，由于目录文件包含驱动程序包的组件的哈希值，因此，只要这些组件将哈希到相同的值，就会保留目录文件中的数字签名。

SignTool 还可以向数字签名添加时间戳。 时间戳使你可以确定创建签名的时间，并在必要时支持更灵活的证书吊销选项。

以下命令行说明了如何运行 SignTool 来执行以下操作：

- 对 *toastpkg.inf* 示例 [驱动程序包](driver-packages.md)的 *tstamd64.cat* 目录文件进行发布签名。 有关如何创建此 [目录文件](catalog-files.md) 的详细信息，请参阅 [为 Release-Signing 驱动程序包创建编录文件](creating-a-catalog-file-for-release-signing-a-driver-package.md)。

- 使用商业证书颁发机构 (CA) 颁发的 [软件发行者证书 (SPC) ](software-publisher-certificate.md) 。

- 为 SPC 使用兼容的交叉证书。

- 通过时间戳颁发机构 (TSA) 为数字签名分配时间戳。

若要对 *tstamd64.cat* 目录文件进行发布签名，请运行以下命令行：

```cpp
Signtool sign /v /fd sha256 /ac MSCV-VSClass3.cer /s MyPersonalStore /n contoso.com /t http://timestamp.digicert.com tstamd64.cat
```

其中：

- **Sign** 命令将 SignTool 配置为对指定的编录文件 *tstamd64.cat* 进行签名。

- **/V** 选项启用详细操作，其中，SignTool 显示成功执行和警告消息。

- **/Fd** 选项指定用于创建文件签名的文件摘要算法。 默认值为 SHA1。

- **/Ac** 选项指定文件的名称，该文件包含从 CA 获取的交叉证书 (*MSCV-VSClass3*) 。 如果交叉证书不在当前目录中，请使用完整路径名称。

- **/S** 选项指定包含 SPC (*MyPersonalStore)* 的个人证书存储的名称。

- **/N** 选项指定在指定的证书存储中安装的 SPC (*Contoso.com)* 的名称。

- **/T** 选项指定 `http://timestamp.digicert.com` 将对数字签名进行时间戳的 TSA () 的 URL。

>[!IMPORTANT]
>包含时间戳会提供密钥吊销所需的信息，以防签名者的代码签名私钥泄漏。

- *tstamd64.cat* 指定将进行数字签名的目录文件的名称。

有关 SignTool 及其命令行参数的详细信息，请参阅 [**SignTool**](../devtest/signtool.md)。

有关发布签名驱动程序包的详细信息，请参阅 [发布签名驱动程序包](release-signing-driver-packages.md)。
