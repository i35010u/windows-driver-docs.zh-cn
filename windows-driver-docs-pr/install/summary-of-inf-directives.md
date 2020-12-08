---
title: INF 指令摘要
description: INF 指令摘要
keywords:
- INF 文件 WDK 设备安装，指令
- 指令 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae3a7b68cc51942e3fe8401a7773d0d4ae228d85
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829843"
---
# <a name="summary-of-inf-directives"></a>INF 指令摘要





以下列表汇总了许多 (，但并不是所有可在 INF 文件中使用的指令) 。 INF 指令名称不区分大小写。 例如， **Addreg**、 **Addreg** 和 **Addreg** 同样适用于 INF 文件中的指令规范。

本部分首先列出最常用的指令，以及它们的倒数或相关指令。 最少使用的指令位于列表的末尾。

<a href="" id="addreg-directive"></a>[**AddReg 指令**](inf-addreg-directive.md)  
此指令引用一个或多个 *add-registry 节*，这是用于在注册表中添加或修改子项和值项的 INF 部分。

**AddReg** (或 **DelReg**) 指令所在的特定 INF 部分确定了默认的相对注册表位置，该位置将接收在引用的 "*添加注册表- (部分* *") 中* 指定的修改。 这些默认注册表位置通常是特定于设备或特定于驱动程序的 HKEY_LOCAL_MACHINE 子项。 有关详细信息，请参阅 [设备和驱动程序的注册表树和密钥](registry-trees-and-keys.md)。

附加的 *添加注册表部分* 可以为系统定义的设备接口（例如，) 导出到较高级别驱动程序的系统定义的设备接口）设置注册表信息， (如导出到较高级别驱动程序的内核流式处理接口、对于驱动程序服务的已安装组件导出的新设备接口、驱动程序服务或)  (如果 INF 具有 **ClassInstall32** 部分，则为设备的新

<a href="" id="delreg-directive"></a>[**DelReg 指令**](inf-delreg-directive.md)  
**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此指令引用一个或多个用于从注册表中删除过时的子项和/或值项的 *del-节*。 例如，此类部分可能出现在升级先前安装的 INF 中。

<a href="" id="copyfiles-directive"></a>[**CopyFiles 指令**](inf-copyfiles-directive.md)  
此指令引用一个或多个 *文件列表部分*，指定将模型/设备特定的驱动程序映像和任何其他必需的文件从分发媒体传输到每个此类文件的目标目录。 此外，此指令可以指定要从分发媒体复制到默认目标目录的单个文件。

<a href="" id="delfiles-directive"></a>[**DelFiles 指令**](inf-delfiles-directive.md)  
**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此很少使用的指令引用一个或多个 *文件列表部分*，指定要从安装目标中删除的文件。

<a href="" id="renfiles-directive"></a>[**RenFiles 指令**](inf-renfiles-directive.md)  
**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此很少使用的指令引用一个或多个 *文件列表部分*，指定要在目标上重命名的与 INF 关联的源文件。

<a href="" id="addservice-directive"></a>[**AddService 指令**](inf-addservice-directive.md)  
此指令至少引用一个 *服务安装部分*，可能会有一个附加的 *事件日志-安装部分*。

大多数类型的设备（ (安装驱动) 程序的设备的 INF 文件）都具有一个由 INF 编写器定义的 *服务安装部分* ，用于指定系统提供的驱动程序或服务上的任何依赖项，在这种情况下系统初始化过程中应加载提供的驱动程序，等等。 许多用于设备驱动程序的 INF 文件还具有一个由 INF 编写器定义的 *事件日志-安装部分* ，该 **AddService** 指令通过设备驱动程序设置事件日志记录。

<a href="" id="delservice-directive"></a>[**DelService 指令**](inf-delservice-directive.md)  
**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此很少使用的指令删除以前安装的服务。

<a href="" id="addinterface-directive"></a>[**AddInterface 指令**](inf-addinterface-directive.md)  
此指令将引用一个 *添加接口部分* ，其中指定了一个或多个 **AddReg** 指令，其中包含为此设备/驱动程序所支持的设备接口设置注册表项的部分。 此外，此类 *添加接口部分* 可以引用指定删除-注册表、文件传输、文件删除和/或文件重命名操作的一个或多个其他部分。

<a href="" id="bitreg-directive"></a>[**BitReg 指令**](inf-bitreg-directive.md)  
**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此很少使用的指令引用一个或多个在注册表中指定现有 [REG_BINARY](/windows/desktop/SysInfo/registry-value-types)类型值项的一个或多个 *位注册表* 项。

<a href="" id="logconfig-directive"></a>[**LogConfig 指令**](inf-logconfig-directive.md)  
**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此指令将引用一个或多个 *日志配置节*，该配置节指定由 PnP 设备枚举器 (检测) 或手动安装的设备在 INF 中可接受的与总线相关的特定于设备的硬件配置。 例如，对于手动安装的非 PnP ISA、EISA 和 MCA 设备，使用此指令。  (另请参阅 [**INF DDInstall. LogConfigOverride 部分**](inf-ddinstall-logconfigoverride-section.md)。 ) 

<a href="" id="updateinis-directive"></a>[**UpdateInis 指令**](inf-updateinis-directive.md)  
**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此很少使用的指令引用一个或多个 *更新-ini 部分*，指定在安装过程中所提供的 ini 文件的各个部分，并且可能在该 ini 文件中指定逐行修改。

<a href="" id="updateinifields-directive"></a>[**UpdateIniFields 指令**](inf-updateinifields-directive.md)  
**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此很少使用的指令引用一个或多个 *inifields* 指定对 INI 文件行中的字段进行的修改。

<a href="" id="ini2reg-directive"></a>[**Ini2Reg 指令**](inf-ini2reg-directive.md)  
**注意**  如果要构建通用或移动驱动程序包，则此指令无效。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

此很少使用的指令引用一个或多个 *ini 到注册表节*，指定要写入注册表的 ini 文件的行或部分。

可在其中指定上一列表中的任何指令的部分，由系统确定。 每个指令的基本形式显示在每个部分的引用的正式语法中，例如：

```cpp
[DDInstall] | [DDInstall.HW] | [DDInstall.CoInstallers] | 
[ClassInstall32] | [ClassInstall32.ntx86] | [ClassInstall32.ntia64] | [ClassInstall32.ntamd64]

AddReg=add-registry-section[,add-registry-section] ...
```

本部分的其余部分介绍了适用于每个系统定义的命名节、标准 INF 写入器定义的部分以及可在 INF 文件中指定的指令的正式语法和含义。

 

