---
title: 打开注册表中的设备安装程序类
description: 打开注册表中的设备安装程序类
ms.assetid: B747EB2B-892C-4465-98E0-245FF7BC1E70
keywords:
- 注册表 WDK 设备安装，打开注册表中的设备安装程序类
- 设备安装程序类 WDK 设备安装，打开注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4ff3cb7321ee1a0a15f164e8d47f9fa1ce3cb88
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546133"
---
# <a name="opening-registry-keys-for-a-device-setup-class"></a>打开注册表中的设备安装程序类


并不直接访问设备安装程序类的注册表项。 与任何注册表项，可能会更改的 Windows 不同版本之间的位置和这些密钥的名称。

若要安全地打开的注册表项[设备安装程序类](device-setup-classes.md)，使用下列任一[SetupAPI](setupapi.md)函数：

-   [**SetupDiOpenClassRegKey**](https://msdn.microsoft.com/library/windows/hardware/ff552065)
-   [**SetupDiOpenClassRegKeyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552067)与*标志*参数设置为 DIOCR_INSTALLER

 

 





