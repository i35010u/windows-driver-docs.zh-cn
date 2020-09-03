---
title: 更改启动参数
description: 更改启动参数
ms.assetid: e835e1e9-ad80-462b-b55f-2fa0e55009a5
keywords:
- 启动项参数 WDK
- 启动参数 WDK
- 启动选项 WDK，启动参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ac8b21863cfbe59ac30cda8fdd5b0ae59377e83
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385063"
---
# <a name="changing-boot-parameters"></a>更改启动参数

若要启用和配置与启动相关的操作系统功能（如调试），必须将启动参数添加到操作系统的启动项。

若要更改运行 Windows 的系统上的启动参数，可以使用 BCDEdit。

## <a name="span-idusing_bcdeditspanspan-idusing_bcdeditspanusing-bcdedit"></a><span id="using_bcdedit"></span><span id="USING_BCDEDIT"></span>使用 BCDEdit

若要将启动配置参数添加到启动条目，请使用 BCDEdit boot entry 选项更改全局设置，如 **/ems**、 **/debug**、 **/dbgsettings**，或使用 [**BCDEdit/set**](./bcdedit--set.md) 选项设置单个参数。 有关 BCDEdit 选项的完整列表，请在命令提示符下键入 **BCDEdit/？** 或 **BCDEdit/？** &lt;命令 &gt; 查找有关特定命令的帮助。

例如，以下命令为指定的启动条目启用 PAE：

```
bcdedit /set {802d5e32-0784-11da-bd33-000476eba25f} pae forceenable
```

若要打开或关闭内核调试器，请将 **/debug** 选项用于以下语法：

```
bcdedit /debug <ID> [on | off]
```

&lt;ID &gt; 是与启动项关联的 GUID。 如果未指定 &lt; ID &gt; ，则该命令将修改当前处于活动状态的操作系统。 以下命令将打开一个启动条目（称为 DebugEntry）的内核调试器：

```
bcdedit /debug {49916baf-0e08-11db-9af4-000bdbd316a0} on
```

若要查看当前的启动条目，请在命令提示符下键入 **bcdedit** 。 DebugEntry 的启动项显示内核调试器已打开。

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