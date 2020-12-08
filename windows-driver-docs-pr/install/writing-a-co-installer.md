---
title: 编写辅助安装程序
description: 编写辅助安装程序
keywords:
- 设备设置 WDK 设备安装，共同安装程序
- 设备安装 WDK，共同安装程序
- 安装设备 WDK，共同安装程序
- 共同安装程序的 WDK 设备安装，关于共同安装程序
- coinstallers WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ed1d28dc534f7d84358b64a7e345a6b477f1952
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840931"
---
# <a name="writing-a-co-installer"></a>编写辅助安装程序





**注意**  通用或移动驱动程序包不支持本部分中介绍的功能。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

共同安装程序是帮助安装设备的 Microsoft Win32 DLL。 Setupapi.log 为类安装程序的 "帮助程序" 调用共同安装程序。 例如，供应商可以提供共同安装程序，将特定于设备的信息写入无法由 INF 文件处理的注册表中。

本节包括下列主题：

[辅助安装程序操作](co-installer-operation.md)

[辅助安装程序界面](co-installer-interface.md)

[辅助安装程序功能](co-installer-functionality.md)

[处理 DIF 代码](handling-dif-codes.md)

[注册辅助安装程序](registering-a-co-installer.md)

 

 





