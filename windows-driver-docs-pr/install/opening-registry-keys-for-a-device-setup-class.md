---
title: 打开设备安装程序类的注册表项
description: 打开设备安装程序类的注册表项
keywords:
- 注册表 WDK 设备安装，打开设备安装程序类的注册表项
- 设备设置类 WDK 设备安装，打开注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a17d6f54c91cae45191ffb492b9b63dc37fee395
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793601"
---
# <a name="opening-registry-keys-for-a-device-setup-class"></a>打开设备安装程序类的注册表项


不要直接访问设备安装程序类的注册表项。 与任何注册表项一样，这些密钥的位置和名称在不同版本的 Windows 之间可能会更改。

若要安全地打开 [设备安装程序类](./overview-of-device-setup-classes.md)的注册表项，请使用以下 [setupapi.log](setupapi.md) 函数之一：

-   [**SetupDiOpenClassRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkey)
-   [**SetupDiOpenClassRegKeyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa) ，其 *Flags* 参数设置为 DIOCR_INSTALLER

 

