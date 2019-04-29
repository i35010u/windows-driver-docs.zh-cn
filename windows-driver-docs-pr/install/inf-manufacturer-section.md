---
title: INF Manufacturer 节
description: 制造商部分标识可以通过使用 INF 文件安装的一个或多个设备的制造商。
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
ms.openlocfilehash: 8ee959c01e9d4070aee4042ccc7951e53a19292f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378463"
---
# <a name="inf-manufacturer-section"></a>INF Manufacturer 节


**制造商**部分标识可以通过使用 INF 文件安装的一个或多个设备的制造商。

```ini
[Manufacturer]

manufacturer-identifier
[manufacturer-identifier] 
[manufacturer-identifier] 
...
```

## <a name="entries"></a>条目


<a href="" id="manufacturer-identifier"></a>*manufacturer-identifier*  
唯一标识制造商和一个 INF 部分，其中包含标识制造商的设备型号的信息。 每个*制造商标识符*条目必须位于单独的行上，使用以下格式：

```ini
manufacturer-name |
%strkey%=models-section-name |
%strkey%=models-section-name [,TargetOSVersion] [,TargetOSVersion] ...  (Windows XP and later versions of Windows)
```

这些项定义，如下所示：

<a href="" id="manufacturer-name"></a>*manufacturer-name*  
标识设备的制造商。 INF 还必须包含相应[ **INF*模型*部分**](inf-models-section.md)具有相同名称。 制造商，以字符为单位的最大长度是名称的 LINE_LEN。 （在这种方式中指定的条目不能进行本地化。）

<a href="" id="strkey-"></a>*strkey*   
指定标记，表示制造商的名称的 INF 文件中唯一。 每个此类 %*strkey*必须在定义 %令牌[ **INF 字符串部分**](inf-strings-section.md)的 INF 文件。

<a href="" id="models-section-name"></a>*models-section-name*  
指定每个制造商生产的 INF 编写器定义名称[ **INF*模型*部分**](inf-models-section.md) INF 文件中。 该值的 INF 文件中必须是唯一的因此必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

<a href="" id="targetosversion"></a>*TargetOSVersion*  
指定一个或多个目标操作系统版本与哪些各种 INF***模型***可以使用部分。 Windows 选择 INF***模型***与执行它的操作系统版本最匹配的部分。

**注意**：在C++上面的代码，在一个条目中列出了多个 TargetOSVersions。  这是添加多个 TargetOSVersions 的正确方法。  无法代表每个目标作为一个单独的条目。  请参阅下面的示例 3 中的相关的信息。


有关的说明*TargetOSVersion*修饰，请参阅以下**备注**部分。

**重要**:  从 Windows Server 2003 SP1 开始，INF 文件必须修饰模型部分名称中的条目**INF 制造商部分**，以及关联 INF***模型***部分名称，与.ntia64 或。ntamd64 平台扩展，以指定非 x86 目标操作系统的系统版本。 基于 x86 的目标操作系统版本的 INF 文件或非 PnP 驱动程序 INF 文件，例如适用于基于 x64 的体系结构的文件系统驱动程序 INF 文件中不需要这些平台扩展。

 

<a name="remarks"></a>备注
-------

安装一个或多个设备的任何 INF 文件必须具有**制造商**部分。 IHV/OEM 提供 INF 文件通常在本部分中指定只有一个条目。 如果指定了多个条目，每个条目必须 INF 的单独的行上。

使用 %*strkey*%=*模型节名称*条目简化了对国际市场的 INF 文件的本地化，如中所述[创建国际 INF文件](creating-international-inf-files.md)和个的参考页[ **INF 字符串部分**](inf-strings-section.md)。

如果指定了一个 INF 文件中的一个或多个条目*制造商名称*格式，每个此类条目隐式指定名称的相应***模型***INF 中的其他位置的部分。

您可以将每个系统提供 INF 文件的**制造商**部分为表的内容，因为本部分中设置的每个制造商的设备型号为安装[设备安装程序类](device-setup-classes.md). INF 文件中的每个条目**制造商**部分指定了这两个更易于本地化 %*strkey*的制造商和唯一-到--INF 每个的制造商名称的 %令牌***模型***节名称。

*模型节名称*中的条目**制造商**部分可以修饰来指定目标操作系统版本。 不同[ **INF*模型*各节**](inf-models-section.md)可以指定针对不同版本的操作系统。 指定的版本指示操作系统版本与 INF***模型***部分使用。 如果未不指定任何版本，Windows 将使用指定***模型***部分中的所有操作系统的所有版本。

对于 Windows XP 到 Windows 10，版本 1511年的格式*TargetOSVersion*修饰是按如下所示：

```ini
nt[Architecture][.[OSMajorVersion][.[OSMinorVersion][.[ProductType][.SuiteMask]]]]
```
从 Windows 10，版本 1607 （内部 14310 及更高版本） 格式的开始*TargetOSVersion*修饰是按如下所示：
```ini
nt[Architecture][.[OSMajorVersion][.[OSMinorVersion][.[ProductType][.[SuiteMask][.[BuildNumber]]]]]
```

每个字段定义，如下所示：

<a href="" id="nt"></a>**nt**  
指定目标操作系统是基于 NT 的。 Windows 2000 和更高版本的 Windows 是所有基于 NT 的。

<a href="" id="architecture"></a>*体系结构*  
标识的硬件平台。 如果指定，这必须是**x86**， **ia64**， **amd64**， **arm**，或**arm64**。

Windows Server 2003 在 SP1 之前，如果*体系结构*未指定，则关联的 INF***模型***部分可与任何硬件平台。

从 Windows Server 2003 SP1 开始，体系结构中，必须指定[ **INF*模型*各节**](inf-models-section.md)名称非 x86 目标操作系统版本。 体系结构中是可选的 INF***模型***部分基于 x86 的目标操作系统版本的名称。

<a href="" id="osmajorversion"></a>*OSMajorVersion*  
一个数字表示操作系统的主版本号。 下表定义 Windows 操作系统的主的版本。

| Windows 版本        | 主要版本 |
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
一个数字表示操作系统的次版本号。 下表定义 Windows 操作系统的次的版本。

| Windows 版本        | 次要版本 |
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
在中定义的一个数字，表示 VER_NT_xxxx 标志之一*Winnt.h*，如下所示：

**0x0000001** (VER_NT_WORKSTATION)

**0x0000002** (VER_NT_DOMAIN_CONTROLLER)

**0x0000003** (VER_NT_SERVER)

如果指定的产品类型，则操作系统与指定的产品类型匹配时才使用 INF 文件。 如果 INF 有关单个操作系统版本，支持多个产品类型多个*TargetOSVersion*为必需项。

<a href="" id="suitemask"></a>*SuiteMask*  
表示一个或多个中定义的 VER_SUITE_xxxx 标志的组合的数字*Winnt.h*。 这些标记包括：

**0x00000001** (VER_SUITE_SMALLBUSINESS)

**0x00000002** (VER_SUITE_ENTERPRISE)

**0x00000004** (VER_SUITE_BACKOFFICE)

**0x00000008** (VER_SUITE_COMMUNICATIONS)

**0x00000010** (VER_SUITE_TERMINAL)

**0x00000020** (VER_SUITE_SMALLBUSINESS_RESTRICTED)

**0x00000040** (VER_SUITE_EMBEDDEDNT)

**0x00000080** (VER_SUITE_DATACENTER)

**0x00000100** (VER_SUITE_SINGLEUSERTS)

**0x00000200** (VER_SUITE_PERSONAL)

**0x00000400** (VER_SUITE_SERVERAPPLIANCE)

如果指定了一个或多个套件掩码值，仅当操作系统匹配所有指定的产品套件，则使用 INF。 如果 INF 有关单个操作系统版本，支持多个产品套件组合多个*TargetOSVersion*为必需项。

<a href="" id="buildnumber"></a>*BuildNumber*  
一个数字，表示最小的 OS 生成到其中的部分是适用，从生成 14310 或更高版本的 Windows 10 版本。

生成号被假定为相对于某些特定的操作系统主要/次要版本，并可能会重置为某一将来 OS 主要/次要版本。  任何生成指定的数字*TargetOSVersion*仅当操作系统主要/次要版本的计算修饰*TargetOSVersion*完全匹配的当前 OS （或 AltPlatformInfo） 版本。  如果当前 OS 版本高于指定的 OS 版本*TargetOSVersion*修饰 （OSMajorVersion，OSMinorVersion） 部分被视为适用而不考虑指定的生成号。 同样，如果当前 OS 版本低于指定的 OS 版本*TargetOSVersion*修饰，该节不适用。

如果提供的内部版本号，则操作系统版本和的 BuildNumber *TargetOSVersion*修饰必须同时大于 OS 版本和 Windows 10 生成 14310 首次引入此修饰的生成号。  早期版本的操作系统 (例如，Windows 10 生成 10240) 这些更改不会将分析未知的修饰，因此尝试这些前面生成的目标实际上将阻止该 OS 考虑修饰根本有效。

有关详细信息*TargetOSVersion*修饰，请参阅[结合使用的操作系统版本的平台扩展](combining-platform-extensions-with-operating-system-versions.md)。

**重要**  我们强烈建议您始终修饰*模型节名称*中的条目**制造商**并[***模型***](inf-models-section.md)与目标操作系统的平台扩展的 Windows XP 或更高版本的 Windows 的部分。 对于基于 x86 的硬件平台，应避免使用 **.nt**平台扩展，并使用 **.ntx86**相反。

 

如果包含在 INF**制造商**节条目具有修饰的文本，它还必须包括[ **INF*模型*部分**](inf-models-section.md)名称与匹配的操作系统修饰。 例如，如果 INF 包含以下**制造商**部分：

**%FooCorp%=FooMfg, NTx86....0x80, NTamd64**

则还必须包含 INF [ **INF*模型*各节**](inf-models-section.md)使用以下名称：

-   **\[FooMfg.NTx86....0x80\]**

    此名称适用于 Windows XP 的数据中心套件和更高版本的 Windows 基于 x86 的硬件平台上。

-   **\[FooMfg.NTamd64\]**

    此名称适用于所有产品类型和套件的 Windows XP 和更高版本的 Windows 基于 x64 的硬件平台上。

Windows 安装过程中，选择[ **INF*模型*部分**](inf-models-section.md)如下所示：

1.  如果在基于 x86 的版本包括数据中心产品套件的操作系统 （Windows XP 或更高版本） 中正在运行 Windows，Windows 将选择**\[FooMfg.NTx86...0x80\]** ***模型***部分。
2.  如果 Windows 正在运行的操作系统 （Windows XP 或更高版本） 的任何产品套件基于 x64 的版本中，Windows 将选择**\[FooMfg.NTamd64\]** ***模型***部分。

如果 INF 旨在用于使用操作系统版本早于 Windows XP，则必须还包含未修饰***模型***名为部分 **\[FooMfg\]**。

如果 INF 支持多个制造商生产，每个制造商必须遵循这些规则。

下面的其他示例的*TargetOSVersion*修饰：

-   **%FooCorp% = FooMfg, NTx86**

    在此示例中，结果 INF***模型***节的名称是 **\[FooMfg.NTx86\]**，并适用于任何 x86 版本的操作系统 (Windows XP 或更高版本)。

-   **%FooCorp% = FooMfg, NT.7.8**

    在此示例中，对于版本 7.8 和更高版本的操作系统生成 INF***模型***节的名称是 **\[FooMfg.NT.7.8\]**。 对于早期版本的操作系统，例如，Windows XP **\[FooMfg.NT\]** 使用。

安装程序的所选内容的哪些 INF***模型***要使用的部分根据以下规则：

-   如果包含 INF [ **INF*模型*各节**](inf-models-section.md)的多个的主要和次要运行系统的版本号，Windows 使用最高版本的部分号不在其安装正在进行的操作系统版本比更高版本。
-   如果 INF***模型***部分相匹配的操作系统版本还包括产品类型和/或产品套件修饰，Windows 选择与正在运行的操作系统最匹配的部分。

假设，例如，没有数据中心产品套件的情况下，Windows 正在执行 Windows XP （版本 5.1），并查找中的以下条目**制造商**部分：

**%FooCorp%=FooMfg, NT, NT.5, NT.5.5, NT....0x80**

在这种情况下，Windows 将查找[ **INF*模型*部分**](inf-models-section.md)名为 **\[FooMfg.NT.5\]**。 Windows 还使用**\[FooMfg.NT.5\]** 部分中的特定版本号将优先于产品类型和套件掩码因为如果数据中心版本的 Windows XP 上执行。

如果你想要显式排除的特定操作系统版本、 产品类型或套件 INF，创建一个空[ **INF*模型*部分**](inf-models-section.md)。 例如，名为一个空部分**\[FooMfg.NTx86.6.0\]** 禁止在基于 x86 的操作系统版本 6.0 和更高版本上安装。

<a name="examples"></a>示例
--------

此示例演示**制造商**单一 IHV INF 的典型部分。

```ini
[Manufacturer]
%Mfg%=Contoso        ; Models section == Contoso

[Contoso]

; ...
[Strings]
Mfg = "Contoso, Ltd."
```

下一个示例显示了一部分**制造商**特定于设备的类的安装程序的 INF 的典型部分：

```ini
[Manufacturer]
%CONTOSO%=Contoso_Section
; several entries omitted here for brevity
%FABRIKAM%=Fabrikam_Section
%ADATUM%=Adatum_Section
```

下面的示例演示**制造商**部分特定于 x86 平台，Windows XP 及更高版本：

```ini
[Manufacturer]
%foo%=foosec,NTx86.5.1

[foosec.NTx86.5.1]
```

下面的示例演示**制造商**部分特定于 x64 的平台，Windows 10 版本 14393 及更高版本：

```ini
[Manufacturer]
%foo%=foosec,NTamd64.10.0...14393

[foosec.NTamd64.10.0...14393]
```

以下两个示例演示主干 INF 文件与各种特定于操作系统的 INF*模型*部分：

示例 1：

```ini
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

```ini
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

```ini
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
**注意**：在指定多个 TargetOSVersions 时，将它们排列在一起在一个条目中在此示例中所示。  无法代表每个目标作为一个单独的条目。 

## <a name="see-also"></a>请参阅


[结合使用的操作系统版本的平台扩展](combining-platform-extensions-with-operating-system-versions.md)

[***模型***](inf-models-section.md)

[**Strings**](inf-strings-section.md)

 

 






