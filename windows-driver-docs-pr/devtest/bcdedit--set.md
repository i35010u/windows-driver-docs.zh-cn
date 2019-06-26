---
title: BCDEdit /set
description: BCDEdit/set 命令设置 Windows 引导配置数据存储 (BCD) Windows 7、 Windows Server 2008、 Windows 8、 Windows 8.1，Windows 10、 Windows Server 2012 和 Windows Server 2012 R2 中的启动项选项值。
ms.assetid: e66d9c55-9a44-4de2-a1a4-634c7d550735
ms.date: 02/07/2018
keywords:
- BCDEdit /set Driver Development Tools
topic_type:
- apiref
api_name:
- BCDEdit /set
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7137391bf4ff88f4339fc0e1adf3b0017aeef1f4
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393787"
---
# <a name="bcdedit-set"></a>BCDEdit /set

**BCDEdit /set**命令在 Windows 引导配置数据存储 (BCD) 设置启动项选项值。 使用**BCDEdit /set**命令来配置特定的启动项元素，如内核调试程序设置、 内存选项或启用测试签名的内核模式代码或负载备用硬件抽象层 (HAL) 的选项和内核文件。 若要删除的启动项选项，请使用[ **BCDEdit /deletevalue** ](bcdedit--deletevalue.md)命令。

> [!CAUTION]
> 若要使用 BCDEdit 修改 BCD，所需管理权限。 更改某些启动项选项使用**BCDEdit /set**命令可能导致您的计算机无法运行。 或者，使用系统配置实用程序 (MSConfig.exe) 更改启动设置。

> [!NOTE]
> 设置 BCDEdit 选项之前，您可能需要禁用或暂停 BitLocker 和安全启动的计算机上。

```syntax
bcdedit  /set [{ID}] datatype value
```

## <a name="parameters"></a>Parameters

\[ **{ID}** \]  
**{ID}** 是与启动条目关联的 GUID。 如果未指定 **{ID}** ，命令将修改当前操作系统启动项目。 如果指定的启动项，则与启动项关联的 GUID 必须括在大括号 **{}** 。 若要查看所有活动的引导条目的 GUID 标识符，请使用**bcdedit /enum**命令。 当前引导条目的标识符是 **{当前}** 。 有关此选项的详细信息，请使用以下命令： **bcdedit /？ID**

> [!NOTE]
> 如果使用的[Windows PowerShell](https://go.microsoft.com/fwlink/p/?linkid=108518)，必须使用引号将启动条目标识符，例如： **"{49916baf-0e08-11db-9af4-000bdbd316a0}"** 或 **"{current}"** .

*datatype* *value*  

以下列表显示了一些有用*数据类型*及其关联*值*。

**bootlog** \[ **yes** | **no** \]  
使系统初始化日志。 此日志存储在 %WINDIR%目录中的 Ntbtlog.txt 文件中。 以文本格式，它包括加载和卸载驱动程序的列表。

**bootmenupolicy** \[ **旧版** | **标准** \]  
定义的类型系统将使用的启动菜单。 适用于 Windows 10、 Windows 8.1、 Windows 8 和 Windows RT 默认值是**标准**。 对于 Windows Server 2012 R2，Windows Server 2012 中，默认值是**旧版**。 当**旧版**选择后，高级的选项菜单 (**F8**) 可用。 当**标准**选择，但仅在某些情况下会显示的启动菜单： 例如，如果启动故障，如果您从启动修复磁盘或安装媒体，如果配置了多个启动项或者如果手动配置计算机以使用高级的启动。 当**标准**已选中**F8**在启动过程中忽略的键。 Windows 8 Pc 启动快速因此没有足够的时间来按**F8**。 有关详细信息，请参阅[（包括安全模式） 的 Windows 启动设置](https://go.microsoft.com/fwlink/p/?linkid=313921)。

> [!NOTE]
> 选项为从 Windows 8 和 Windows Server 2012 开始提供。 此外可以使用**onetimeadvancedoptions**若要使用的高级的选项 (**F8**) 菜单 (**旧版**) 在下一步启动一次。

**bootstatuspolicy** *policy*

控制启动状态策略。 启动状态*策略*可以是以下之一：

- `DisplayAllFailures`：如果没有失败的启动、 关闭故障或失败的检查点将显示所有错误。 计算机将故障转移到在重新启动 Windows 恢复环境。

- `IgnoreAllFailures`：如果没有失败的启动、 关闭故障或失败的检查点将忽略错误。 计算机将尝试正常启动，出现错误后。

- `IgnoreShutdownFailures`：如果关闭故障仅忽略错误。 如果关闭故障，计算机不会不自动故障转移到在重新启动 Windows 恢复环境。 这是 Windows 8 的默认设置。

- `IgnoreBootFailures`：仅忽略错误，如果存在失败的引导。 如果失败的引导，计算机不会不自动故障转移到在重新启动 Windows 恢复环境。

- `IgnoreCheckpointFailures`：仅忽略错误，如果存在失败的检查点。 如果失败的检查点，计算机不会不自动故障转移到在重新启动 Windows 恢复环境。 选项为从 Windows 8 和 Windows Server 2012 开始提供。

- `DisplayShutdownFailures`：如果关闭故障，则显示错误。 如果关闭故障，计算机将故障转移到在重新启动 Windows 恢复环境。 将忽略对启动失败和失败的检查点。 选项为从 Windows 8 和 Windows Server 2012 开始提供。

- `DisplayBootFailures`：如果没有失败的引导，则显示错误。 如果失败的引导，计算机将故障转移到在重新启动 Windows 恢复环境。 将忽略关闭故障和失败的检查点。 选项为从 Windows 8 和 Windows Server 2012 开始提供。

- `DisplayCheckpointFailures`：如果没有失败的检查点，则显示错误。 如果失败的检查点，计算机将故障转移到在重新启动 Windows 恢复环境。 将忽略启动和关闭失败。 选项为从 Windows 8 和 Windows Server 2012 开始提供。

**bootux** \[ **disabled** | **basic** | **standard** \]  
控制启动屏幕动画。 可能的值为已禁用、 基本和标准。

> [!NOTE]
> 不支持 Windows 8 和 Windows Server 2012 中。

**disabledynamictick** \[ **yes** | **no** \]  
启用和禁用动态计时器刻度线功能。 

> [!NOTE]
> 此选项应仅用于调试。

**disableelamdrivers** \[ **yes** | **no** \]  
控制早期启动反恶意软件 (ELAM) 驱动程序的加载。 操作系统加载程序中删除此条目出于安全原因。 此选项仅可通过使用 F8 菜单上触发。 人必须在物理上存在 （在计算机上） 来触发此选项。

> [!NOTE]
> 此选项应仅用于调试。 

**forcelegacyplatform** \[ **yes** | **no** \]  
强制 OS 假定旧 PC 设备的状态，如 CMOS 和键盘控制器。

> [!NOTE]
> 此选项应仅用于调试。 

**groupsize** *maxsize*设置的最大逻辑处理器数在单处理器组中，其中*最大大小*是任何介于 1 和 64 （含) 之间的 2 的幂。 默认情况下，处理器组具有的最大大小为 64 个逻辑处理器。 可以使用此启动配置设置重写的大小和计算机的处理器组的构成出于测试目的。 [处理器组](https://go.microsoft.com/fwlink/p/?linkid=155063)多于 64 个逻辑处理器的计算机提供支持。 此启动选项是 64 位版本的 Windows 7 和 Windows Server 2008 R2 和更高版本上可用。 此启动选项具有对 32 位版本的 Windows 7 没有影响。

使用**groupsize**选项如果想要强制多个组，计算机具有 64 或更少活动的逻辑处理器。 有关使用此选项的详细信息，请参阅[测试多个处理器组支持的驱动程序的启动参数](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-parameters-to-test-drivers-for-multiple-processor-group-support)。

**groupaware** \[ **on** | **off** \]  
需要注意的多个处理器组环境中的多个组的强制驱动程序。 使用此选项以帮助公开在驱动程序和组件中的跨组不兼容。 [处理器组](https://go.microsoft.com/fwlink/p/?linkid=155063)多于 64 个逻辑处理器的计算机提供支持。 此启动选项是 64 位版本的 Windows 7 和 Windows Server 2008 R2 和更高版本上可用。 此启动选项具有对 32 位版本的 Windows 7 没有影响。 可以使用**groupaware**选项和**groupsize**选项来测试对函数具有多个组的驱动程序兼容性计算机具有 64 或更少活动的逻辑处理器时。

**Groupaware 上的**设置可确保组 0 以外的组中启动了进程。 这会增加驱动程序和组件之间的跨组交互的机会。 该选项还会修改的旧版功能的行为**KeSetTargetProcessorDpc**， **KeSetSystemAffinityThreadEx**，并**KeRevertToUserAffinityThreadEx**以便它们始终在最高编号组包含活动的逻辑处理器上执行。 应更改驱动程序调用这些旧的函数的任何调用对应的可识别组 (**KeSetTargetProcessorDpcEx**， **KeSetSystemGroupAffinityThread**，和**KeRevertToUserGroupAffinityThread**)。

有关使用此选项的详细信息，请参阅[测试多个处理器组支持的驱动程序的启动参数](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-parameters-to-test-drivers-for-multiple-processor-group-support)。

**hal** *文件*指示操作系统加载程序加载备用 HAL 文件。 指定的文件必须位于 %systemroot%\\system32 目录。

**hypervisorbusparams** *Bus.Device.Function*  
定义 PCI 总线、 设备和函数的调试设备的数字。 例如，1.5.0 介绍总线 1，5，0 函数设备上调试设备。 使用 1394年电缆或 USB 2.0 或 USB 3.0 调试电缆进行调试时，请使用此选项。

**hypervisordebug** \[ **On** | **Off** \]  
控制是否启用了虚拟机监控程序调试器。

**串行**  
指定用于调试的串行连接。 当**串行**指定选项，还设置**hypervisordebugport**并**hypervisorbaudrate**选项。

``` syntax
bcdedit /set hypervisordebugtype serial
bcdedit /set hypervisordebugport 1
bcdedit /set hypervisorbaudrate 115200
bcdedit /set hypervisordebug on
bcdedit /set hypervisorlaunchtype auto
```

**1394**  
指定用于调试的 IEEE 1394 (FireWire) 连接。 使用此选项时， **hypervisorchannel**还应设置选项。

> [!IMPORTANT]
> 1394 传输协议是可在 Windows 10，版本 1607年及更早版本中使用。 不在更高版本的 Windows 中可用。 应转换到其他传输，如使用以太网 KDNET 项目。 有关该传输的详细信息，请参阅[设置向上 KDNET 网络内核调试自动](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-automatically)。


**Net**  
指定用于调试的以太网网络连接。 使用此选项时， **hypervisorhostip**选项必须也是设置。

**hypervisorhostip** *IP 地址*(只使用何时**hypervisordebugtype**是**Net**。)对于通过网络连接调试虚拟机监控程序，指定主机调试器的 IPv4 地址。 有关调试的 HYPER-V 信息，请参阅[使用 HYPER-V 创建虚拟机](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine)。

**hypervisorhostport** \[ *port* \]  
(仅使用何时**hypervisordebugtype**是**Net**。)为网络调试，指定要与主机调试器上进行通信的端口。 应为 49152 或更高版本。

**hypervisordhcp** \[ **yes** | **no** \]  
控件使用的 DHCP 网络调试器与虚拟机监控程序一起使用。 此值设置为**没有**强制使用的自动专用 IP 寻址 (APIPA) 获取链接本地 IP 地址。

**hypervisoriommupolicy** \[ **default** | **enable** | **disable**\]  
控制虚拟机监控程序是否使用输入输出内存管理单元 (IOMMU)。

**hypervisorlaunchtype** \[ **Off** | **Auto** \]  
控制虚拟机监控程序启动选项。 如果您设置了调试器为调试目标计算机上的 HYPER-V，此选项设置为**自动**目标计算机上。 有关详细信息，请参阅[使用 HYPER-V 创建虚拟机](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine)。

**hypervisorloadoptions NOFORCESNOOP** \[ **是** | **否** \]  
指定虚拟机监控程序是否应强制实施系统 IOMMUs 上的 snoop 控制。

**hypervisornumproc** *number*  
指定可以在虚拟机监控程序中启动的逻辑处理器的总数。

**hypervisorrootproc** *number*  
根分区中指定的最大虚拟处理器数和后续拆分非统一内存体系结构 (NUMA) 节点，这可能会在虚拟机监控程序中启动的逻辑处理器的数量限制。

**hypervisorrootprocpernode** *number*  
可在预先拆分，非统一内存体系结构 (NUMA) 节点启动根分区中指定的虚拟处理器的总数。

**hypervisorusekey** \[ *key* \]  
(仅使用何时**hypervisordebugtype**是**Net**。)为网络调试指定用来对连接进行加密密钥。 \[0-9\]并\[a 到 z\]仅允许。

**hypervisoruselargevtlb** \[ **是** | **没有**会增加虚拟转换旁路缓冲器 (TLB) 大小。

**increaseuserva** *兆字节为单位*以兆字节，为用户模式虚拟地址空间中指定的内存量。

在 32 位版本的 Windows 中，应用程序具有 4 千兆字节 (GB) 的可用虚拟地址空间。 虚拟地址空间划分，以便在应用程序可以 2 GB，其他 2GB 是仅供系统。

4 千兆字节优化功能，启用了**increaseuserva**选项，允许您以增加可供该应用程序的虚拟地址空间最多为 3 GB，从而减少量为 1 到 2 之间，系统GB。 **BCEdit increaseuserva /set** *兆字节为单位*命令可以指定 2048 (2GB) 和 3072 (3 GB) 之间的任何值中的十进制格式表示兆字节数。 Windows 使用剩余的地址空间 (GB 减去指定的量) 作为其内核模式地址空间。

请参阅[4gb 的优化 (Windows)](https://docs.microsoft.com/windows/desktop/Memory/4-gigabyte-tuning)有关此功能的其他信息。

**内核***文件*指示操作系统加载程序加载备用内核。 指定的文件必须位于 %systemroot%\\system32 目录。

**loadoptions busparams**=*Bus.Device.Function*时存在多个控制器指定的目标控制器。 使用 1394年电缆或 USB 2.0 调试电缆进行调试时，此语法是适当。 *总线*指定总线数*设备*指定设备数，和*函数*指定的函数数目。

> [!NOTE]
> 用于 1394年调试，总线参数必须指定以十进制，无论哪个配置的 Windows 的版本。 使用 USB 2.0 调试的总线参数的格式取决于 Windows 版本。 Windows Server 2008 中的 USB 2.0 总线参数必须指定以十六进制格式。 在 Windows 7 和 Windows Server 2008 R2 和更高版本的 Windows，USB 2.0 总线参数必须指定以十进制。

**maxgroup** \[ **on** | **off** \]  
最大化处理器组配置中创建的组的数。

**Maxgroup 上的**设置将 NUMA 节点分配到组中最大化的特定计算机的组数的方式。 创建的组数是该计算机有，NUMA 节点数或支持此版本的 Windows 组的最大数目，两者中较小。 默认行为 (**maxgroup 关闭)** 是打包在 NUMA 节点紧密，少组到尽可能。

如果你想要使用多个组、 计算机具有 64 或更少活动逻辑处理器，并且计算机已有多个 NUMA 节点，请使用此选项。 此外可以使用此选项更改具有超过 64 个逻辑处理器的计算机的默认组配置。

[处理器组](https://docs.microsoft.com/windows/desktop/ProcThread/processor-groups)多于 64 个逻辑处理器的计算机提供支持。 此选项是 64 位版本的 Windows 7 和 Windows Server 2008 R2 和更高版本上可用。 此启动选项具有对 32 位版本的 Windows 7 没有影响。

有关使用此选项的详细信息，请参阅[测试多个处理器组支持的驱动程序的启动参数](boot-parameters-to-test-drivers-for-multiple-processor-group-support.md)。

**nointegritychecks** \[ **上** | **关闭**\]禁用完整性检查。 启用安全启动后无法设置。 Windows 7 和 Windows 8，将忽略此值。

**nolowmem** \[ **上** | **关闭**\]控制是否内存不足的使用。 当**nolowmem 上的**指定，则此选项将操作系统、 设备驱动程序和所有应用程序加载到地址超过 4 GB 范围，并指示 Windows 分配所有内存池，在上面 4 GB 范围的地址。 请注意， **nolowmem** Windows 8、 Windows Server 2012 和更高版本的 Windows 中忽略选项。

**novesa** \[ **上** | **关闭**\]指示 VGA 驱动程序是否应避免 VESA BIOS 的调用。 Windows 8 和 Windows Server 2012 中已忽略该选项。

**novga** \[ **上** | **关闭**\]禁止使用 VGA 模式在 OS 中。 选项为从 Windows 8 和 Windows Server 2012 开始提供。

**nx** \[ **Optin |选择禁用 |AlwaysOn |AlwaysOff**\]  
启用、 禁用，并配置数据执行保护 (DEP)，一组旨在防止在受保护的内存位置运行有害代码的硬件和软件技术。 DEP 设置有关的信息，请参阅[数据执行保护](https://docs.microsoft.com/windows/desktop/Memory/data-execution-prevention)。

**Optin**  
仅为操作系统组件，包括 Windows 内核和驱动程序启用 DEP。 管理员可以使用应用程序兼容性工具包 (ACT) 来启用对所选的可执行文件的 DEP。

**选择禁用**  
为操作系统和所有进程，包括 Windows 内核和驱动程序启用 DEP。 但是，管理员可以通过使用禁用所选的可执行文件的 DEP**系统**中**控制面板**。

**AlwaysOn**  
为操作系统和所有进程，包括 Windows 内核和驱动程序启用 DEP。 若要禁用 DEP 的所有尝试将被都忽略。

**AlwaysOff**  
禁用 dep。 有选择地启用 DEP 的尝试将被忽略。

在 Windows Vista 中，此参数还将禁用物理地址扩展 (PAE)。 此参数不会禁用 Windows Server 2008 上的 PAE。

**onecpu** \[ **on** | **off** \]  
强制启动要在具有多个逻辑处理器的计算机中使用的 CPU。

例如，以下命令配置要使用一个处理器的当前操作系统加载程序。

```syntax
bcdedit /set onecpu on
```

**onetimeadvancedoptions** \[ **on** | **off** \]  
下一次启动上的控件是否在系统启动到旧菜单 （F8 菜单）。

> [!NOTE]
> 选项为从 Windows 8 和 Windows Server 2012 开始提供。

```syntax
bcdedit /set {current} onetimeadvancedoptions on
```

**pae** \[ **默认** | **ForceEnable** | **ForceDisable** \]  
启用或禁用物理地址扩展 (PAE)。 启用 PAE 后，系统将加载 Windows 内核的 PAE 版本。

**Pae**参数是仅在 32 位版本的 Windows 在基于 x86 和基于 x64 的处理器的计算机上运行的启动项上有效。 在 32 位版本的 Windows （Windows 8) 之前，默认情况下禁用 PAE。 但是，Windows 会自动启用 PAE 时计算机针对配置热添加内存设备在超过 4 GB 区域中，内存范围内定义的静态资源关系表 (SRAT)。 *热添加内存*支持而无需重新启动或关闭计算机可以添加内存设备。 在这种情况下，在系统启动时，必须启用 PAE，因为它是自动启用，以便系统可以立即解决扩展添加重启之间的内存。 仅在 Windows Server 2008 Datacenter Edition 上支持热添加内存用于基于 Itanium 的系统; Windows Server 2008和所有更高版本的 Windows Server datacenter 和 enterprise 版本上。 此外，对于 Windows Server 2008 之前的 Windows 版本，热添加内存支持仅在 ACPI BIOS，x86 的计算机上处理器和专用的硬件。 对于 Windows Server 2008 和更高版本的 Windows Server，它被支持所有处理器体系结构。

在计算机上，并支持启用了硬件的数据执行保护 (DEP)，则运行 32 位版本的 Windows 操作系统支持 DEP，PAE 会自动启用 DEP 启用时，并且，所有 32 位版本的 Windows 操作系统上除 Windows Server 2003 SP1，PAE 系统已禁用时禁用 dep。 若要启用 PAE DEP 处于禁用状态时，你必须启用 PAE 显式，通过使用**nx AlwaysOff /set**并 **/set pae ForceEnable**。 DEP 的详细信息，请参阅[引导参数配置 DEP 和 PAE](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-parameters-to-configure-dep-and-pae)。

有关使用详细信息**pae**参数和其他参数，会影响 PAE 配置，请参阅[引导参数配置 DEP 和 PAE](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-parameters-to-configure-dep-and-pae)。

**pciexpress** \[ **default** | **forcedisable**\]  
启用或禁用 PCI Express 的功能。 如果计算机平台都支持 PCI Express 功能和 ACPI \_OSC 方法授予控制操作系统功能的 Windows 支持通过 PCI Express 本机控件功能 （这是默认值） 的高级的功能。 使用**forcedisable**选项来替代 PCI Express 的高级的功能，并且使用旧 PCI Express 的行为。 有关详细信息，请参阅[启用 PCI Express 的本机控件在 Windows 中](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn631753(v=vs.85))。

**quietboot** \[ **on** | **off** \]  
控制的高分辨率来代替 Windows 启动屏幕显示和动画位图的显示。 在 Windows Vista 之前的操作系统 **/noguiboot**提供类似功能。

> [!NOTE]
> 不要使用**quietboot**选项在 Windows 8 中，因为它会阻止的 bug 检查数据以外的所有启动图形显示。

**removememory** *兆字节为单位*从操作系统可以使用的总可用内存中删除内存。

例如，以下命令删除大小 256 MB 的内存从总可用到与指定的启动项关联的操作系统。

``` syntax
bcdedit /set {49916baf-0e08-11db-9af4-000bdbd316a0} removememory 256
```

**sos** \[ **on** | **off** \]  
控件的显示驱动程序的名称，像它们在启动过程中加载。 使用**上的 sos**显示的名称。 使用**sos 关闭**禁止显示。

**testsigning** \[ **on** | **off** \]  
控制 Windows 10、 Windows 8.1，Windows 8、 Windows 7、 Windows Server 2008 或 Windows Vista 是否将加载任何类型的测试签名的内核模式代码。 此选项未设置默认情况下，在 64 位版本的 Windows 10、 Windows 8.1，Windows 8、 Windows 7、 Windows Server 2008 上的方式测试签名的内核模式驱动程序和 Windows Vista 将不会加载默认情况下。 在运行 BCDEdit 命令后，重新启动计算机，以便使更改生效。 有关详细信息，请参阅[简介测试签名](https://docs.microsoft.com/windows-hardware/drivers/install/introduction-to-test-signing)。

> [!NOTE]
> 设置 BCDEdit 选项之前，您可能需要禁用或暂停 BitLocker 和安全启动的计算机上。

**tpmbootentropy** \[ **默认** | **ForceEnable** | **ForceDisable**\]  
确定是否从受信任的平台模块 (TPM) 来帮助设置在操作系统中的随机数字生成器种子收集平均信息量。

**truncatememory** *地址*限制可用于 Windows 物理内存量。 在使用此选项，Windows 将忽略所有内存处于或高于指定物理地址。 指定*地址*以字节为单位。

例如，以下命令将物理地址限制设置为 1 GB。 以十进制 (1073741824) 或十六进制 (0x40000000)，可以指定的地址。

``` syntax
bcdedit /set {49916baf-0e08-11db-9af4-000bdbd316a0} truncatememory 0x40000000
```

**tscsyncpolicy** \[ **默认** | **旧版** | **增强** \]  
控件的时间戳计数器同步策略。 此选项应仅用于调试。

> [!NOTE]
> 选项为从 Windows 8 和 Windows Server 2012 开始提供。

**usefirmwarepcisettings** \[ **yes** | **no** \]  
启用或禁用 BIOS 配置外围组件互连 (PCI) 资源的使用。

**useplatformclock** \[ **yes** | **no** \]  
强制使用平台时钟作为系统的性能计数器。

> [!NOTE]
> 此选项应仅用于调试。

**uselegacyapicmode** \[ **yes** | **no** \]  
若要强制旧的 APIC 模式中，即使使用的处理器和芯片集支持扩展 APIC 模式。

**useplatformtick** \[ **yes** | **no** \]  
强制的时钟; 如果要备份的平台源中，通过允许没有综合的计时器。 选项为从 Windows 8 和 Windows Server 2012 开始提供。

> [!NOTE]
> 此选项应仅用于调试。

**vga** \[ **on** | **off** \]  
强制使用安全的解决方法。 例如，在运行 Windows 7 的计算机，此选项将强制使用 640 x 480 分辨率。 在运行 Windows 8 的计算机，此选项不会强制使用 800 x 600 分辨率是否可用，或者 640 x 480。

**xsavedisable** \[ **0** | **1** \]  
当设置为零 (0) 以外的值会禁用 XSAVE 处理器内核中的新功能。

**x2apicpolicy** \[ **enable** | **disable** \]  
启用或禁用的扩展 APIC 模式下，如果受支持。 系统默认为使用扩展 APIC 模式是否可用。

### <a name="comments"></a>备注

有关特定 BCD 元素和启动选项的详细信息，可以使用命令**BCDEdit /？OSLOADER**和**BCDEdit /？类型 OSLOADER**。

若要查看当前启动项目和设置，请使用**bcdedit /enum**命令。 此命令显示活动的引导条目和其关联的全局唯一标识符 (GUID)。 使用与标识符 **/set**命令来配置特定的启动项的选项。

若要删除一个启动选项值，已设置该值，请使用 **/deletevalue**选项。 该命令的语法如下所示：

**bcdedit** /**deletevalue** \[ **{ID}** \] *datatatype*

例如，如果您更改处理器组选项**groupsize**为新值用于测试目的，可以通过键入以下命令，然后重新启动计算机还原为默认值为 64。

``` syntax
bcdedit /deletevalue groupsize
```

对启动选项的任何更改需要重启才能生效。 常用的 BCDEdit 命令有关的信息，请参阅[启动配置数据编辑器常见问题](https://go.microsoft.com/fwlink/p/?linkid=155086)。

## <a name="requirements"></a>要求

|||
|----|----|
|最低受支持的客户端|Windows Vista|
|最低受支持的服务器|Windows Server 2008|
|||

## <a name="see-also"></a>请参阅

- [BCDEdit /deletevalue](bcdedit--deletevalue.md)
