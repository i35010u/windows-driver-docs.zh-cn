---
title: INF 指令摘要
description: INF 指令摘要
ms.assetid: 6212502c-183c-4abb-9e56-59dba15fc685
keywords:
- INF 文件 WDK 设备安装，指令
- 指令 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e216d6ca081b008b602d13e80b7213eabb58150a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339665"
---
# <a name="summary-of-inf-directives"></a>INF 指令摘要





以下列表总结了许多 （但并非所有） 可以 INF 文件中使用的指令。 INF 指令名称不区分大小写。 例如， **Addreg**， **addReg**，并**AddReg**都作为 INF 文件中的指令规范同样有效。

本部分列出最常使用的指令前，以及它们相互或相关的指令。 最很少使用的指令是向列表的末尾。

<a href="" id="addreg-directive"></a>[**AddReg 指令**](inf-addreg-directive.md)  
此指令引用一个或多个*添加注册表部分*s，该值是 INF 部分用于添加或修改子项和值在注册表中的条目。

在其中的特定 INF 部分**AddReg** (或**DelReg**) 指令所在确定默认值，将收到引用中指定的修改的相对注册表位置*添加注册表部分*(或*删除注册表部分*)。 这些默认注册表位置通常是某个位置下 HKEY_LOCAL_MACHINE 注册表树中的特定于设备的或特定于驱动程序的子项。 有关详细信息，请参阅[注册表树和设备和驱动程序的密钥](registry-trees-and-keys.md)。

其他*添加注册表部分*可以将设置导出到更高级别设备驱动程序，新的供应商提供共同安装程序，系统定义的设备接口 （如内核流式处理接口） 的注册表信息导出的设备驱动程序服务，用于为给定类已安装的组件的接口或 （很少） 新的安装程序类的设备如果 INF **ClassInstall32**部分。

<a href="" id="delreg-directive"></a>[**DelReg 指令**](inf-delreg-directive.md)  
**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此指令引用一个或多个*del 注册表部分*s 用于删除已过时的子项和/或值注册表中的项。 例如，此类部分可能会显示在升级之前安装 INF。

<a href="" id="copyfiles-directive"></a>[**CopyFiles Directive**](inf-copyfiles-directive.md)  
此指令引用一个或多个*文件列表部分*s 指定传输特定于设备的模型/驱动程序映像和任何其他必要的文件的分发介质中的每个此类文件的目标目录。 或者，此指令可以指定单个文件可以从分发介质复制到默认目标目录。

<a href="" id="delfiles-directive"></a>[**DelFiles 指令**](inf-delfiles-directive.md)  
**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

这很少使用指令引用一个或多个*文件列表部分*s 指定要删除从安装的目标文件。

<a href="" id="renfiles-directive"></a>[**RenFiles 指令**](inf-renfiles-directive.md)  
**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

这很少使用指令引用一个或多个*文件列表部分*s 指定 INF 关联源代码文件，以在目标上重命名。

<a href="" id="addservice-directive"></a>[**AddService Directive**](inf-addservice-directive.md)  
此指令引用至少*服务安装部分*，也可能包含额外*事件日志-安装部分*。

对于大多数类型的设备 （即安装驱动程序） 的 INF 文件具有 INF 编写器的定义*服务安装部分*以系统提供的驱动程序或服务，在系统的哪个阶段期间指定任何依赖初始化过程应加载提供的驱动程序，等等。 多个设备驱动程序的 INF 文件还具有 INF 编写器的定义*事件日志-安装部分*引用**AddService**指令以将设备驱动程序事件日志设置。

<a href="" id="delservice-directive"></a>[**DelService Directive**](inf-delservice-directive.md)  
**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此很少使用的指令中删除以前安装的服务。

<a href="" id="addinterface-directive"></a>[**AddInterface Directive**](inf-addinterface-directive.md)  
此指令引用*添加接口部分*在其中一个或多个**AddReg**指令指定引用的支持的设备接口的注册表项设置的部分此设备/驱动程序。 （可选） 此类*添加接口部分*可以引用一个或多个指定删除注册表、 文件传输，文件删除和/或文件重命名操作的其他部分。

<a href="" id="bitreg-directive"></a>[**BitReg 指令**](inf-bitreg-directive.md)  
**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

这很少使用指令引用一个或多个*位注册表部分*指定现有的 s [REG_BINARY](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)的中值的特定位会被修改为其在注册表中键入值项.

<a href="" id="logconfig-directive"></a>[**LogConfig Directive**](inf-logconfig-directive.md)  
**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此指令引用一个或多个*日志配置部分*s （通过即插即用设备枚举器） 检测到的设备 INF 中指定可接受的总线相对，以及特定于设备的硬件配置或手动安装。 例如，INF 文件的非-即插即用 ISA，EISA，而 MCA 设备，则在手动安装，使用此指令。 (另请参阅[ **INF DDInstall.LogConfigOverride 部分**](inf-ddinstall-logconfigoverride-section.md)。)

<a href="" id="updateinis-directive"></a>[**UpdateInis 指令**](inf-updateinis-directive.md)  
**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

这很少使用指令引用一个或多个*更新 ini 部分*s 指定的提供的 INI 文件在安装过程中读取的部件，并可能指定行的行在该 INI 文件中进行修改。

<a href="" id="updateinifields-directive"></a>[**UpdateIniFields 指令**](inf-updateinifields-directive.md)  
**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

这很少使用指令引用一个或多个*更新 inifields 部分*s 指定的 INI 文件的行中的字段在进行修改。

<a href="" id="ini2reg-directive"></a>[**Ini2Reg 指令**](inf-ini2reg-directive.md)  
**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

这很少使用指令引用一个或多个*注册表部分 ini*s 指定行或 INI 文件写入到注册表的部分。

任何前面的列表中的指令可指定在其下的部分是系统确定。 每个指令的基本形式中的每个部分中，例如参考的正式语法所示：

```cpp
[DDInstall] | [DDInstall.HW] | [DDInstall.CoInstallers] | 
[ClassInstall32] | [ClassInstall32.ntx86] | [ClassInstall32.ntia64] | [ClassInstall32.ntamd64]

AddReg=add-registry-section[,add-registry-section] ...
```

本部分的其余部分描述的正式语法和每个系统定义命名的节、 INF 编写器定义的标准部分，和可以 INF 文件中指定的指令的含义。

 

 





