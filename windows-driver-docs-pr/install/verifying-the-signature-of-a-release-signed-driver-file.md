---
title: 验证已进行发布签名的驱动程序文件的签名
description: 验证已进行发布签名的驱动程序文件的签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20db533aa1265c762facc8f2ac2c1e8cc2f6ddc7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840949"
---
# <a name="verifying-the-signature-of-a-release-signed-driver-file"></a>验证已进行发布签名的驱动程序文件的签名


若要验证由软件发行者证书创建的驱动程序文件中的嵌入签名 [ (SPC)](software-publisher-certificate.md)，请使用以下 [**SignTool**](../devtest/signtool.md) 命令：

```cpp
SignTool verify /v /kp DriverFileName.sys
```

其中：

-   **Verify** 命令将 SignTool 配置为验证嵌入驱动程序文件DriverFileName.sys 中的签名 *。*

-   **/V** 选项将 SignTool 配置为打印执行和警告消息。

-   **/Kp** 选项将 SignTool 配置为验证嵌入到 *DriverFileName.sys* 中的签名是否符合 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)和 windows Vista 和更高版本的 windows 的 [PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)。

-   *DriverFileName.sys* 是驱动程序文件的名称。

例如，下面的命令验证 *Toaster.sys* 是否具有有效的嵌入签名。 在此示例中，T *oaster.sys* 位于运行命令的目录下的 *amd64* 子目录中。

```cpp
SignTool verify /kp amd64\toaster.sys
```

 

