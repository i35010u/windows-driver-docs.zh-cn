---
title: 打开安装程序类中所有设备的软件键
description: 打开安装程序类中所有设备的软件键
ms.assetid: B601982E-FCD6-4932-813C-A68B2F15FC5C
keywords:
- 软件密钥 WDK 设备安装，打开安装程序类中的所有设备
- 安装程序类 WDK 设备安装，打开适用于设备的软件密钥
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71c3b5baffb5d9f08679ad64c399201e0b2003a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366647"
---
# <a name="opening-software-keys-for-all-devices-in-a-setup-class"></a>打开安装程序类中所有设备的软件键


在用户模式应用程序打开时*软件密钥*对于设备安装程序类中的所有设备，它必须不直接访问注册表，以枚举设备安装程序类的子项。 与任何注册表项，可能会更改的 Windows 不同版本之间的位置和此密钥的名称。

若要安全地枚举并打开设备安装程序类的子项，请按照下列步骤：

1.  使用[ **SetupDiGetClassDevs** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)或[ **SetupDiGetClassDevsEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsexa)检索一组指定的所有设备的信息设备安装程序类。

2.  使用[ **SetupDiEnumDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinfo)要枚举一组中的所有设备。

3.  使用[ **SetupDiOpenDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)打开每个设备的软件密钥。 *KeyType*参数必须设置为 DIREG_DRV。

**请注意**  某些设备可能没有软件密钥，例如，当设备是存在并且通过枚举[插即用 (PnP) 管理器](pnp-manager.md)，但未安装。

 

 

 





