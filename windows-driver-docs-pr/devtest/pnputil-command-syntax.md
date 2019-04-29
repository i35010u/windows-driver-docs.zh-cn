---
title: PnPUtil 命令语法
description: 如何运行 PnPUtil，包括语法和参数。
ms.assetid: f14ceb98-8d82-43dd-b06e-2595b59b6999
keywords:
- PnPUtil 命令语法驱动程序开发工具
topic_type:
- apiref
api_name:
- PnPUtil
api_type:
- NA
ms.date: 01/31/2018
ms.localizationpriority: medium
ms.openlocfilehash: b591b0ab1676b56e5b35db7c7cc9c1bb77ed7f89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356303"
---
# <a name="pnputil-command-syntax"></a>PnPUtil 命令语法


若要运行 PnPUtil，打开命令提示符窗口 (**以管理员身份运行**) 并键入使用以下语法和参数的命令。

**请注意**  PnPUtil (PnPUtil.exe) 包含在每个版本的 Windows，从 Windows Vista 开始 (在 %windir%\\system32 目录)。

 

```
pnputil [/add-driver <...> | /delete-driver <...> |
         /export-driver <...> | /enum-drivers | /?]
```

## <a name="commands"></a>命令

  **/add-driver** <filename.inf | *.inf> [/subdirs] [/install] [/reboot]

将驱动程序包添加到驱动程序存储区。  
```
/subdirs - traverse sub directories for driver packages.  
/install - install/update drivers on any matching devices.  
/reboot - reboot system if needed to complete the operation.  
```

  **/delete-driver** *<oem#.inf> [/uninstall] [/force] [/reboot]*

从驱动程序存储区中删除驱动程序包。  

```
/uninstall - uninstall driver package from any devices using it.  
/force - delete driver package even when it is in use by devices.  
/reboot - reboot system if needed to complete the operation.  
```

**/export-driver** <em><oem#.inf | *> <target directory></em>

将驱动程序包从驱动程序存储区导出到目标目录。

**/enum-drivers**

枚举中的所有第三方驱动程序程序包驱动程序存储区。

**/?**

显示命令行语法。

## <a name="legacy-command-mapping"></a>旧命令映射

以下命令仍受支持，但旧。  我们建议你改为使用最新的语法。

```
  -a [-i]  <filename.inf> ==> /add-driver <filename.inf> [/install]

  -d [-f]  <oem#.inf>     ==> /delete-driver <oem#.inf> [/force]

  -e                     ==> /enum-drivers
```
 

###  <a name="comments"></a>备注



有关如何使用 PnPUtil 工具的示例，请参阅[PnPUtil 示例](pnputil-examples.md)。

 

 





