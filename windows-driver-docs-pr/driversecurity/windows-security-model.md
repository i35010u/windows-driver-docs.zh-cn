---
title: 驱动程序开发人员的 Windows 安全模型
description: Windows 安全模型是主要基于每个对象的权限，只有少量的系统范围的权限。
ms.assetid: 3A7ECA7C-1FE6-4ADB-97A9-A61C6FCE9F04
ms.date: 02/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5e1d01bdc20dc36d5f01c9c9135f74296cea7ccc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544661"
---
# <a name="span-idintroductionspanspan-idintroductionspanspan-idintroductionspanwindows-security-model-for-driver-developers"></a><span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>驱动程序开发人员的 Windows 安全模型

Windows 安全模型基于安全对象。 每个组件的操作系统必须确保它所负责的对象的安全性。 驱动程序，因此，必须保护其设备和设备对象的安全性。

本主题概述了如何将 Windows 安全模型适用于内核模式驱动程序。 


## <a name="windows-security-model"></a>Windows 安全模型

Windows 安全模型是主要基于每个对象的权限，只有少量的系统范围的权限。 可以保护的对象包括，— 但不限于，— 进程、 线程、 事件和其他同步对象，以及文件、 目录和设备。

对于每个类型的对象，泛型读取、 写入和执行权限映射到详细的特定于对象的权限。 例如，对于文件和目录，可能的权限包括读取或写入文件或目录、 读取或写入扩展的文件属性的权限、 遍历一个目录的权限和写入对象的安全描述符的权限的权限。 

安全模型涉及到以下概念：

-   安全标识符 (Sid)
-   访问令牌
-   安全描述符
-   访问控制列表 (Acl)
-   权限

### <a name="span-idsecurityidentifierssidsspanspan-idsecurityidentifierssidsspanspan-idsecurityidentifierssidsspansecurity-identifiers-sids"></a><span id="Security_Identifiers__SIDs_"></span><span id="security_identifiers__sids_"></span><span id="SECURITY_IDENTIFIERS__SIDS_"></span>安全标识符 (Sid)


安全标识符 (SID，也称为*主体*) 标识用户、 组或登录会话。 每个用户具有一个唯一的 SID，操作系统在登录时进行检索。

Sid 由如 operating system 或域服务器的颁发机构颁发。 一些 Sid 众所周知，并具有名称和标识符。 例如，SID S-1-1-0 标识每个人 （或世界）。


### <a name="access-tokens"></a>访问令牌

每个进程具有访问令牌。 访问令牌描述过程的完整的安全的上下文。 它包含在用户的 SID 的用户所属的组 SID 和登录会话的 SID，以及授予用户的系统级权限的列表。

默认情况下，系统使用的主访问令牌的进程时进程的线程与安全对象进行交互。 但是，线程可以模拟客户端帐户。 当一个线程模拟时，它具有除其自身的主令牌的模拟令牌。 模拟令牌都描述在线程正在模拟的用户帐户的安全上下文。 模拟是远程过程调用 (RPC) 处理中尤为常见。

介绍了线程或进程的受限制的安全上下文的访问令牌调用受限制的令牌。 中的 Sid*受限的令牌*可以设置只为拒绝访问，不允许访问，对安全对象。 此外，该标记可以描述一组有限的系统范围的权限。 用户的 SID 和标识将保持不变，但用户的访问权限是有限的而进程正在使用受限的令牌。 [CreateRestrictedToken](https://msdn.microsoft.com/library/windows/desktop/aa446583.aspx)函数创建受限的令牌。


### <a name="security-descriptors"></a>安全描述符

每个命名的 Windows 对象具有的安全描述符;某些未命名的对象也可以这样做。 安全描述符描述的所有者和组 Sid 以及其 Acl 对象。

通常由创建该对象的函数创建对象的安全描述符。 当驱动程序调用[IoCreateDevice](https://msdn.microsoft.com/library/windows/hardware/ff548397.aspx)或[IoCreateDeviceSecure](https://msdn.microsoft.com/library/windows/hardware/ff548407.aspx)例程来创建设备对象，系统安全描述符应用到创建的设备对象并设置该对象的 Acl。 适用于大多数设备，设备信息 (INF) 文件中指定 Acl。

有关详细信息[安全描述符](https://docs.microsoft.com/windows-hardware/drivers/kernel/security-descriptors)内核驱动程序文档中。

### <a name="access-control-lists"></a>访问控制列表

访问控制列表 (Acl) 让你精细控制对对象的访问。 ACL 是每个对象的安全描述符的一部分。

每个 ACL 包含零个或多个访问控制项 (ACE)。 每个 ACE，又包含一个单一的 SID 标识用户、 组或计算机和拒绝或允许针对该 SID 的权限的列表。

### <a name="acls-for-device-objects"></a>设备对象的 Acl

可以使用三种方式设置的设备对象的 ACL:

-   在其设备类型的默认安全描述符中设置。
-   以编程方式创建**RtlCreateSecurityDescriptor**函数，并通过设置**RtlSetDaclSecurityDescriptor**函数。
-   指定在安全描述符定义语言 (SDDL) 设备的 INF 文件中或在调用**IoCreateDeviceSecure**例程。

所有驱动程序应使用 INF 文件中 SDDL 来为它们的设备对象指定 Acl。

SDDL 是一种可扩展说明语言，使组件可以创建 Acl 以字符串格式。 SDDL 可供用户模式和内核模式代码。 下图显示了设备对象的 SDDL 字符串的格式。

![设备对象的 sddl 字符串](images/wsm-sddlstrings.gif)

访问值指定允许的访问类型。 SID 值指定确定 （有关示例，用户或组） 的访问值应用到一个安全标识符。

例如，以下 SDDL 字符串允许的系统 (SY) 访问权限的所有内容，并允许每个人都其他 (WD) 仅读取访问权限：

``` syntax
“D:P(A;;GA;;;SY)(A;;GR;;;WD)”
```

标头文件 wdmsec.h 还包括一组预定义适用于设备对象的 SDDL 字符串。 例如，标头文件定义 SDDL\_DEVOBJ\_SYS\_所有\_ADM\_RWX\_世界\_RWX\_RES\_RWX，如下所示：

``` syntax
"D:P(A;;GA;;;SY)(A;;GRGWGX;;;BA)(A;;GRGWGX;;;WD)(A;;GRGWGX;;;RC)"
```

此字符串的第一个段允许的内核和对设备的操作系统 (SY) 完全控制。 第二段允许任何人都内置 Administrators 组 (BA); 若要访问整个设备，但不是能更改 ACL 中。 第三个段，每个人都 (WD) 来读取或写入到设备，并在第四个段授予不受信任的代码 (RC) 到相同的权限。 驱动程序可以使用预定义的字符串按原样或模型的特定于设备的对象的字符串。

堆栈中的所有设备对象应都具有相同的 Acl。 更改堆栈更改整个设备堆栈上的 Acl 中的一个设备对象上的 Acl。

但是，将新的 device 对象添加到堆栈不会更改任何 Acl，这些新的设备对象 （如果它具有 Acl），或者这些堆栈中任何现有设备对象。 该驱动程序时驱动程序创建一个新的设备对象并将其附加到堆栈的顶部，应通过将复制到新的设备对象复制堆栈的 Acl **DeviceObject.Characteristics**字段从下一个较低的驱动程序。

**IoCreateDeviceSecure**例程支持使用预定义如 WD 和 SY Sid 的 SDDL 字符串的子集。 用户模式 Api 和 INF 文件支持完整的 SDDL 语法。

### <a name="security-checks-using-acls"></a>安全检查使用 Acl

当在过程请求对象的访问权限时，安全检查两个比较对象与调用方的访问令牌中的 Sid 的 Acl。

系统比较严格自上而下的顺序的 Ace，并将在第一个相关匹配项处停止。 因此，在创建 ACL 时，应始终将的拒绝 Ace 上述相应授予 Ace。 以下示例演示如何进行比较。

**示例 1:比较到一个访问令牌的 ACL**

示例 1 显示了如何在系统比较到调用方的进程的访问令牌的 ACL。 假定调用方想要打开具有下表中所示的 ACL 的文件。

**示例文件 ACL**

| 权限 | SID        | 访问                |
|------------|------------|-----------------------|
| 允许      | 记帐 | 写入、 删除         |
| 允许      | 销售      | 追加                |
| 拒绝       | 法律      | 追加、 写入、 删除 |
| 允许      | Everyone   | Read                  |

 

此 ACL 具有四个 Ace，这尤其适用于记帐、 销售、 法律和 Everyone 组。

接下来，假定用于发出请求的进程的访问令牌包含 Sid 的一位用户和三个组，按以下顺序：

用户 Jim (S-1-5-21...)

组记帐 (S-1-5-22...)

组法律 (S-1-5-23...)

组 Everyone (S-1-1-0)

当文件 ACL 与访问令牌进行比较，系统首先查找用户文件的 ACL 中 Jim 的 ACE。 没有显示，因此接下来寻找 Accounting 组的 ACE。 上表中所示，文件的 ACL，因此 Jim 中的第一个条目显示 Accounting 组的 ACE ' s 过程授予的权限写入或删除该文件，即停止比较。 如果法律组 ACE 改为在 ACL 中前面为 Accounting 组的 ACE，原本被拒绝进程编写、 添加和删除对文件的访问。

**示例 2:比较到受限令牌的 ACL**

系统将为受限令牌 ACL 与比较不受限制的令牌中的那些相同的方式进行比较。 但是，拒绝 SID 在受限令牌可匹配仅 Deny ACE ACL 中。

示例 2 显示了如何在系统比较使用受限令牌的文件的 ACL。 假定该文件具有相同 ACL 上表中所示。 但是，在此示例中，该过程具有受限制的令牌，其中包含以下 Sid:

用户 Jim (S-1-5-21...)拒绝

组记帐 (S-1-5-22...)拒绝

组法律 (S-1-5-23...)拒绝

组 Everyone (S-1-1-0)

文件的 ACL 不会列出 Jim 的 SID，因此系统将继续到 Accounting 组 SID。 尽管文件的 ACL 具有 Accounting 组的 ACE，但此 ACE 是允许访问;因此，它不匹配的 SID 在进程的受限令牌中，此操作会拒绝访问。 因此，系统将继续到法律组 SID。 该文件的 ACL 包含法律组拒绝访问的 ACE，因此，进程无法写入，追加或删除文件。

### <a name="privileges"></a>权限


特权是用户执行与系统相关的本地计算机上，加载驱动程序、 更改的时间，或关闭系统等操作的权限。

特权是不同的访问权限，因为它们适用于与系统相关的任务和资源，而不是对象，并且它们由系统管理员，而不是由操作系统分配给用户或组。

每个进程的访问令牌包含一系列过程授予的权限。 权限使用之前，必须专门启用。 有关权限的详细信息，请参阅[特权](https://docs.microsoft.com/windows-hardware/drivers/kernel/privileges)内核驱动程序文档中。

 

## <a name="span-idcreating-a-filespanspan-idcreating-a-filespanspan-idcreating-a-filespanwindows-security-model-scenario-creating-a-file"></a><span id="Creating-A-File"></span><span id="CREATING-A-FILE"></span><span id="creating-a-file"></span>Windows 安全模型方案：创建文件

系统使用每当进程创建文件或对象的句柄时的 Windows 安全模型中所述的安全构造。

下图显示了在用户模式进程尝试创建一个文件时被触发的与安全相关的操作。

![创建如下所述的文件示例](images/wsm-creatingafile.gif)

上图显示了系统时在用户模式应用程序调用的响应**CreateFile**函数。 以下说明，请参阅图中的带圆圈数字：

1.  在用户模式应用程序调用**CreateFile**函数，传递有效的 Microsoft Win32 文件名称。
2.  用户模式下 Kernel32.dll 将请求传递给 Ntdll.dll，后者将 Win32 名称转换为 Microsoft Windows NT 文件名称。
3.  Ntdll.dll 调用**NtCreateFile**具有 Windows 文件名称的函数。 内 Ntoskrnl.exe，I/O 管理器处理**NtCreateFile**。
4.  I/O 管理器会请求重新打包到对象管理器调用。
5.  对象管理器解决符号链接，并确保用户具有遍历权限将在其中创建该文件的路径。 有关详细信息，请参阅[安全检查对象管理器中](#omchecks)。
6.  对象管理器调用拥有与请求关联的基础对象类型的系统组件。 对于文件创建请求，该组件是 I/O 管理器，它拥有的设备对象。
7.  I/O 管理器检查针对用户的过程，以确保用户具有对设备的所需的访问权限的访问令牌的设备对象的安全描述符。 有关详细信息，请参阅[安全检查在 I/O 管理器中](#iomanchecks)。
8.  如果用户进程所需的权限，I/O 管理器创建一个句柄，并将发送 IRP\_MJ\_到设备或文件系统驱动程序的创建请求。
9.  该驱动程序根据需要执行额外的安全检查。 例如，如果请求设备的命名空间中指定的对象，该驱动程序必须确保调用方具有所需的访问权限。 有关详细信息，请参阅[驱动程序中的安全检查](#driver)。

### <a name="span-idomchecksspanspan-idomchecksspansecurity-checks-in-the-object-manager"></a><span id="omchecks"></span><span id="OMCHECKS"></span>安全检查对象管理器中

检查访问权限的责任属于可执行此类检查的最高级别的组件。 如果对象管理器可以验证调用方的访问权限，它会这样。 如果没有，对象管理器将请求传递到该组件负责基础对象类型。 该组件，接下来验证访问权限，如果它知道如何操作;如果不能它将请求传递给下一个仍组件，如驱动程序。

对象管理器检查 Acl 对于简单的对象类型，如事件和互斥锁。 对于具有一个命名空间的对象，类型所有者执行安全检查。 例如，I/O 管理器被视为设备对象和文件对象的类型所有者。 如果对象管理器找到设备对象或文件对象的名称解析名称时，它将传送名称到 I/O 管理器，如上面给出的文件创建方案中所示。 如果可以 I/O 管理器然后检查访问权限。 如果名称指定的设备命名空间、 I/O 管理器的对象又移交到设备 （或文件系统） 的名称的驱动程序，并该驱动程序负责验证请求的访问。

### <a name="span-idiomanchecksspanspan-idiomanchecksspansecurity-checks-in-the-io-manager"></a><span id="iomanchecks"></span><span id="IOMANCHECKS"></span>安全检查在 I/O 管理器

当 I/O 管理器创建一个句柄时，它将检查对象的权限，对进程访问令牌并将存储为句柄以及用户授予的权限。 当更高版本的 I/O 请求到达时，I/O 管理器将检查与句柄关联的权限，以确保进程的执行所请求的 I/O 操作的权限。 例如，如果进程更高版本请求写入操作，I/O 管理器将检查与句柄关联的权限，以确保调用方具有对对象的写访问权限。 

如果重复的句柄，可以从副本中删除权限，但不是会添加到它。

当 I/O 管理器创建一个对象时，它将泛型 Win32 访问模式转换为特定于对象的权限。 例如，以下权限适用于文件和目录：


| Win32 访问模式 | 特定于对象的权限 |
|-------------------|------------------------|
|   泛型\_读取   |        ReadData        |
|  泛型\_编写   |       WriteData        |
| 泛型\_EXECUTE  |     ReadAttributes     |
|   泛型\_所有    |          全部           |
 
若要创建一个文件，进程必须具有目标路径中的父目录遍历权限。 例如，若要创建\\设备\\CDROM0\\目录\\File.txt，进程必须有权遍历\\设备\\设备\\CDROM0，并且\\设备\\CDROM0\\目录。 I/O 管理器检查仅这些目录遍历权限。

分析的文件的名称时，I/O 管理器检查遍历权限。 如果文件名的符号链接，I/O 管理器将其解析为完整路径，然后检查从根开始遍历权限。 例如，假定符号链接\\DosDevices\\D 将映射到 Windows NT 设备名\\设备\\CDROM0。 进程必须具有遍历权限\\设备目录。

有关详细信息，请参阅[对象处理](https://docs.microsoft.com/windows-hardware/drivers/kernel/object-handles)并[对象安全](https://docs.microsoft.com/windows-hardware/drivers/kernel/object-security)。

### <a name="span-iddriverspanspan-iddriverspansecurity-checks-in-the-driver"></a><span id="driver"></span><span id="DRIVER"></span>该驱动程序中的安全检查

操作系统内核有效时，将视为具有自己的命名空间的文件系统的每个驱动程序。 因此，当调用方尝试在设备命名空间中创建一个对象，I/O 管理器检查的进程的路径中具有目录遍历权限。 

WDM 驱动程序与 I/O 管理器不执行对的命名空间的安全检查，除非已指定 FILE_DEVICE_SECURE_OPEN 创建设备对象。  如果未设置 FILE_DEVICE_SECURE_OPEN，驱动程序负责确保其命名空间的安全性。 有关详细信息，请参阅[控制设备 Namespace 访问](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-namespace-access)并[保护设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)。

有关 WDF 驱动程序，FILE_DEVICE_SECURE_OPEN 标志始终设置，以便将检查设备的安全描述符的才允许应用程序访问设备的命名空间内的任何名称。 有关详细信息，请参阅[控制 KMDF 驱动程序中的设备访问](https://docs.microsoft.com/windows-hardware/drivers/wdf/controlling-device-access-in-kmdf-drivers)。



## <a name="windows-security-boundaries"></a>Windows 安全边界

驱动程序进行通信和对用户模式下的不同权限级别的调用方可以被视为跨越信任边界。 信任边界是从较低的特权进程跨越到更高特权的进程的任何代码执行路径。

更高版本不一致会在权限级别，更有趣的边界想要执行对目标的驱动程序或进程的特权提升攻击等攻击的攻击者。

创建威胁模型的一部分是过程的检查安全边界并查找未预料到的路径。 有关详细信息，请参阅[驱动程序的威胁建模](threat-modeling-for-drivers.md)。 

跨信任边界的任何数据不受信任和必须进行验证。 

下图显示了三个内核驱动程序和两个应用，应用程序容器和一个用管理员权限运行的应用程序中的一个。 红线指示示例信任边界。

![显示三个内核驱动程序和两个应用，一个应用程序容器中的驱动程序攻击面](images/driver-security-attack-surface.png)

应用容器可以提供其他约束，并在管理员级别未运行，路径 (1) 是提升攻击的更高风险路径，因为应用程序容器 （非常低权限进程） 和内核驱动程序之间是信任边界。 

路径 (2) 是较低的风险路径，如应用程序管理员权限运行，而在内核驱动程序中直接调用。 管理员已在系统上的拥有很高特权，因此管理员提供的对内核的攻击面，而不给攻击者，一个有趣的目标，但仍值得一提的信任边界。

路径 (3) 是跨多个创建威胁模型时，可能会丢失的信任边界的代码执行路径的示例。
在此示例中，则驱动程序 1 和 3，驱动程序之间的信任边界因为驱动程序 1 将输入的用户模式应用并将其传递直接向驱动程序 3。

所有输入传入从用户模式驱动程序是不受信任，应验证。 输入来自其他驱动程序也可能是不受信任，具体取决于以前的驱动程序是否只是简单的传递 （例如数据已接收到从应用程序 1 的驱动程序 1，驱动程序 1 未执行此操作对数据的任何验证，只需传递其前滚到驱动程序 3）。 请务必确定所有的攻击面和信任边界，并验证处理，通过创建完整的威胁模型的所有数据。


## <a name="windows-security-model-recommendations"></a>Windows 安全模型建议 

-   在调用设置强默认 Acl **IoCreateDeviceSecure**例程。
-   每个设备的 INF 文件中指定 Acl。 如有必要，这些 Acl 可以放宽紧密的默认 Acl。
-   将文件设置\_设备\_SECURE\_打开特性要应用于设备命名空间的设备对象的安全设置。
-   未定义允许文件的 Ioctl\_ANY\_访问，除非此类访问不能被恶意利用。
-   使用**IoValidateDeviceIoControlAccess**例程，以增强安全性上允许的文件的现有 IOCTL\_ANY\_访问。
-   创建威胁模型来检查安全边界，并查找未预料到的路径。 有关详细信息，请参阅[驱动程序的威胁建模](threat-modeling-for-drivers.md)。 
-   请参阅[驱动程序安全核对清单](driver-security-checklist.md)为其他驱动程序的安全建议。


### <a name="see-also"></a>另请参阅

[保护设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)

[驱动程序安全清单](driver-security-checklist.md)







