---
title: 打开设备的软件键
description: 打开设备的软件键
ms.assetid: CA9EC186-7991-4cc5-B49E-DFE87A13BCFA
keywords:
- 软件密钥 WDK 设备安装，打开
- 打开软件密钥 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f6f9dd285b1edcea3e9d8c8e78e82b16548720b
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716168"
---
# <a name="opening-a-devices-software-key"></a>打开设备的软件键


不得直接打开设备的 *软件密钥*。 与任何注册表项一样，这些注册表项的位置或格式在不同版本的 Windows 之间可能会更改。

**注意**   仅当找到相应的设备后，才应打开设备的软件密钥。 有关此过程的详细信息，请参阅 [枚举已安装设备](enumerating-installed-devices.md)。

 

若要打开设备的软件密钥，请遵循以下准则：

-   若要打开现有的软件密钥，请使用 [**SetupDiOpenDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendevregkey)。 若要创建软件密钥，请使用 [**SetupDiCreateDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdicreatedevregkeya)。 在任一情况下，都必须将 *KeyType* 参数设置为 DIREG_DRV。

    **注意**   必须将*samDesired*参数设置为所需的最小访问权限。 不能将此参数设置为 KEY_ALL_ACCESS。 有关如何为注册表访问指定访问权限的详细信息，请参阅 [安全地访问注册表项](accessing-registry-keys-safely.md)。

     

-   内核模式调用方应使用 [**IoOpenDeviceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey) ，并将 *DevInstKeyType* 参数设置为 PLUGPLAY_REGKEY_DRIVER。

 

