---
title: 打开设备的硬件键
description: 打开设备的硬件键
ms.assetid: FED22F37-D09C-4207-8C2C-FB6484A8D19D
keywords:
- 硬件密钥 WDK 设备安装，打开
- 打开硬件密钥 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecee18dee8a40cf47582ae02ed33eb41edbeede8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837399"
---
# <a name="opening-a-devices-hardware-key"></a>打开设备的硬件键


*硬件密钥*是设备特定的注册表子项，其中包含有关设备的信息。 不得直接打开设备的硬件密钥。 与任何注册表项一样，这些注册表项的位置或格式在不同版本的 Windows 之间可能会更改。 

**请注意**  仅在找到相应的设备后才打开设备的硬件密钥。 有关此过程的详细信息，请参阅[枚举已安装设备](enumerating-installed-devices.md)。

 

若要打开或创建设备的硬件密钥，请遵循以下准则：

-   若要打开现有硬件密钥，请使用[**SetupDiOpenDevRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)。 若要创建硬件密钥，请使用[**SetupDiCreateDevRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)。 在任一情况下，都必须将*KeyType*参数设置为 DIREG_DEV。

    **请注意**  必须将*samDesired*参数设置为所需的最小访问权限。 不能将此参数设置为 KEY_ALL_ACCESS。 有关如何为注册表访问指定访问权限的详细信息，请参阅[安全地访问注册表项](accessing-registry-keys-safely.md)。

     

-   内核模式调用方应使用[**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey) ，并将*DevInstKeyType*参数设置为 PLUGPLAY_REGKEY_DEVICE。

 

 





