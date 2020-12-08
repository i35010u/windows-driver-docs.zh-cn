---
title: 已安装显示驱动程序的指令
description: 已安装的显示驱动程序指令是一个软件设备设置，它为作为驱动程序包的一部分安装的 UMD 提供了正确的名称。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b73ecbf12a3ba9819c5020d454f29ea3d6ec75e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839287"
---
# <a name="installed-display-drivers-directive"></a>已安装显示驱动程序的指令


已安装的显示驱动程序指令是一个软件设备设置，它为作为驱动程序包的一部分安装的 UMD 提供了正确的名称。

``` syntax
HKR,, InstalledDisplayDrivers,              %REG_MULTI_SZ%, 
UserModeDriverName1, UserModeDriverName2, UserModeDriverNameWow1, UserModeDriverNameWow2
```

例如：

``` syntax
For example:
X86:
HKR,, InstalledDisplayDrivers,              %REG_MULTI_SZ%, r200umd

X64:
HKR,, InstalledDisplayDrivers,              %REG_MULTI_SZ%, r200umd, r200umdva, r200umd64, r200umd64va
```

 

 





