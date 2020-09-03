---
title: BCDEdit /bootdebug
description: /Bootdebug boot 选项启用或禁用当前或指定的 Windows 操作系统启动项的启动调试。
ms.assetid: 85d0a25e-c411-4d7e-ae11-ce5bed1a37b8
ms.date: 04/22/2019
keywords:
- BCDEdit/bootdebug 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /bootdebug
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9bed13154526772a9ed998c42ebfc19f6decd8af
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384409"
---
# <a name="bcdedit-bootdebug"></a>BCDEdit /bootdebug


**/Bootdebug** boot 选项启用或禁用当前或指定的 Windows 操作系统启动项的启动调试。


``` syntax
    bcdedit /bootdebug [{ID}] { on | off } 
```

<a name="parameters"></a>参数
----------

**{**<em>ID</em>**}**

**{**<em>Id</em>**}** 是与启动项关联的 ID，如默认 OS 启动项的 {默认}。 如果未指定 **{**<em>ID</em>**}**，则该命令将修改当前处于活动状态的操作系统。 有关使用启动条目标识符的详细信息，请参阅 [启动选项标识符](boot-options-identifiers.md)。

**on**

启用指定启动项的启动调试。 如果未指定启动项，则为当前操作系统启用启动调试。

**off**

禁用指定启动项的启动调试。 如果未指定启动项，则为当前操作系统禁用启动调试。

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

### <a name="comments"></a>注释

**/Bootdebug** boot 选项启用特定启动项的启动调试。 使用 **/dbgsettings** 选项可配置要使用的调试连接的类型，以及连接参数 (*debugtype*) 。 

下表显示了 dbgsettings 的默认值。

|dbgsetting 参数|默认值|
|--- |--- |
|debugtype|Local|
|debugstart|活动|
|noumex|是|


以下命令启用了当前操作系统的 Windows 启动加载程序的启动调试。 Windows 启动加载器 ( # A0) 控制负载 UI，并加载内核启动驱动程序。

```
bcdedit /bootdebug on
```

以下命令禁用 ( # A0) 的 Windows 启动管理器的启动调试。 Windows 启动管理器选择将启动的操作系统，然后加载 Windows 启动加载程序。

```
bcdedit /bootdebug {bootmgr} off
```

在下面的示例中，通过命令，可以调试 Windows 启动管理器、启动加载程序，然后对操作系统进行内核调试。 这种组合允许在每个启动阶段进行调试。 如果使用此组合，则目标计算机将进入调试器三次：加载 Windows 启动管理器时、启动加载程序加载时以及操作系统启动时。

```
bcdedit /bootdebug {bootmgr} on 
bcdedit /bootdebug on 
bcdedit /debug on 
```

有关 Windows 调试工具的常规信息，请参阅 [Windows 调试](../debugger/index.md)。