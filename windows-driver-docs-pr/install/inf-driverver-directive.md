---
title: INF DriverVer 指令
description: DriverVer 指令指定此 INF 安装的驱动程序的版本信息。
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
ms.openlocfilehash: ac05af47a91018e15a7fc5a2dd6a9d3c47513dcc
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223169"
---
# <a name="inf-driverver-directive"></a>INF DriverVer 指令


**DriverVer**指令指定此 INF 安装的驱动程序的版本信息。

```inf
[Version] |
[DDInstall]
 
DriverVer=mm/dd/yyyy,w.x.y.z 
```

## <a name="entries"></a>条目


<a href="" id="mm-dd-yyyy"></a>*mm/dd/yyyy*  
此值指定 "[驱动程序包](driver-packages.md)" 的日期，其中包含驱动程序文件和 INF。 此日期必须是驱动程序包中任何文件的最新日期。

必须按月/日/年顺序指定日期。 月份和日期必须包含两位数，年份必须包含四位数字。 连字符（-）可用作日期字段分隔符，而不是斜线（/）。

<a href="" id="w-x-y-z"></a>*w.x.y.z. z*  
此值指定版本号。

每个*w*、 *x*、 *y*和*z*都必须是大于或等于零且小于65535的整数。

对于 Windows XP SP1、Windows Server 2003 和更高版本的 Windows，安装程序也将此值与驱动程序的排名和日期结合*使用*，以选择设备的驱动程序。 有关详细信息，请参阅[Windows 如何选择驱动程序](how-setup-selects-drivers.md)。

以下几点适用于 Windows 2000 和 Windows XP 的此值：

-   此值仅用于显示目的（例如，在设备管理器中），而不用于选择设备驱动程序。
-   应将此值视为输入驱动程序（如鼠标或键盘驱动程序）所需的值。 如果不包含版本值，则可能无法以编程方式更新输入驱动程序。 通常，应在所有[驱动程序包](driver-packages.md)中指定版本信息，因为操作系统使用版本信息作为确定最新驱动程序的条件。

<a name="remarks"></a>备注
-------

从 Windows 2000 开始，INF 文件必须在其[**INF 版本部分**](inf-version-section.md)中有一个**DriverVer**指令，以便为整个 INF 提供版本信息。 单个[**INF *DDInstall*节**](inf-ddinstall-section.md)还可包含**DriverVer**指令，以提供各个驱动程序的版本信息。 *DDInstall*部分中的**DriverVer**指令更为具体，并优先于**版本**部分中的全局**DriverVer**指令。

当操作系统搜索驱动程序时，它会选择一个在具有较早日期的驱动程序上具有最新**DriverVer**日期的驱动程序。 如果 INF 没有**DriverVer**指令或包含无效的日期规范，则操作系统将应用默认日期00/00/0000。 仅适用于 Windows 2000，未签名的驱动程序的日期为00/00/0000。

<a name="examples"></a>示例
--------

```inf
[Version]
...
DriverVer=09/28/1999,5.00.2136.1
```

## <a name="see-also"></a>另请参阅


[***DDInstall***](inf-ddinstall-section.md)

[**版本**](inf-version-section.md)

 

 






