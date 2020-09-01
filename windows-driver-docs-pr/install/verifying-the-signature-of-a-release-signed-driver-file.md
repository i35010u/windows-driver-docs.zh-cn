---
title: 验证已进行发布签名的驱动程序文件的签名
description: 验证已进行发布签名的驱动程序文件的签名
ms.assetid: 70876389-6493-4c16-8a82-ca72fc23325c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6125b08024fa4bbe9016fa46b373bf926aeffa4
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097221"
---
# <a name="verifying-the-signature-of-a-release-signed-driver-file"></a>验证已进行发布签名的驱动程序文件的签名


若要验证由软件发行者证书创建的驱动程序文件中的嵌入签名 [ (SPC) ](software-publisher-certificate.md)，请使用以下 [**SignTool**](../devtest/signtool.md) 命令：

```cpp
SignTool verify /v /kp DriverFileName.sys
```

其中：

-   **Verify**命令将 SignTool 配置为验证嵌入驱动程序文件DriverFileName.sys 中的签名 *。*

-   **/V**选项将 SignTool 配置为打印执行和警告消息。

-   **/Kp**选项将 SignTool 配置为验证嵌入到*DriverFileName.sys*中的签名是否符合[内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)和 windows Vista 和更高版本的 windows 的[PnP 设备安装签名要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)。

-   *DriverFileName.sys* 是驱动程序文件的名称。

例如，下面的命令验证 *Toaster.sys* 是否具有有效的嵌入签名。 在此示例中，T*oaster.sys* 位于运行命令的目录下的 *amd64* 子目录中。

```cpp
SignTool verify /kp amd64\toaster.sys
```

 

