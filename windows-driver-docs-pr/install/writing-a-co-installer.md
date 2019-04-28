---
title: 编写辅助安装程序
description: 编写辅助安装程序
ms.assetid: d5637321-9cff-4b24-8941-d3ca16b0d8c1
keywords:
- 设备安装程序 WDK 设备安装，共同安装程序
- 设备安装 WDK，共同安装程序
- 安装设备 WDK，共同安装程序
- 共同安装程序 WDK 设备安装，有关共同安装程序
- WDK 共同安装程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 812c7d40cf4da3d6c323f92fd934faea7c8ecf24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339258"
---
# <a name="writing-a-co-installer"></a>编写辅助安装程序





**请注意**  通用或移动设备的驱动程序包中不支持在本部分中所述的功能。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

辅助安装程序是可帮助您进行设备安装的 Microsoft Win32 DLL。 共同安装程序安装程序 Api 调用为"帮助器"对于类的安装程序。 例如，供应商可以提供特定于设备的信息写入到注册表中不能由 INF 文件处理的共同安装程序。

本部分包括以下主题：

[辅助安装程序操作](co-installer-operation.md)

[共同安装程序界面](co-installer-interface.md)

[辅助安装程序功能](co-installer-functionality.md)

[处理 DIF 代码](handling-dif-codes.md)

[注册辅助安装程序](registering-a-co-installer.md)

 

 





