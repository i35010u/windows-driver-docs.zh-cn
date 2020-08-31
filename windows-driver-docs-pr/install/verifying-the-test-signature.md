---
title: 验证测试签名
description: 验证测试签名
ms.assetid: 996ce3d4-76b5-4c78-9ea9-ca8a04cfef99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d8b0b486ca669a6c600f626959579d78de25ac5
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094853"
---
# <a name="verifying-the-test-signature"></a>验证测试签名


将测试证书复制到测试计算机上的 "受信任的根证书颁发机构" 证书存储区后，可以使用 [**SignTool**](../devtest/signtool.md) 执行以下操作：

-   验证[驱动程序包](driver-packages.md)的 [目录文件](catalog-files.md)中指定文件的签名。

-   验证内核模式二进制文件的嵌入签名，如 *启动启动驱动程序*。

下面的示例在 Toastpkg.inf 示例的签名目录文件*tstamd64.cat*中验证一个文件*toastpkg.inf*的签名。 有关如何创建此目录文件的详细信息，请参阅 [使用 Inf2Cat 创建编录文件](using-inf2cat-to-create-a-catalog-file.md)：

```cpp
Signtool verify /pa /v /c tstamd64.cat toastpkg.inf
```

其中：

-   **Verify**命令将 SignTool 配置为验证指定的文件，而不是*oastpkg*。

-   **/Pa**选项指定在验证数字签名时使用 Authenticode 验证策略。

-   **/V**选项启用详细操作，其中，SignTool 显示成功执行和警告消息。

-   **/C**选项指定目录文件名称。

    **注意**   当验证嵌入的已签名内核模式二进制文件的签名时，请不要使用 **/c**参数。

     

-   *toastpkg.inf* 指定要验证的文件的名称。

下面的示例验证 *toastpkg.inf* 示例的已签名目录文件（ *Tstamd64.cat*）的签名：

```cpp
Signtool verify /pa /v tstamd64.cat
```

有关如何使用 [**SignTool**](../devtest/signtool.md) 验证目录文件的数字签名的详细信息，请参阅 [验证测试签名的目录文件的签名](verifying-the-signature-of-a-test-signed-catalog-file.md)。

 

