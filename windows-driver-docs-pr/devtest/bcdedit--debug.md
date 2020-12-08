---
title: BCDEdit /debug
description: /debug 启动选项可启用或禁用与指定的启动项目或当前启动项目关联的 Windows 操作系统的内核调试。
ms.date: 04/22/2019
keywords:
- BCDEdit/debug 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /debug
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7ae796c2441a635a37fe9a72619e7d6e82e9d05b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824269"
---
# <a name="bcdedit-debug"></a>BCDEdit /debug


**/Debug** boot 选项启用或禁用与指定启动项或当前启动项关联的 Windows 操作系统的内核调试。

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。


``` syntax
bcdedit /debug [{ID}] { on | off }
```

<a name="parameters"></a>参数
----------

**{**<em>ID</em>**}**   

**{**<em>Id</em>**}** 是与启动项关联的 ID，如默认 OS 启动项的 {默认}。 如果未指定 **{**<em>ID</em>**}**，则该命令将修改当前处于活动状态的操作系统。 有关使用启动条目标识符的详细信息，请参阅 [启动选项标识符](boot-options-identifiers.md)。

 **基于**   
启用指定启动项的内核调试。 如果未指定启动项，则为当前操作系统启用内核调试。

**非**   
禁用指定启动项的内核调试器。 如果未指定启动项，则为当前操作系统禁用内核调试。

### <a name="comments"></a>注释

**/Debug** boot 选项对特定启动条目启用内核调试。 使用 **/dbgsettings** 选项可配置要使用的调试连接的类型和连接参数。 如果没有为启动项指定 **/dbgsettings** ，则使用全局调试设置。 下表显示了全局设置的默认值。

|dbgsetting 参数|默认值|
|--- |--- |
|debugtype|Local|
|debugstart|可用|
|noumex|是|


下面的示例启用了默认启动项的内核调试。

```console
bcdedit /debug on 
```

有关 Windows 调试工具的信息，请参阅 [Windows 调试](../debugger/index.md) 和 [自动设置 KDNET 网络内核调试](../debugger/setting-up-a-network-debugging-connection-automatically.md)
