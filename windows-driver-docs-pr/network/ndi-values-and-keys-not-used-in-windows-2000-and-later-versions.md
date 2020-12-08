---
title: 弃用的 Ndi 值和键
description: Windows 2000 及更高版本中弃用的 Ndi 值和密钥
keywords:
- 添加-注册表--WDK 网络、Ndi 值和密钥
- Ndi 密钥 WDK 网络
- Ndi 值 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 199ee202242ec18368908aba749ab9ed7e521291
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798051"
---
# <a name="deprecated-ndi-values-and-keys"></a>弃用的 Ndi 值和键





**重要提示**  以下 **Ndi** 注册表项和值不再用于 Windows 操作系统。 如果要将网络驱动程序从 Windows 95/98/Me 迁移到更高版本的操作系统，请不要使用这些值。

 

**DeviceVxD**

**DevLoader**

**DriverDesc**

**InfFile**

**InfSelection**

**Ndi \\ CardType**

**Ndi \\ 兼容性**

**Ndi \\ DeviceID**

**Ndi \\**<em>filename</em> \\...

**Ndi \\ 安装**

**Ndi \\ InstallInf**

**Ndi \\ 接口 \\ DefLower**

**Ndi \\ 接口 \\ DefUpper**

**Ndi \\ 接口 \\ ExcludeAny**

**Ndi \\ 接口 \\ RequireAny**

**Ndi \\ NdiInstaller**

**Ndi \\**<em>param-名称</em>**\\ resc**

**Ndi \\Params \\**<em>参数键名称</em>**\\ 标志**

**Ndi \\Params \\**<em>参数-名称</em>**\\ 位置**

**Ndi \\ 删除**

**NDIS** \\...

**StaticVxD**

由于 Windows 不支持 **Ndi \\**<em>param-name</em>**\\ resc** 和 **Ndi \\ \\ Params**<em>param-name</em>**\\ 标志** 值，用户无法通过 "**高级** 属性" 页指定适配器资源。

 

 





