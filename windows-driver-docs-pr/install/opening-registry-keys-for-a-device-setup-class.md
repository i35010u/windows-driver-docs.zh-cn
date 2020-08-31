---
title: 打开设备安装程序类的注册表项
description: 打开设备安装程序类的注册表项
ms.assetid: B747EB2B-892C-4465-98E0-245FF7BC1E70
keywords:
- 注册表 WDK 设备安装，打开设备安装程序类的注册表项
- 设备设置类 WDK 设备安装，打开注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f747eac8d0f08137e6c91e40c8a3a5f5e69be81
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094979"
---
# <a name="opening-registry-keys-for-a-device-setup-class"></a>打开设备安装程序类的注册表项


不要直接访问设备安装程序类的注册表项。 与任何注册表项一样，这些密钥的位置和名称在不同版本的 Windows 之间可能会更改。

若要安全地打开 [设备安装程序类](./overview-of-device-setup-classes.md)的注册表项，请使用以下 [setupapi.log](setupapi.md) 函数之一：

-   [**SetupDiOpenClassRegKey**](/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkey)
-   [**SetupDiOpenClassRegKeyEx**](/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa) ，其 *Flags* 参数设置为 DIOCR_INSTALLER

 

