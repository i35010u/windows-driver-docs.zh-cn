---
title: 打开安装程序类中所有设备的软件键
description: 打开安装程序类中所有设备的软件键
ms.assetid: B601982E-FCD6-4932-813C-A68B2F15FC5C
keywords:
- 软件密钥 WDK 设备安装，打开安装程序类中的所有设备
- 安装程序类 WDK 设备安装，打开适用于设备的软件密钥
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 603a1cdc57e3645c02848c997af5deba9bf6bf58
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330262"
---
# <a name="opening-software-keys-for-all-devices-in-a-setup-class"></a>打开安装程序类中所有设备的软件键


在用户模式应用程序打开时*软件密钥*对于设备安装程序类中的所有设备，它必须不直接访问注册表，以枚举设备安装程序类的子项。 与任何注册表项，可能会更改的 Windows 不同版本之间的位置和此密钥的名称。

若要安全地枚举并打开设备安装程序类的子项，请按照下列步骤：

1.  使用[ **SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551069)或[ **SetupDiGetClassDevsEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551072)检索一组指定的所有设备的信息设备安装程序类。

2.  使用[ **SetupDiEnumDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff551010)要枚举一组中的所有设备。

3.  使用[ **SetupDiOpenDevRegKey** ](https://msdn.microsoft.com/library/windows/hardware/ff552079)打开每个设备的软件密钥。 *KeyType*参数必须设置为 DIREG_DRV。

**请注意**  某些设备可能没有软件密钥，例如，当设备是存在并且通过枚举[插即用 (PnP) 管理器](pnp-manager.md)，但未安装。

 

 

 





