---
title: Gcdef.dll，默认模拟设备属性表
description: Gcdef.dll，默认模拟设备属性表
ms.assetid: a8226abb-11c1-4425-93d8-b74e1960ba10
keywords:
- Gcdef.dll
- 默认模拟设备属性表
- 属性表 WDK DirectInput Gcdef.dll
- 游戏控制器 WDK DirectInput Gcdef.dll
- 控制面板 WDK DirectInput Gcdef.dll
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f35c7b345d28a843fda180dd31f36e3a0ceec614
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563858"
---
# <a name="gcdefdll-the-default-analog-device-property-sheet"></a>Gcdef.dll，默认模拟设备属性表





硬件供应商不创建其自己的控制面板使用默认模拟设备属性表由 Gcdef.dll 提供的服务。 不具有任何控制器**ConfigCLSID**注册表项下的键及其**HKEY\_本地\_机\\系统\\CurrentControlSet\\控件\\MediaProperties\\PrivateProperties\\游戏杆\\OEM\\**<em>控制器\_名称</em>条目使用此默认属性表。 此属性页包含以下两个页面：

-   **测试：** 本页演示设备正确响应。 它返回与设备属性相关联的注册表设置的图形表示形式，并允许用户对其进行查看。

-   **设置：** 此页允许用户将有关设备的特定信息写入到系统。 服务提供的校准以及方向舵或脚踏板。

 

 




