---
title: 不推荐使用的 Ndi 值和键
description: Ndi 值和 Windows 2000 及更高版本中不推荐使用的密钥
ms.assetid: 932e1c83-feb6-47a8-bed3-847ee4094b9e
keywords:
- 添加注册表部分 WDK 网络、 Ndi 值和密钥
- Ndi 密钥 WDK 网络
- Ndi 值 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84224a135380761c23db7486004e22568c09da1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383609"
---
# <a name="deprecated-ndi-values-and-keys"></a>不推荐使用的 Ndi 值和键





**重要**  以下**Ndi** Windows 操作系统中不再使用注册表项和值。 如果要从 Windows 95/98/我迁移网络驱动程序，到更高版本的操作系统，请使用这些值。

 

**DeviceVxD**

**DevLoader**

**DriverDesc**

**InfFile**

**InfSelection**

**Ndi\\CardType**

**Ndi\\兼容性**

**Ndi\\DeviceID**

**Ndi\\**<em>filename</em>\\...

**Ndi\\安装**

**Ndi\\InstallInf**

**Ndi\\Interfaces\\DefLower**

**Ndi\\Interfaces\\DefUpper**

**Ndi\\Interfaces\\ExcludeAny**

**Ndi\\Interfaces\\RequireAny**

**Ndi\\NdiInstaller**

**Ndi\\**<em>param-key-name</em>**\\resc**

**Ndi\\Params\\**<em>param-key-name</em>**\\flag**

**Ndi\\Params\\**<em>param-key-name</em>**\\location**

**Ndi\\Remove**

**NDIS**\\...

**StaticVxD**

因为 Windows 不支持**Ndi\\**<em>参数密钥名称</em>**\\resc**并**Ndi\\Params\\**<em>参数密钥名称</em>**\\标志**的值，用户不能指定适配器资源通过**高级**属性页。

 

 





