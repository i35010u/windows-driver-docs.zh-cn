---
title: 打开设备安装程序类的注册表项
description: 打开设备安装程序类的注册表项
ms.assetid: B747EB2B-892C-4465-98E0-245FF7BC1E70
keywords:
- 注册表 WDK 设备安装，打开注册表中的设备安装程序类
- 设备安装程序类 WDK 设备安装，打开注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d6e67a92cc35506af4868f7477f07a9fe0156dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366645"
---
# <a name="opening-registry-keys-for-a-device-setup-class"></a>打开设备安装程序类的注册表项


并不直接访问设备安装程序类的注册表项。 与任何注册表项，可能会更改的 Windows 不同版本之间的位置和这些密钥的名称。

若要安全地打开的注册表项[设备安装程序类](device-setup-classes.md)，使用下列任一[SetupAPI](setupapi.md)函数：

-   [**SetupDiOpenClassRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey)
-   [**SetupDiOpenClassRegKeyEx** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa)与*标志*参数设置为 DIOCR_INSTALLER

 

 





