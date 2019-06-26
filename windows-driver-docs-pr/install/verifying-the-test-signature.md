---
title: 验证测试签名
description: 验证测试签名
ms.assetid: 996ce3d4-76b5-4c78-9ea9-ca8a04cfef99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6f26a149f1ea3878723d9c8aa212e77f2cf542d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380413"
---
# <a name="verifying-the-test-signature"></a>验证测试签名


测试证书复制到测试计算机上的受信任的根证书颁发机构证书存储后[ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)可用于执行以下操作：

-   验证指定的文件中的签名[驱动程序包](driver-packages.md) [编录文件](catalog-files.md)。

-   验证嵌入的内核模式二进制文件，如*引导启动驱动程序*。

下面的示例验证的签名的文件之一*toastpkg.inf*，在 Toastpkg 示例的签名的编录文件中， *tstamd64.cat*。 有关如何创建此目录文件的详细信息，请参阅[使用 Inf2Cat 创建编录文件](using-inf2cat-to-create-a-catalog-file.md):

```cpp
Signtool verify /pa /v /c tstamd64.cat toastpkg.inf
```

其中：

-   **验证**命令将配置 SignTool 验证指定的文件中，t*oastpkg.inf*。

-   **/Pa**选项指定使用验证码验证策略时验证数字签名。

-   **/V**选项启用详细的操作，在其中 SignTool 显示成功执行消息和警告消息。

-   **/C**选项指定的目录文件名称。

    **请注意**  时验证嵌入签名的内核模式二进制文件的签名，请勿使用 **/c**参数。

     

-   *toastpkg.inf*指定要验证的文件的名称。

下面的示例验证的签名*Toastpkg*示例的签名的编录文件*Tstamd64.cat*:

```cpp
Signtool verify /pa /v tstamd64.cat
```

有关如何使用详细信息[ **SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)若要验证的数字签名的编录文件，请参阅[验证 Test-Signed 编录文件签名](verifying-the-signature-of-a-test-signed-catalog-file.md)。

 

 





