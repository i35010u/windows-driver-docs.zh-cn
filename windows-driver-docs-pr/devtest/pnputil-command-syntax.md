---
title: PnPUtil 命令语法
description: 如何运行 PnPUtil，包括语法和参数。
keywords:
- PnPUtil 命令语法驱动程序开发工具
topic_type:
- apiref
api_name:
- PnPUtil
api_type:
- NA
ms.date: 03/03/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7dd3801f8d3e55f6f62b2dd53f16e8dca897ab8d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841029"
---
# <a name="pnputil-command-syntax"></a>PnPUtil 命令语法


若要运行 PnPUtil，请打开命令提示符窗口 (**以管理员身份运行**) 并使用以下语法和参数键入命令。

**注意**  Windows 的每个版本都包含了 PnPUtil ( # A0) ，从% windir% system32 目录) 中的 Windows Vista (开始 \\ 。

 

```
pnputil [/add-driver <...> | /delete-driver <...> |
         /export-driver <...> | /enum-drivers     |
     /disable-device <...> | /enable-device <...> |
     /restart-device <...> | /remove-device <...> | 
     /scan-devices <...> | /enum-devices <...>    |
     /enum-interfaces <...> | /?]
```

## <a name="commands"></a>命令

 **/add-driver** * <文件名 .inf | *.inf> [/subdirs] [/install] [/reboot]*

**从 Windows 10 版本1607开始提供。**

将 () 中的驱动程序包添加到驱动程序存储区中。  
```
/subdirs - traverse sub directories for driver packages.  
/install - install/update drivers on any matching devices.  
/reboot - reboot system if needed to complete the operation.  
```

**/delete-driver** *<oem # .inf> [/uninstall] [/force] [/reboot]*

**从 Windows 10 版本1607开始提供。**

从驱动程序存储区中删除驱动程序包。  

```
/uninstall - uninstall driver package from any devices using it.  
/force - delete driver package even when it is in use by devices.  
/reboot - reboot system if needed to complete the operation.  
```

**/export-driver** <em><oem # .inf |* > <target directory></em>

**从 Windows 10 版本1607开始提供。**

将驱动程序包从驱动程序存储区 () 导出到目标目录。

**/enum-drivers**

**从 Windows 10 版本1607开始提供。**

枚举驱动程序存储区中的所有第三方驱动程序包。

**/disable-device** <em> \<instance ID\> [/reboot]</em>

**从 Windows 10 版本2004开始提供**

禁用系统上的设备。 

```
/reboot - reboot system if needed to complete the operation.
```

**/enable-device** *\<instance ID\> [/reboot]*

**从 Windows 10 版本2004开始提供**

在系统上启用设备。  

```
/reboot - reboot system if needed to complete the operation.
```

**/restart-device** *\<instance ID\> [/reboot]*

**从 Windows 10 版本2004开始提供**

重新启动系统上的设备设备。 

```
/reboot - reboot system if needed to complete the operation.
```

**/remove-device** *\<instance ID\> [/subtree] [/reboot]*

**从 Windows 10 版本2004开始提供**

尝试从系统中删除设备。 

```
/subtree - remove entire device subree, including any child devices.
/reboot - reboot system if needed to complete the operation.
```

**/scan-devices** *[/instanceid \<instance ID\> ] [/async]*

**从 Windows 10 版本2004开始提供**

扫描系统中是否有任何设备硬件更改。 

```
/instanceid <instance ID> - scan device subtree for changes.
/async - scan for changes asynchronously.
```
**/enum-devices** *[只有当/connected] [/disconnected] [/instanceid \<instance ID\> ] [/class 相同 <名称 |GUID>] [/problem [ \<problem code\> ]] [/ids] [/relations] [/drivers]*

**从 Windows 10 版本1903开始提供**

枚举系统上的所有设备。

```
/connected | /disconnected - filter by connected devices or filter by disconnected devices.
/instanceid <instance ID> - filter by device instance ID.
/class <name | GUID> - filter by device class name or GUID.
/problem [<code>] - filter by devices with problems or filter by specific problem code.
/ids - display hardware IDs and compatible IDs.
/relations - display parent and child device relations.
/drivers - display matching and installed drivers.
```

**/enum-interfaces** *[/enabled |/disabled] [/class 相同 \<GUID\> ]*

**从 Windows 10 版本1903开始提供**

枚举系统上的所有设备接口。

```
/enabled | /disabled - filter by enabled interfaces or filter by disabled interfaces.
/class <GUID> - filter by interface class GUID.
```

**/?**

显示命令行语法。

## <a name="legacy-command-mapping"></a>旧式命令映射

以下命令仍受支持，但是旧的。  建议您改用最新的语法。

```
  -a [-i]  <filename.inf> ==> /add-driver <filename.inf> [/install]

  -d [-f]  <oem#.inf>     ==> /delete-driver <oem#.inf> [/force]

  -e                     ==> /enum-drivers
```
 

###  <a name="comments"></a>注释



有关如何使用 PnPUtil 工具的示例，请参阅 [PnPUtil 示例](pnputil-examples.md)。

 

 





