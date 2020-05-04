---
title: INF Manufacturer 节
description: "\"制造商\" 部分标识了可以使用 INF 文件安装的一个或多个设备的制造商。"
ms.assetid: c5128d0a-d581-4461-8eb9-5680b6b6ef38
keywords:
- INF 制造商部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF Manufacturer Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48800a2794abf8caeaf5e90c94371b9e5c65aa26
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223141"
---
# <a name="inf-manufacturer-section"></a>INF Manufacturer 节


"**制造商**" 部分标识了可以使用 INF 文件安装的一个或多个设备的制造商。

```inf
[Manufacturer]

manufacturer-identifier
[manufacturer-identifier] 
[manufacturer-identifier] 
...
```

## <a name="entries"></a>条目


<a href="" id="manufacturer-identifier"></a>*制造商-标识符*  
唯一标识制造商和 INF 部分，其中包含用于标识制造商设备型号的信息。 每个*制造商标识符*条目都必须位于单独的行中，并使用以下格式：

```inf
manufacturer-name |
%strkey%=models-section-name |
%strkey%=models-section-name [,TargetOSVersion] [,TargetOSVersion] ...  (Windows XP and later versions of Windows)
```

这些项的定义如下：

<a href="" id="manufacturer-name"></a>*制造商-名称*  
标识设备制造商。 INF 还必须包含具有相同名称的对应[**INF*型号*部分**](inf-models-section.md)。 制造商名称的最大长度，以字符为 LINE_LEN。 （以这种方式指定的项不能进行本地化。）

<a href="" id="strkey-"></a>*strkey*   
指定一个令牌，该令牌在 INF 文件中唯一，表示制造商的名称。 每个此类%*strkey*% 令牌必须在 inf 文件的[**inf 字符串部分**](inf-strings-section.md)中定义。

<a href="" id="models-section-name"></a>*模型-节名称*  
为 INF 文件中的每个制造商[**Inf*型号*部分**](inf-models-section.md)指定 inf 写入方定义的名称。 此值在 INF 文件中必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅[INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

<a href="" id="targetosversion"></a>*TargetOSVersion*  
指定一个或多个可以使用各种 INF***模型***部分的目标操作系统版本。 Windows 选择与执行它的操作系统版本最匹配的 "INF***模型***" 部分。

有关*TargetOSVersion*修饰的说明，请参阅下面的 "**备注**" 部分以及示例3中的相关信息。

**重要说明**：从 Windows SERVER 2003 SP1 开始，inf 文件必须修饰 " **inf 制造商" 部分**中的 "模型-部分名称" 条目，以及关联的 "inf***模型***" 部分名称，其中 ntia64 或. ntamd64 平台扩展用于指定非 x86 目标操作系统版本。 对于基于 x86 的目标操作系统版本或非 PnP 驱动程序 INF 文件（如基于 x64 的体系结构的文件系统驱动程序 INF 文件），这些平台扩展在 INF 文件中不是必需的。

 

<a name="remarks"></a>备注
-------

安装一个或多个设备的任何 INF 文件都必须具有**制造商**部分。 IHV/OEM 提供的 INF 文件通常只在此部分指定一个条目。 如果指定了多个条目，每个条目必须位于 INF 的单独行中。

使用%*strkey*%=*：节名称*条目可简化国际市场的 INF 文件本地化，如[创建国际 inf 文件](creating-international-inf-files.md)和[**INF 字符串**](inf-strings-section.md)的参考页中所述。

如果 INF 文件指定了*制造商名称*格式的一个或多个条目，则每个此类条目都将隐式指定 INF 中其他位置的相应***型号***部分的名称。

你可以将每个系统提供的 INF 文件的**制造商**部分视为目录，因为此部分为[设备安装程序类](device-setup-classes.md)设置了每个制造商的设备型号。 INF 文件的 "**制造商**" 部分中的每个条目均为制造商名称和每个特定于 inf 的每个制造商的***型号***部分名称指定易于本地化的%*strkey*% 令牌。

"**制造商**" 部分中的 "*型号" 部分名称*项可以进行修饰以指定目标操作系统版本。 对于不同版本的操作系统，可以指定不同的[**INF*模式*部分**](inf-models-section.md)。 指定的版本指示用于使用 INF***模型***部分的操作系统版本。 如果未指定任何版本，Windows 将对所有操作系统的所有版本使用指定的***模型***部分。

对于 Windows XP 到 Windows 10 版本1511， *TargetOSVersion*修饰的格式如下所示：

```inf
nt[Architecture][.[OSMajorVersion][.[OSMinorVersion][.[ProductType][.SuiteMask]]]]
```
从 Windows 10 开始，版本1607（版本14310及更高版本）， *TargetOSVersion*修饰的格式如下所示：
```inf
nt[Architecture][.[OSMajorVersion][.[OSMinorVersion][.[ProductType][.[SuiteMask][.[BuildNumber]]]]]
```

每个字段的定义如下：

<a href="" id="nt"></a>**nt**  
指定目标操作系统基于 NT。 Windows 2000 和更高版本的 Windows 都是基于 NT 的。

<a href="" id="architecture"></a>*种*  
标识硬件平台。 如果已指定，则必须是**x86**、 **ia64**、 **amd64**、 **arm**或**arm64**。

在 Windows Server 2003 SP1 之前，如果未指定*体系结构*，则可以将关联的 "INF***模型***" 部分用于任何硬件平台。

从 Windows Server 2003 SP1 开始，必须在[**INF*模型*部分**](inf-models-section.md)名称中为非 x86 目标操作系统版本指定体系结构。 对于基于 x86 的目标操作系统版本，在 INF***模型***部分名称中，体系结构是可选的。

<a href="" id="osmajorversion"></a>*OSMajorVersion*  
一个数字，表示操作系统的主版本号。 下表定义 Windows 操作系统的主版本。

| Windows 版本        | 主版本 |
|------------------------|---------------|
| Windows 10             | 10            |
| Windows Server 2012 R2 | 6             |
| Windows 8.1            | 6             |
| Windows Server 2012    | 6             |
| Windows 8              | 6             |
| Windows Server 2008 R2 | 6             |
| Windows 7              | 6             |
| Windows Server 2008    | 6             |
| Windows Vista          | 6             |
| Windows Server 2003 R2 | 5             |
| Windows Server 2003    | 5             |
| Windows XP             | 5             |
| Windows 2000           | 5             |

 

<a href="" id="osminorversion"></a>*OSMinorVersion*  
一个数字，表示操作系统的次版本号。 下表定义了 Windows 操作系统的次版本。

| Windows 版本        | 次版本 |
|------------------------|---------------|
| Windows 10             | 0             |
| Windows Server 2012 R2 | 3             |
| Windows 8.1            | 3             |
| Windows Server 2012    | 2             |
| Windows 8              | 2             |
| Windows Server 2008 R2 | 1             |
| Windows 7              | 1             |
| Windows Server 2008    | 0             |
| Windows Vista          | 0             |
| Windows Server 2003 R2 | 2             |
| Windows Server 2003    | 2             |
| Windows XP             | 1             |
| Windows 2000           | 0             |

 

<a href="" id="producttype"></a>*ProductType*  
一个数字，表示*winnt.sif*中定义的一个 VER_NT_xxxx 标志，如下所示：

**0x0000001** （VER_NT_WORKSTATION）

**0x0000002** （VER_NT_DOMAIN_CONTROLLER）

**0x0000003** （VER_NT_SERVER）

如果指定了产品类型，则仅当操作系统与指定的产品类型匹配时，才使用 INF 文件。 如果 INF 支持多个产品类型用于单个操作系统版本，则需要多个*TargetOSVersion*条目。

<a href="" id="suitemask"></a>*SuiteMask*  
一个数字，表示*winnt.sif*中定义的一个或多个 VER_SUITE_xxxx 标志的组合。 这些标志包括：

**0x00000001** （VER_SUITE_SMALLBUSINESS）

**0x00000002** （VER_SUITE_ENTERPRISE）

**0x00000004** （VER_SUITE_BACKOFFICE）

**0x00000008** （VER_SUITE_COMMUNICATIONS）

**0x00000010** （VER_SUITE_TERMINAL）

**0x00000020** （VER_SUITE_SMALLBUSINESS_RESTRICTED）

**0x00000040** （VER_SUITE_EMBEDDEDNT）

**0x00000080** （VER_SUITE_DATACENTER）

**0x00000100** （VER_SUITE_SINGLEUSERTS）

**0x00000200** （VER_SUITE_PERSONAL）

**0x00000400** （VER_SUITE_SERVERAPPLIANCE）

如果指定了一个或多个套件掩码值，则仅当操作系统与所有指定的产品套件匹配时，才使用 INF。 如果 INF 为一个操作系统版本支持多个产品套件组合，则需要多个*TargetOSVersion*条目。

<a href="" id="buildnumber"></a>*BuildNumber*  
一个数字，表示该部分适用于的 Windows 10 版本的最低操作系统内部版本号，从版本14310或更高版本开始。

内部版本号假定为相对于某些特定操作系统主要/次要版本，并且可能会在将来的某个操作系统主要/次要版本中重置。仅当*TargetOSVersion*的操作系统主要/次要版本与当前 os （或 AltPlatformInfo）版本完全匹配时，才计算*TargetOSVersion*修饰指定的任何生成号。如果当前操作系统版本高于*TargetOSVersion*修饰（OSMajorVersion，OSMinorVersion）所指定的操作系统版本，则无论指定的生成号如何，都将该节视为适用。 同样，如果当前操作系统版本低于*TargetOSVersion*修饰指定的操作系统版本，则该部分不适用。

如果提供了生成号，则*TargetOSVersion*修饰的 os 版本和 BuildNumber 必须都大于 Windows 10 build 14310 的操作系统版本和生成号，这一修饰首次引入。  不带这些更改的更早版本的操作系统（例如，Windows 10 版本10240）将不会分析未知的修饰，因此，对这些较早版本的尝试将实际上会阻止操作系统考虑修饰有效。

有关*TargetOSVersion*修饰的详细信息，请参阅将[平台扩展与操作系统版本结合起来](combining-platform-extensions-with-operating-system-versions.md)。

**重要说明：**  我们强烈建议你始终在 "**制造商**和[***型号***](inf-models-section.md)" 部分中为 windows XP 或更高版本的 windows 版本的目标操作系统的平台扩展修饰*模型-节名称*条目。 对于基于 x86 的硬件平台，应避免使用**nt**平台扩展，并改为使用**ntx86** 。

 

如果 INF 包含带有修饰的 "**制造商**" 部分条目，则它还必须包含名称与操作系统修饰相匹配的 " [**INF*模型*" 部分**](inf-models-section.md)。 例如，如果 INF 包含以下**制造商**部分：

**% FooCorp% = FooMfg，NTx86 .。。0x80、NTamd64**

然后，INF 还必须包含具有以下名称的[**Inf*型号*部分**](inf-models-section.md)：

-   **\[FooMfg.NTx86....0x80\]**

    此名称适用于基于 x86 的硬件平台上的 Windows XP 和更高版本的 Windows 的数据中心套件。

-   **\[FooMfg.NTamd64\]**

    此名称适用于基于 x64 的硬件平台上的 Windows XP 及 windows 的更高版本的所有产品类型和套件。

在安装过程中，Windows 会按以下方式选择[**INF*型号*部分**](inf-models-section.md)：

1.  如果 windows 运行在包含数据中心产品套件的基于 x86 的操作系统（windows XP 或更高版本）版本中，则 windows 将选择 " ** \[FooMfg. NTx86 ..."。0x80\] ** ***模型***部分。
2.  如果 windows 在任何产品套件的基于 x64 版本的操作系统（windows XP 或更高版本）上运行，则 windows 将选择** \[FooMfg NTamd64\] ** ***模型***部分。

如果 INF 适用于 Windows XP 之前的操作系统版本，它还必须包含名为** \[FooMfg\]** 的未修饰***模型***部分。

如果 INF 支持多个制造商，则必须遵循每个制造商的这些规则。

下面是*TargetOSVersion*修饰的其他示例：

-   **% FooCorp% = FooMfg，NTx86**

    在此示例中，结果 INF***型号***部分名称为** \[FooMfg. NTx86\]**，适用于任何 x86 版本的操作系统（Windows XP 或更高版本）。

-   **% FooCorp% = FooMfg，NT. 7。8**

    在此示例中，对于版本7.8 及更高版本的操作系统，结果 INF***型号***部分名称为** \[FooMfg\]**。 对于更早版本的操作系统（如 Windows XP）， ** \[将使用 FooMfg\] ** 。

安装程序选择要使用的 INF***模型***部分基于以下规则：

-   如果 INF 包含几个主要或次要操作系统版本号的[**Inf*型号*部分**](inf-models-section.md)，则 Windows 将使用版本号最高的部分，该部分的版本号不高于安装的操作系统版本。
-   如果与操作系统版本匹配的 INF***型号***部分还包含产品类型和/或产品套件装饰，则 Windows 将选择与正在运行的操作系统最匹配的部分。

例如，假设 Windows 在 Windows XP （版本5.1）上执行，没有数据中心产品套件，并在**制造商**部分找到以下条目：

**% FooCorp% = FooMfg，NT，nt. 5，NT. 5.5，NT ...。0x80**

在这种情况下，Windows 将查找名为** \[FooMfg\]** 的[**INF*型号*部分**](inf-models-section.md)。 如果 windows XP 的数据中心版本正在运行，windows 还会使用** \[FooMfg\] **部分，因为特定版本号优先于产品类型和套件掩码。

如果希望 INF 显式排除特定的操作系统版本、产品类型或套件，请创建空的[**INF*模型*部分**](inf-models-section.md)。 例如，名为** \[FooMfg. ntx 86.6.0\] **的空节禁止在基于 x86 的操作系统版本6.0 和更高版本上安装。

<a name="examples"></a>示例
--------

此示例显示了一个适用于单个 IHV 的 INF 的典型**制造商**部分。

```inf
[Manufacturer]
%Mfg%=Contoso        ; Models section == Contoso

[Contoso]

; ...
[Strings]
Mfg = "Contoso, Ltd."
```

下一个示例显示了特定于设备类的安装程序的 INF 的 "**制造商**" 部分的一部分：

```inf
[Manufacturer]
%CONTOSO%=Contoso_Section
; several entries omitted here for brevity
%FABRIKAM%=Fabrikam_Section
%ADATUM%=Adatum_Section
```

以下示例显示了特定于 x86 平台、Windows XP 和更高版本的**制造商**部分：

```inf
[Manufacturer]
%foo%=foosec,NTx86.5.1

[foosec.NTx86.5.1]
```

以下示例显示了特定于 x64 平台、Windows 10 内部版本14393及更高版本的**制造商**部分：

```inf
[Manufacturer]
%foo%=foosec,NTamd64.10.0...14393

[foosec.NTamd64.10.0...14393]
```

以下两个示例显示了包含各种特定于 OS 的 INF*模型*部分的框架 INF 文件：

示例 1：

```inf
[Manufacturer]
%MyName% = MyName,NTx86.5.1
.
[MyName]
%MyDev% = InstallA,hwid
.
[MyName.NTx86.5.1]
%MyDev% = InstallB,hwid
.
[InstallA]   ; Windows 2000 
.
.
[InstallB]   ; Windows XP and later, x86 only
.
```

示例 2：

```inf
[Manufacturer]
%MyName% = MyName,NTx86.6.0,NTx86.5.1,
.
[MyName.NTx86.6.0] ; Empty section, so this INF does not support
.                  ; NT 6.0 and later.
.
[MyName.NTx86.5.1] ; Used for NT 5.1 and later
.                  ; (but not NT 6.0 and later due to the NTx86.6.0 entry)
%MyDev% = InstallB,hwid
.
[MyName]           ; Empty section, so this INF does not support
.                  ; Win2000
.
```

示例 3：

```inf
[Manufacturer]
%MyMfg% = MyMfg, NTamd64.6.1, NTamd64.10.0, NTamd64.10.0...14310
.
[MyMfg.NTamd64.6.1]          ; Used for Windows 7 and later
.                            ; (but not for Windows 10 and later due to the NT.10.0 entry)
.
[MyMfg.NTamd64.10.0]         ; Used for Windows 10
.                            ; (but not for Windows 10 build 14393 and later due to the NT.10.0...14393 entry)
.
[MyMfg.NTamd64.10.0...14393] ; Used for Windows 10 build 14393 and later
.
.
```
**注意**：指定多个 TargetOSVersions 时，请将它们一起放入一个条目中，如本示例中所示。  不要将每个目标表示为单独的条目。 

## <a name="see-also"></a>另请参阅


[将平台扩展与操作系统版本相结合](combining-platform-extensions-with-operating-system-versions.md)

[***模型***](inf-models-section.md)

[**字符串**](inf-strings-section.md)

 

 






