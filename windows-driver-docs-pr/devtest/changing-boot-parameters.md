---
title: 更改启动参数
description: 更改启动参数
ms.assetid: e835e1e9-ad80-462b-b55f-2fa0e55009a5
keywords:
- 启动入口参数 WDK
- 引导参数 WDK
- 启动选项 WDK，引导参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f330203a0065139f51f0a37a564f461845d0344
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375361"
---
# <a name="changing-boot-parameters"></a>更改启动参数

若要启用并配置与启动相关的操作系统功能，如调试，必须将启动参数添加到操作系统的启动项中。

若要更改运行 Windows 的系统上的启动参数，可以使用 BCDEdit。

## <a name="span-idusingbcdeditspanspan-idusingbcdeditspanusing-bcdedit"></a><span id="using_bcdedit"></span><span id="USING_BCDEDIT"></span>使用 BCDEdit

若要添加的启动项启动配置参数，使用 BCDEdit 启动条目选项来更改全局设置，例如 **/ems**， **/debug**， **/dbgsettings**，或设置每个参数使用[ **BCDEdit /set** ](https://msdn.microsoft.com/library/windows/hardware/ff542202)选项。 有关完整列表的 BCDEdit 选项，在命令提示符处，键入**BCDEdit /？** 或**BCDEdit /？** &lt;命令&gt;若要查找有关特定命令的帮助。

例如，以下命令将指定的启动项启用 PAE:

```
bcdedit /set {802d5e32-0784-11da-bd33-000476eba25f} pae forceenable
```

若要启用或禁用内核调试程序，请使用 **/debug**选项使用以下语法：

```
bcdedit /debug <ID> [on | off]
```

&lt;ID&gt;是与启动条目关联的 GUID。 如果未指定&lt;ID&gt;，命令将修改当前处于活动状态的操作系统。 以下命令打开为启动项目，名为 DebugEntry 内核调试程序：

```
bcdedit /debug {49916baf-0e08-11db-9af4-000bdbd316a0} on
```

若要查看当前的启动项，请键入**bcdedit**在命令提示符处。 DebugEntry 的启动项目显示了内核调试程序已打开。

```
## Windows Boot Loader
-------------------
identifier              {49916baf-0e08-11db-9af4-000bdbd316a0}
device                  partition=C:
path                    \Windows\system32\winload.exe
description             DebugEntry
locale                  en-US
inherit                 {bootloadersettings}
osdevice                partition=C:
systemroot              \Windows
resumeobject            {3e3a9f69-024a-11db-b5fc-a50a1ad8a70e}
nx                      OptIn
pae                     ForceEnable
debug                   Yes
```
