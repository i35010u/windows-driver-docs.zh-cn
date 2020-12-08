---
title: 打开设备的硬件键
description: 打开设备的硬件键
keywords:
- 硬件密钥 WDK 设备安装，打开
- 打开硬件密钥 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e61b880eeca363c06aadf2a47df4b976da3668a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839073"
---
# <a name="opening-a-devices-hardware-key"></a>打开设备的硬件键


*硬件密钥* 是设备特定的注册表子项，其中包含有关设备的信息。 不得直接打开设备的硬件密钥。 与任何注册表项一样，这些注册表项的位置或格式在不同版本的 Windows 之间可能会更改。 

**注意**  仅当找到相应的设备后，才应打开设备的硬件密钥。 有关此过程的详细信息，请参阅 [枚举已安装设备](enumerating-installed-devices.md)。

 

若要打开或创建设备的硬件密钥，请遵循以下准则：

-   若要打开现有硬件密钥，请使用 [**SetupDiOpenDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendevregkey)。 若要创建硬件密钥，请使用 [**SetupDiCreateDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdicreatedevregkeya)。 在任一情况下，都必须将 *KeyType* 参数设置为 DIREG_DEV。

    **注意**  必须将 *samDesired* 参数设置为所需的最小访问权限。 不能将此参数设置为 KEY_ALL_ACCESS。 有关如何为注册表访问指定访问权限的详细信息，请参阅 [安全地访问注册表项](accessing-registry-keys-safely.md)。

     

-   内核模式调用方应使用 [**IoOpenDeviceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey) ，并将 *DevInstKeyType* 参数设置为 PLUGPLAY_REGKEY_DEVICE。

 

