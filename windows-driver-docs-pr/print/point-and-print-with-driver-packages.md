---
title: 点选打印与驱动程序包
description: 点选打印与驱动程序包
keywords:
- 指向和打印 WDK，包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 220ca4a001153476fc0562f60023a9b84a268f53
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807563"
---
# <a name="point-and-print-with-driver-packages"></a>点选打印与驱动程序包


连接到打印服务器的打印客户端可以使用 "指向" 和 "打印" 复制整个驱动程序包以便进行安装。 使用 point 和 print with 包的优点是：

-   驱动程序的所有可运行组件都安装在打印客户端上。

-   在打印客户端上检查驱动程序签名和驱动程序完整性。

-   点和打印更值得信赖，并且管理员可在托管环境中更好地控制。

由于引入了驱动程序包，因此从 Windows 的早期版本开始，点和打印过程是不同的。 Windows Vista 使用包安装作为驱动程序安装的首选方法。 在早于 Windows Vista 的 Windows 版本中，指向和打印只能在客户端上安装基本打印功能。

驱动程序包安装需要驱动程序存储区，该存储区在早于 Windows Vista 的 Windows 版本上不可用。 当运行早期版本的 Windows 的客户端连接到 Windows Vista 打印服务器时，打印服务器将使用不带包的 "点" 和 "打印" 在客户端计算机上安装打印机。

 

 




