---
title: 指向并打印与包
description: 指向并打印与包
ms.assetid: ea160ffc-fca3-49e4-894d-67bdc65cda38
keywords:
- 点和打印 WDK，安全性
- 用户帐户控制 WDK 打印机
- UAC WDK 打印机
- 驱动程序存储区 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 302152102b31b63de4756aa2c842e9e1a7b4a977
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533923"
---
# <a name="point-and-print-with-packages"></a>指向并打印与包


驱动程序安装的包方法提供改进的安全点，并通过检查点和打印连接建立过程签名的驱动程序打印。

在 Windows Vista 上安装包识别的第三方驱动程序时，安装程序会自动将驱动程序包复制到驱动程序存储区，并再从驱动程序存储区中驱动程序包将安装驱动程序。 被认为已复制到驱动程序存储区的驱动程序包暂存在。

驱动程序包暂存在未立即安装在系统上，以便它们可用于安装更高版本。 将驱动程序包添加到驱动程序存储区，在安装过程中或分别需要管理员权限。 驱动程序包位于驱动程序存储区后，但是，标准用户可以安装该驱动程序。

由于驱动程序存储区是受信任存储区，将包添加到驱动程序存储区是一项特权的操作。 只能由管理员或已被授予针对设备策略的组策略的驱动程序安装权限的标准用户暂存在驱动程序。

 

 




