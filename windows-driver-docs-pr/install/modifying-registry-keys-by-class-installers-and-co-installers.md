---
title: 通过类安装程序和辅助安装程序修改注册表项
description: 通过类安装程序和辅助安装程序修改注册表项
ms.assetid: A7F41F97-5E06-41d8-B80F-DDBC41A62BB3
keywords:
- 注册表 WDK 设备安装，修改注册表项
- 注册表 WDK 设备安装，修改注册表项类安装程序
- 注册表 WDK 设备安装，修改注册表项，共同安装程序
- 类安装程序 WDK 设备安装，修改注册表项
- 共同安装程序 WDK 设备安装，修改注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ab7836c01266cc19a03b133642ba39dbd44545f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567634"
---
# <a name="modifying-registry-keys-by-class-installers-and-co-installers"></a>通过类安装程序和辅助安装程序修改注册表项


**请注意**  通用或移动设备的驱动程序包中不支持在本部分中所述的功能。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

在某些情况下除外*类的安装程序*并*共同安装程序*不应使用标准注册表函数来创建、 更改或删除注册表项。 在大多数情况下，修改注册表项应仅使用指令都将置于[INF 文件](inf-files.md)。 这些指令的详细信息，请参阅[INF 指令摘要](summary-of-inf-directives.md)。

以下是此规则的例外情况：

-   在必要时，安装程序类和共同安装程序可以使用标准注册表函数修改中的注册表项**HKLM\\软件**子树。

    **请注意**  我们强烈建议安装程序类共同安装程序，作为内设备的条目保存自定义设备属性*软件密钥*。

     

-   安装程序类和共同安装程序有权修改项的子项中**HKLM\\系统\\CurrentControlSet\\控制\\CoDeviceInstallers**注册表项。

以下指导原则后应执行以安全地修改注册表项类安装程序或共同安装程序：

-   安装程序类和共同安装程序必须首先使用[ **SetupDiCreateDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff550973)或[ **SetupDiOpenDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552079)若要打开的句柄将修改注册表项。 打开句柄后，安装程序类和共同安装程序可以使用标准注册表函数修改注册表项。

-   不能使用安装程序类和共同安装程序**SetupDiDeleteDevRegKey**或*硬件密钥*设备。 有关详细信息，请参阅[删除设备的注册表项](deleting-the-registry-keys-of-a-device.md)。

有关标准注册表函数的详细信息，请参阅[注册表函数](https://go.microsoft.com/fwlink/p/?linkid=194529)。

 

 





