---
title: 打开设备的软件键
description: 打开设备的软件键
ms.assetid: CA9EC186-7991-4cc5-B49E-DFE87A13BCFA
keywords:
- 软件密钥 WDK 设备安装，打开
- 打开软件密钥 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0625240bf094b030caeae8ba7e267b399df33147
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366655"
---
# <a name="opening-a-devices-software-key"></a>打开设备的软件键


您必须直接打开设备的*软件密钥*。 与任何注册表项，可能会更改的 Windows 不同版本之间的位置或这些项的格式。

**请注意**  发现相应设备时，才应打开设备的软件密钥。 有关此过程的详细信息，请参阅[枚举安装设备](enumerating-installed-devices.md)。

 

若要打开设备的软件密钥，请遵循以下准则：

-   若要打开现有的软件密钥，请使用[ **SetupDiOpenDevRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)。 若要创建软件密钥，请使用[ **SetupDiCreateDevRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)。 在任一情况下，必须设置*KeyType* DIREG_DRV 参数。

    **请注意**  必须设置*samDesired*参数所需的最小访问权限。 您不设置此参数为 KEY_ALL_ACCESS。 有关如何指定注册表访问权限的访问权限的详细信息，请参阅[访问注册表密钥安全地](accessing-registry-keys-safely.md)。

     

-   内核模式调用方应使用[ **IoOpenDeviceRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey)并设置*DevInstKeyType* PLUGPLAY_REGKEY_DRIVER 参数。

 

 





