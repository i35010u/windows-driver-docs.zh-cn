---
title: 打开安装程序类中所有设备的软件键
description: 打开安装程序类中所有设备的软件键
keywords:
- 软件密钥 WDK 设备安装，为安装程序类中的所有设备打开
- 设置类 WDK 设备安装，打开设备的软件密钥
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93f94c72492e33a36fc51aedaca40b9e5dd64d62
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840335"
---
# <a name="opening-software-keys-for-all-devices-in-a-setup-class"></a>打开安装程序类中所有设备的软件键


当用户模式应用程序打开设备安装程序类中所有设备的 *软件密钥* 时，它不能直接访问注册表来枚举设备安装程序类的子项。 与任何注册表项一样，此密钥的位置和名称在不同的 Windows 版本之间可能会发生更改。

若要安全地枚举并打开设备安装程序类的子项，请执行以下步骤：

1.  使用 [**SetupDiGetClassDevs**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsw) 或 [**SetupDiGetClassDevsEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsexa) 检索有关指定设备安装程序类的所有设备的信息集。

2.  使用 [**SetupDiEnumDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdienumdeviceinfo) 枚举集中的所有设备。

3.  使用 [**SetupDiOpenDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendevregkey) 打开每个设备的软件密钥。 *KeyType* 参数必须设置为 DIREG_DRV。

**注意**  某些设备可能没有软件密钥，例如，当设备存在并且 [即插即用 (PnP) manager](pnp-manager.md) 进行枚举但尚未安装。

 

 

