---
title: 打开设备的硬件密钥
description: 打开设备的硬件密钥
ms.assetid: FED22F37-D09C-4207-8C2C-FB6484A8D19D
keywords:
- 硬件密钥 WDK 设备安装，打开
- 打开硬件密钥 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07321f59c1d5d516edf98cf588e47d57044c0714
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524564"
---
# <a name="opening-a-devices-hardware-key"></a>打开设备的硬件密钥


一个*硬件密钥*是特定于设备的注册表子项，其中包含有关设备的信息。 您必须直接打开设备的硬件密钥。 与任何注册表项，可能会更改的 Windows 不同版本之间的位置或这些项的格式。 

**请注意**  发现相应设备时，才应打开设备的硬件密钥。 有关此过程的详细信息，请参阅[枚举安装设备](enumerating-installed-devices.md)。

 

若要打开或创建设备的硬件密钥，请遵循以下准则：

-   若要打开现有的硬件密钥，请使用[ **SetupDiOpenDevRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552079)。 若要创建硬件密钥，请使用[ **SetupDiCreateDevRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff550973)。 在任一情况下，必须设置*KeyType* DIREG_DEV 参数。

    **请注意**  必须设置*samDesired*参数所需的最小访问权限。 您不设置此参数为 KEY_ALL_ACCESS。 有关如何指定注册表访问权限的访问权限的详细信息，请参阅[访问注册表密钥安全地](accessing-registry-keys-safely.md)。

     

-   内核模式调用方应使用[ **IoOpenDeviceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549443)并设置*DevInstKeyType* PLUGPLAY_REGKEY_DEVICE 参数。

 

 





