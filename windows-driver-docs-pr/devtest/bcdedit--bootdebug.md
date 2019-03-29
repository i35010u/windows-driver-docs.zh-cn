---
title: BCDEdit /bootdebug
description: /Bootdebug 启动选项启用或禁用的当前或指定 Windows 操作系统启动项目的调试启动。
ms.assetid: 85d0a25e-c411-4d7e-ae11-ce5bed1a37b8
ms.date: 05/21/2018
keywords:
- BCDEdit /bootdebug 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /bootdebug
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bb7b5a8daf8b13a7d6539e3767612b7b95512b90
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576039"
---
# <a name="bcdedit-bootdebug"></a>BCDEdit /bootdebug


**/Bootdebug**启动选项启用或禁用的当前或指定 Windows 操作系统启动项目的调试启动。

> [!NOTE]
> 设置 BCDEdit 选项之前，您可能需要禁用或暂停 BitLocker 和安全启动的计算机上。

 

``` syntax
    bcdedit /bootdebug [{ID}] { on | off } 
   
```

<a name="parameters"></a>Parameters
----------

**{**<em>ID</em>**}**   

**{**<em>ID</em>**}** 是与启动条目关联的 GUID。 如果未指定 **{**<em>ID</em>**}**，命令将修改当前处于活动状态的操作系统。 如果指定的启动项，则与启动项关联的 GUID 必须括在大括号**{}**。

**on**   

启用启动调试的指定的启动项目。 如果未指定的启动项，则为当前操作系统启用启动调试。

**off**   

禁用启动指定的启动项目的调试。 如果未指定的启动项，则时禁用当前操作系统的启动调试。

### <a name="comments"></a>备注

**/Bootdebug**启动选项启用启动调试特定的启动项。 使用 **/dbgsettings**选项，若要配置的调试连接类型 (*debugtype*) 对使用和连接参数。 如果没有 **/dbgsettings**指定为启动项目中，将使用全局调试设置。 下表中列出的全局设置的默认值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">dbgsetting 参数</th>
<th align="left">默认值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Debugtype</p></td>
<td align="left"><p>序列</p></td>
</tr>
<tr class="even">
<td align="left"><p>Debugport</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Baudrate</p></td>
<td align="left"><p>115200</p></td>
</tr>
</tbody>
</table>

 

有关 Windows 调试工具的信息，请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)。 有关设置和配置内核模式调试会话，请参阅[设置了内核模式调试手动](https://msdn.microsoft.com/library/windows/hardware/hh439378)。

以下命令禁用启动调试的 Windows 启动管理器 (Bootmgr.exe)。 Windows 启动管理器选择的操作系统将启动，并加载 Windows 启动加载程序。

```
bcdedit /bootdebug {bootmgr} off 
```

以下命令启用当前操作系统的 Windows 启动加载器的调试启动。 Windows 启动加载器 (Winload.exe) 控件的进度栏，然后加载内核启动驱动程序。

```
bcdedit /bootdebug on 
```

在以下示例中，第一个命令设置全局调试器设置 1394年内核调试连接。 接下来的三个命令启用的 Windows 启动管理器、 启动加载器和操作系统的内核调试然后调试。 这种结合让每个阶段的启动调试。 如果使用这种组合，则目标计算机将进入调试器三次： 在 Windows 启动管理器加载、 引导加载程序加载时，和在操作系统启动时。

```
bcdedit /dbgsettings 1394 CHANNEL:1 
bcdedit /bootdebug {bootmgr} on 
bcdedit /bootdebug on 
bcdedit /debug on 
```

 

 





