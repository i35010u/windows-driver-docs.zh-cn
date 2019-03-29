---
title: INF DriverVer 指令
description: DriverVer 指令指定安装此 INF 的驱动程序的版本信息。
ms.assetid: b8c17839-a027-4fb6-b017-8e9a3fd0d694
keywords:
- INF DriverVer 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DriverVer Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a81f9fea8cb3b1afe8a57b2d2235b10175f7b180
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568664"
---
# <a name="inf-driverver-directive"></a>INF DriverVer 指令


一个**DriverVer**指令指定安装此 INF 的驱动程序的版本信息。

```ini
[Version] |
[DDInstall]
 
DriverVer=mm/dd/yyyy,w.x.y.z 
```

## <a name="entries"></a>条目


<a href="" id="mm-dd-yyyy"></a>*mm/dd/yyyy*  
此值指定的日期"[驱动程序包](driver-packages.md)"，其中包括驱动程序文件和 INF。 此日期必须是最新的驱动程序包中的任何文件的日期。

必须按月/日/年顺序指定的日期。 月和日必须包含两位数字，并且一年必须包含四位数字。 连字符 （-） 可用作日期字段分隔符，而不是反斜杠 （/）。

<a href="" id="w-x-y-z"></a>*w.x.y.z*  
此值指定的版本号。

每个*w*， *x*， *y*，以及*z*必须是大于或等于零且小于 65535 的整数。

对于 Windows XP SP1、 Windows Server 2003 和更高版本的 Windows，此值也是*使用*由安装程序，与驱动程序级别和日期，以选择设备驱动程序结合使用。 有关详细信息，请参阅[Windows 中如何选择驱动程序](how-setup-selects-drivers.md)。

以下几点适用于 Windows 2000 和 Windows XP 的此值：

-   此值是用于显示目的仅 （例如，在设备管理器） 并不用于选择设备驱动程序。
-   应考虑为输入驱动程序 （如鼠标或键盘驱动程序） 需要提供此值。 如果未包括的版本值，可能会不会以编程方式更新输入驱动程序。 通常情况下，应在所有指定的版本信息[驱动程序包](driver-packages.md)因为操作系统使用版本信息的条件来确定最新驱动程序。

<a name="remarks"></a>备注
-------

从 Windows 2000 开始，INF 文件必须具有**DriverVer**指令及其[ **INF 版本部分**](inf-version-section.md)提供整个 INF 的版本信息。 各个[ **INF *DDInstall*各节**](inf-ddinstall-section.md)还可以包含**DriverVer**指令来提供个人的版本信息驱动程序。 **DriverVer**中的指令*DDInstall*各节更特定，并优先于全局**DriverVer**指令**版本**部分。

当操作系统搜索驱动程序时，它将选择具有较新的驱动程序**DriverVer**转移的驱动程序，具有以前的某个日期的日期。 如果不具有 INF **DriverVer**指令或包含无效的日期的规范中，操作系统将应用默认的日期的 00 00/0000。 对于 Windows 2000，未签名驱动程序还分配 00 00/0000 的日期。

<a name="examples"></a>示例
--------

```ini
[Version]
...
DriverVer=09/28/1999,5.00.2136.1
```

## <a name="see-also"></a>请参阅


[***DDInstall***](inf-ddinstall-section.md)

[**版本**](inf-version-section.md)

 

 






