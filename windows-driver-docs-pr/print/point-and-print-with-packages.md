---
title: 使用包进行点选打印
description: 使用包进行点选打印
keywords:
- 要点和打印 WDK，安全性
- 用户帐户控制 WDK 打印机
- UAC WDK 打印机
- 驱动程序存储 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d179c7ba9292257788b98e809886a90891c71b32
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807561"
---
# <a name="point-and-print-with-packages"></a>使用包进行点选打印


驱动程序安装包方法可在建立点和打印连接的过程中检查驱动程序签名，从而提高点和打印的安全性。

当在 Windows Vista 上安装了包感知第三方驱动程序时，安装程序会自动将驱动程序包复制到驱动程序存储区，然后从驱动程序存储区中的驱动程序包安装驱动程序。 已将已复制到驱动程序存储区中的驱动程序包称为暂存。

可以暂存驱动程序包，而无需立即将其安装在系统上，以便以后可以安装它们。 若要在安装过程中或单独添加驱动程序包，则需要管理员权限。 但是，驱动程序包位于驱动程序存储区中之后，标准用户可以安装驱动程序。

由于驱动程序存储是受信任的存储区，因此将包添加到驱动程序存储区是一种特权操作。 驱动程序只能通过组策略设备策略的管理员或已被授予驱动程序安装权限的标准用户进行暂存。

 

 




