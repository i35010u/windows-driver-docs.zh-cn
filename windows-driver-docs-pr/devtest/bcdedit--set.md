---
title: BCDEdit /set
description: BCDEdit/set 命令在 Windows 7、Windows Server 2008、Windows 8、Windows 8.1、Windows 10、Windows Server 2012 和 Windows Server 2012 R2 的 Windows 启动配置数据存储 (BCD) 中设置启动项目选项值。
ms.assetid: e66d9c55-9a44-4de2-a1a4-634c7d550735
ms.date: 02/07/2018
keywords:
- BCDEdit /set 驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /set
api_type:
- NA
ms.localizationpriority: high
ms.openlocfilehash: 3d23d3cb03193b83601342d5fc35b9aa82864d55
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384397"
---
# <a name="bcdedit-set"></a>BCDEdit /set

BCDEdit/set 命令在 Windows 启动配置数据存储 (BCD) 中设置启动项目选项值。 使用 BCDEdit /set 命令可配置特定的启动项目元素，如内核调试程序设置、内存选项或启用测试签名的内核模式代码或负载备用硬件抽象层 (HAL) 的选项和内核文件。 若要删除启动项目选项，请使用 [BCDEdit/deletevalue](bcdedit--deletevalue.md) 命令。

> [!CAUTION]
> 需要管理权限才能使用 BCDEdit 来修改 BCD。 使用 BCDEdit /set 命令更改某些启动项目选项可能导致计算机无法运行。 请改为使用系统配置实用程序 (MSConfig.exe) 更改启动设置。

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

```syntax
bcdedit  /set [{ID}] datatype value
```

## <a name="parameters"></a>参数

\[ **{ID}** \]  
{ID} 是与启动项关联的 GUID。 如果未指定 {ID}，命令将修改当前操作系统启动项。 如果指定了启动目，则必须用大括号 { } 将与启动项关联的 GUID 括起来。 要查看所有活动启动项的 GUID 标识符，请使用 bcdedit /enum 命令。 当前启动项的标识符是 {current}。 有关此选项的详细信息，请使用以下命令：bcdedit /?ID

> [!NOTE]
> 如果使用 [Windows PowerShell](/powershell/module/Microsoft.PowerShell.Core/?view=powershell-6)，必须使用引号将启动项标识符引起来，例如：“{49916baf-0e08-11db-9af4-000bdbd316a0}”或“{current}” 。

*datatype* *value*  

以下列表显示了一些有用的数据类型及其关联值 。

**bootlog** \[ **yes** | **no** \]  
启用系统初始化日志。 此日志存储在 %WINDIR% 目录中的 Ntbtlog.txt 文件中。 它包括以文本格式加载和卸载的驱动程序列表。

**bootmenupolicy** \[ **Legacy** | **Standard** \]  
定义系统将使用的启动菜单类型。 对于 Windows 10、Windows 8.1、Windows 8 和 Windows RT，默认值为 Standard。 对于 Windows Server 2012 R2 和 Windows Server 2012，默认值为 Legacy。 选择 Legacy 时，“高级选项”菜单 (F8) 可用 。 选择 Standard 时，仅在某些情况下会显示启动菜单：例如，出现启动故障、从修复磁盘或安装媒体启动、配置了多个启动项目或手动配置了计算机以使用高级启动。 选择 Standard 时，在启动过程中将忽略 F8 键 。 Windows 8 电脑会快速启动，因此没有足够的时间按 F8。 有关详细信息，请参阅[ Windows 启动设置（包括安全模式）](https://support.microsoft.com/help/17076/windows-8-startup-settings-safe-mode)。

> [!NOTE]
> 此选项从 Windows 8 和 Windows Server 2012 开始提供。 还可以使用 onetimeadvancedoptions 在下一次启动时使用一次高级选项 (F8) 菜单 (Legacy)  。

**bootstatuspolicy** *policy*

控制启动状态策略。 启动状态策略可以是以下项之一：

- `DisplayAllFailures`：如果存在启动故障、关闭故障或检查点故障，则将显示所有错误。 重新启动时，计算机会将故障转移到 Windows 恢复环境。

- `IgnoreAllFailures`：如果存在启动故障、关闭故障或检查点故障，则将忽略所有错误。 出现错误后，计算机将尝试正常启动。

- `IgnoreShutdownFailures`：仅关机失败时，才忽略错误。 如果关机失败，计算机不会在重新启动时自动故障转移到 Windows 恢复环境。 这是 Windows 8 的默认设置。

- `IgnoreBootFailures`：仅启动失败时，才忽略错误。 如果启动失败，计算机不会在重新启动时自动故障转移到 Windows 恢复环境。

- `IgnoreCheckpointFailures`：仅检查点失败时，才忽略错误。 如果检查点失败，计算机不会在重新启动时自动故障转移到 Windows 恢复环境。 此选项从 Windows 8 和 Windows Server 2012 开始提供。

- `DisplayShutdownFailures`：仅关机失败时，才显示错误。 如果关机失败，计算机会在重新启动时故障转移到 Windows 恢复环境。 忽略启动故障和检查点故障。 此选项从 Windows 8 和 Windows Server 2012 开始提供。

- `DisplayBootFailures`：仅启动失败时，才显示错误。 如果启动失败，计算机会在重新启动时故障转移到 Windows 恢复环境。 忽略关机故障和检查点故障。 此选项从 Windows 8 和 Windows Server 2012 开始提供。

- `DisplayCheckpointFailures`：仅检查点失败时，才显示错误。 如果检查点失败，计算机会在重新启动时故障转移到 Windows 恢复环境。 忽略启动和关机故障。 此选项从 Windows 8 和 Windows Server 2012 开始提供。

**bootux** \[ **disabled** | **basic** | **standard** \]  
控制启动屏幕动画。 可能的值为 disabled、basic 和 standard。

> [!NOTE]
> Windows 8 和 Windows Server 2012 不支持。

**disabledynamictick** \[ **yes** | **no** \]  
启用和禁用动态计时器时钟周期功能。 

> [!NOTE]
> 此选项应仅用于调试。

**disableelamdrivers** \[ **yes** | **no** \]  
控制开机初期启动的反恶意软件 (ELAM) 驱动程序的加载。 出于安全原因，OS 加载程序删除了此条目。 此选项只能通过使用 F8 菜单触发。 用户必须当场出现（在计算机上）才能触发此选项。

> [!NOTE]
> 此选项应仅用于调试。 

**forcelegacyplatform** \[ **yes** | **no** \]  
强制 OS 假定存在旧式电脑设备，如 CMOS 和键盘控制器。

> [!NOTE]
> 此选项应仅用于调试。 

**groupsize** *maxsize* 设置单个处理器组中逻辑处理器的最大数量，其中最大大小为介于 1 到 64（含）之间 2 的任意次幂。 默认情况下，处理器组的最大大小为 64 个逻辑处理器。 可以使用此启动配置设置来替代计算机处理器组的大小和组成，以便进行测试。 [处理器组](/windows/win32/procthread/processor-groups)对具有超过 64 个逻辑处理器的计算机提供支持。 此启动选项适用于 64 位版本的 Windows 7 和 Windows Server 2008 R2 及更高版本。 此启动选项对 32 位版本的 Windows 7 不起作用。

如果要强制多个组，并且计算机的可用逻辑处理器不超过 64 个，请使用 groupsize 选项。 有关使用此选项的详细信息，请参阅[用于测试驱动程序是否支持多个处理器组的启动参数](./boot-parameters-to-test-drivers-for-multiple-processor-group-support.md)。

**groupaware** \[ **on** | **off** \]  
强制驱动程序了解多个处理器组环境中的多个组。 使用此选项可帮助公开驱动程序和组件中的跨组不兼容性。 [处理器组](/windows/win32/procthread/processor-groups)对具有超过 64 个逻辑处理器的计算机提供支持。 此启动选项适用于 64 位版本的 Windows 7 和 Windows Server 2008 R2 及更高版本。 此启动选项对 32 位版本的 Windows 7 不起作用。 当计算机的可用逻辑处理器不超过 64 个时，可以使用 groupaware 选项和 groupsize 选项来测试驱动程序是否与多个组兼容 。

groupaware on 设置可确保进程在组 0 以外的组中启动。 这增加了驱动程序和组件之间跨组交互的机会。 该选项还会修改旧函数 KeSetTargetProcessorDpc、KeSetSystemAffinityThreadEx 和 KeRevertToUserAffinityThreadEx 的行为，以便它们始终对包含可用逻辑处理器的最高编号组进行操作  。 调用任何这些旧函数的驱动程序应更改为调用其组感知对应项（KeSetTargetProcessorDpcEx、KeSetSystemGroupAffinityThread 和 KeRevertToUserGroupAffinityThread）  。

有关使用此选项的详细信息，请参阅[用于测试驱动程序是否支持多个处理器组的启动参数](./boot-parameters-to-test-drivers-for-multiple-processor-group-support.md)。

hal file 指示操作系统加载程序加载备用 HAL 文件。 指定的文件必须位于 %SystemRoot%\\system32 目录中。

**hypervisorbusparams** *Bus.Device.Function*  
定义调试设备的 PCI 总线、设备和功能号。 例如，1.5.0 描述调试设备的总线 1、设备 5、功能 0。 这些值显示在“常规”选项卡上的“位置”下的设备管理器中 。  

**hypervisordebug** \[ **On** | **Off** \]  
控制是否启用虚拟机监控程序调试器。

**串行**  
指定用于调试的串行连接。 指定“串行”选项时，还可以设置 hypervisordebugport 和 hypervisorbaudrate 选项  。

``` syntax
bcdedit /set hypervisordebugtype serial
bcdedit /set hypervisordebugport 1
bcdedit /set hypervisorbaudrate 115200
bcdedit /set hypervisordebug on
bcdedit /set hypervisorlaunchtype auto
```

**1394**  
指定用于调试的 IEEE 1394 (FireWire) 连接。 使用此选项时，还应设置 hypervisorchannel 选项。

> [!IMPORTANT]
> 1394 传输可用于 Windows 10 版本 1607 及更低版本。
> 它在 Windows 的更高版本中不可用。 应将项目转换为其他传输，例如使用以太网的 KDNET。 有关该传输的详细信息，请参阅[自动设置 KDNET 网络内核调试](../debugger/setting-up-a-network-debugging-connection-automatically.md)。


**Net**  
指定用于调试的以太网网络连接。 使用此选项时，务必设置 hypervisorhostip 选项。

**hypervisorhostip** *IP address*仅 hypervisordebugtype 为 Net 时使用。 ）若要通过网络连接调试虚拟机监控程序，请指定主机调试器的 IPv4 地址。 有关对 Hyper-V 进行调试的信息，请参阅[使用 Hyper-V 创建虚拟机](/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine)。

**hypervisorhostport** \[ *port* \]  
（仅 hypervisordebugtype 为 Net 时使用。 ）对于网络调试，请指定要在主机调试器上通信的端口。 必须是 49152 或以上。

**hypervisordhcp** \[ **yes** | **no** \]  
控制虚拟机监控程序所使用的网络调试器使用 DHCP。 将此选项设置为不强制使用自动专用 IP 地址 (APIPA) 获取本地链接 IP 地址。

**hypervisoriommupolicy** \[ **default** | **enable** | **disable**\]  
控制虚拟机监控程序是否使用输入输出内存管理单元 (IOMMU)。

**hypervisorlaunchtype** \[ **Off** | **Auto** \]  
控制虚拟机监控程序启动选项。 如果要设置调试器以在目标计算机上调试 Hyper-V，请在目标计算机上将此选项设置为“自动”。 有关详细信息，请参阅[使用 Hyper-V 创建虚拟机](/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine)。

**hypervisorloadoptions NOFORCESNOOP** \[ **Yes** | **No** \]  
指定虚拟机监控程序是否应对系统 IOMMU 执行窥探控制。

**hypervisornumproc** *number*  
指定可在虚拟机监控程序中启动的逻辑处理器的总数。

**hypervisorrootproc** *number*  
指定根分区中虚拟处理器的最大数量，并限制拆分后非一致性内存体系结构 (NUMA) 节点的数量，这些节点可以在虚拟机监控程序中启动逻辑处理器。

**hypervisorrootprocpernode** *number*  
指定根分区中可在预拆分非一致性内存体系结构 (NUMA) 节点内启动的虚拟处理器总数。

**hypervisorusekey** \[ *key* \]  
（仅 hypervisordebugtype 为 Net 时使用。 ）对于网络调试，请指定用于加密连接的密钥。 只允许 0-9 和 a-z 中的字符\[\]\[\]。

**hypervisoruselargevtlb** \[ **yes** | **no** 增加虚拟 Translation Lookaside Buffer (TLB) 大小。

**increaseuserva** *Megabytes* 指定用户模式虚拟地址空间的内存量（以兆字节为单位）。

在 Windows 的 32 位版本中，应用程序的可用虚拟地址空间为 4 GB。 分配此虚拟地址空间，让应用程序使用 2 GB 空间，另外 2 GB 仅限系统使用。

使用 increaseuserva 选项启用的 4 GB 调优功能，可以将应用程序可用的虚拟地址空间增加到 3 GB，从而将系统可用的内存量减少到 1 到 2 GB。 BCEdit /set increaseuserva Megabytes 命令可以指定十进制表示法中 2048 (2 GB) 和 3072 (3 GB) 兆字节之间的任何值。 Windows 使用剩余的地址空间（4 GB 减去指定数量）作为其内核模式地址空间。

有关此功能的其他信息，请参阅 [4 GB 优化 (Windows)](/windows/desktop/Memory/4-gigabyte-tuning)。

**kernel** *file* 指示操作系统加载程序加载备用内核。 指定的文件必须位于 %SystemRoot%\\system32 目录中。

**loadoptions busparams**=*Bus.Device.Function* 指定目标控制器。 Bus 指定总线号，Device 指定设备号，Function 指定功能号  。 这些值显示在“常规”选项卡上的“位置”下的设备管理器中 。  

> [!NOTE]
> 对于 1394 调试，无论配置的是哪个版本的 Windows，都必须以十进制形式指定总线参数。 用于 USB 2.0 调试的总线参数的格式取决于 Windows 版本。 在 Windows Server 2008 中，必须以十六进制指定 USB 2.0 总线参数。 在 Windows 7 和 Windows Server 2008 R2 及 Windows 更高版本中，必须以十进制形式指定USB 2.0 总线参数。

**maxgroup** \[ **on** | **off** \]  
最大化在处理器组配置中创建的组数。

“maxgroup on”设置以最大化特定计算机的组数的方式将 NUMA 节点分配给组。 创建的组数是计算机具有的 NUMA 节点数，或者此 Windows 版本支持的最大组数（以较小者为准）。 默认行为 (maxgroup off) 是将 NUMA 节点紧密地打包到尽可能少的组中。

如果希望使用多个组，那么使用此选项需要满足两个条件：计算机的可用逻辑处理器不超过 64 个，并且计算机已具有多个 NUMA 节点。 如果计算机的逻辑处理器数超过 64 个，那么还可使用此选项来更改计算机的默认组配置。

[处理器组](/windows/desktop/ProcThread/processor-groups)对具有超过 64 个逻辑处理器的计算机提供支持。 此选项适用于 64 位版本的 Windows 7 和 Windows Server 2008 R2 及更高版本。 此启动选项对 32 位版本的 Windows 7 不起作用。

有关使用此选项的详细信息，请参阅[用于测试驱动程序是否支持多个处理器组的启动参数](boot-parameters-to-test-drivers-for-multiple-processor-group-support.md)。

**nointegritychecks** \[ **on** | **off** \] 禁用完整性检查。 启用安全启动时无法设置。 Windows 7 和 Windows 8 将忽略此值。

**nolowmem** \[ **on** | **off** \] 控制低内存的使用。 指定为“nolowmem on”时，此选项会将操作系统、设备驱动程序和所有应用程序加载到 4 GB 边界以上的地址中，并指示 Windows 在 4 GB 边界以上的地址分配所有内存池。 请注意，Windows 8、Windows Server 2012 和 Windows 更高版本会忽略 nolowmem 选项。

**novesa** \[ **on** | **off** \] 指示 VGA 驱动程序是否应避免 VESA BIOS 调用。 Windows 8 和 Windows Server 2012 将忽略该选项。

**novga** \[ **on** | **off** \] 禁用 OS 中的 VGA 模式。 该选项从 Windows 8 和 Windows Server 2012 开始提供。

**nx** \[**Optin |OptOut | AlwaysOn |AlwaysOff**\]  
启用、禁用和配置数据执行保护 (DEP)，这是一组硬件和软件技术，旨在防止有害代码在受保护的内存位置运行。 有关 DEP 设置的信息，请参阅[数据执行保护](/windows/desktop/Memory/data-execution-prevention)。

**Optin**  
仅为操作系统组件启用 DEP，包括 Windows 内核和驱动程序。 管理员可以使用应用程序兼容性工具包 (ACT) 在选定的可执行文件上启用 DEP。

**Optout**  
为操作系统和所有进程（包括 Windows 内核和驱动程序）启用 DEP。 但是，管理员可以使用“控制面板”中的“系统”来禁用所选可执行文件的 DEP 。

**AlwaysOn**  
为操作系统和所有进程（包括 Windows 内核和驱动程序）启用 DEP。 将忽略禁用 DEP 的所有尝试。

**AlwaysOff**  
禁用 DEP。 将忽略有选择地启用 DEP 的尝试。

在 Windows Vista 上，还可使用此参数禁用物理地址扩展 (PAE)。 在 Windows Server 2008 上，使用此参数无法禁用 PAE。

**onecpu** \[ **on** | **off** \]  
仅强制在具有多个逻辑处理器的计算机中使用启动 CPU 。

例如，以下命令将当前操作系统加载程序配置为使用一个处理器。

```syntax
bcdedit /set onecpu on
```

**onetimeadvancedoptions** \[ **on** | **off** \]  
控制系统是否引导到下一个启动时的旧菜单（F8 菜单）。

> [!NOTE]
> 该选项从 Windows 8 和 Windows Server 2012 开始提供。

```syntax
bcdedit /set {current} onetimeadvancedoptions on
```

**pae** \[ **Default** | **ForceEnable** | **ForceDisable** \]  
启用或禁用物理地址扩展 (PAE)。 启用 PAE 后，系统将加载 Windows 内核的 PAE 版本。

pae 参数仅在 32 位版本的 Windows 的启动项目上有效，该版本在具有基于 x86 和 x64 的处理器的计算机上运行。 在 Windows 的 32 位版本（Windows 8 之前）上，默认情况下禁用 PAE。 但是，计算机配置为内存范围超过 4 GB 区域的热添加内存设备时，Windows 会自动启用 PAE，这是静态资源关联表 (SRAT) 定义的。 “热添加内存”支持无需重新启动或关闭计算机即可添加的内存设备。 在这种情况下，由于必须在系统启动时启用 PAE，因此会自动启用它，以便系统可以立即对重启之间添加的扩展内存进行寻址。 热添加内存仅在以下版本中受支持：Windows Server 2008（数据中心版本）、面向基于 Itanium 系统的 Windows Server 2008 以及所有更高版本的 Windows Server 的数据中心和企业版。 此外，对于 Windows Server 2008 之前的 Windows 版本，热添加内存仅在具有 ACPI BIOS、x86 处理器和专用硬件的计算机上受支持。 对于 Windows Server 2008 和更高版本的 Windows Server，所有处理器体系结构都支持热添加内存。

对于支持启用硬件的数据执行保护 (DEP) 的计算机，如何正在运行支持 DEP 的 32 位版本的 Windows 操作系统，则启用 DEP 时会在所有 32 位版本的 Windows 操作中（Windows Server 2003 SP1 除外）自动启用 PAE，并在禁用 DEP 时禁用 PAE。 若要在禁用 DEP 时启用 PAE，必须通过使用 /set nx AlwaysOff 和 /set pae ForceEnable 来显式启用 PAE 。 有关 DEP 的详细信息，请参阅[用于配置 DEP 和 PAE 的启动参数](./boot-parameters-to-configure-dep-and-pae.md)。

有关使用 pae 参数和影响 PAE 配置的其他参数的详细信息，请参阅[用于配置 DEP 和 PAE 的启动参数](./boot-parameters-to-configure-dep-and-pae.md)。

**pciexpress** \[ **default** | **forcedisable**\]  
启用或禁用 PCI Express 功能。 如果计算机平台支持 PCI Express 功能，并且 ACPI \_OSC 方法将功能的控制权授予操作系统，Windows 将通过 PCI Express 本机控制功能启用高级功能（这是默认设置）。 使用 forcedisable 选项替代高级 PCI Express 功能并使用旧版 PCI Express 行为。 有关详细信息，请参阅[在 Windows 中启用 PCI Express 本机控制](/previous-versions/windows/hardware/design/dn631753(v=vs.85))。

**quietboot** \[ **on** | **off** \]  
控制高分辨率位图的显示，以代替 Windows 启动屏幕的显示和动画。 在 Windows Vista 之前的操作系统中，/noguiboot 具有类似的功能。

> [!NOTE]
> 请勿在 Windows 8 中使用 quietboot 选项，因为它会阻止显示错误检查数据（所有启动图形除外）。

**removememory** *Megabytes* 从操作系统可以使用的总可用内存中删除内存。

例如，以下命令从与指定启动项关联的操作系统可用的总计中删除 256 MB 的内存。

``` syntax
bcdedit /set {49916baf-0e08-11db-9af4-000bdbd316a0} removememory 256
```

**sos** \[ **on** | **off** \]  
控制驱动程序在启动过程中加载时的名称的显示。 使用 sos on 可显示名称。 使用 sos off 可禁止显示。

**testsigning** \[ **on** | **off** \]  
控制 Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2008 或 Windows Vista 是否会加载任何类型的测试签名内核模式代码。 默认情况下不设置此选项，这意味着在 Windows 10、Windows 8.1、Windows 8、Windows 7、Windows Server 2008 和 Windows Vista 的 64 位版本上默认不加载测试签名的内核模式驱动程序。 运行 BCDEdit 命令后，重启计算机，使更改生效。 有关详细信息，请参阅 [测试签名简介](../install/introduction-to-test-signing.md)。

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

**tpmbootentropy** \[ **default** | **ForceEnable** | **ForceDisable**\]  
确定是否从受信任的平台模块 (TPM) 收集熵，以帮助在操作系统中设定随机数生成器的种子。

**truncatememory** *address* 限制 Windows 可用的物理内存量。 使用此选项时，Windows 会忽略指定物理地址或以上的所有内存。 指定地址（以字节为单位）。

例如，以下命令将物理地址限制设置为 1 GB。 可以以十进制 (1073741824) 或十六进制 (0x40000000) 指定地址。

``` syntax
bcdedit /set {49916baf-0e08-11db-9af4-000bdbd316a0} truncatememory 0x40000000
```

**tscsyncpolicy** \[ **Default** | **Legacy** | **Enhanced** \]  
控制时间戳计数器同步策略。 此选项应仅用于调试。

> [!NOTE]
> 该选项从 Windows 8 和 Windows Server 2012 开始提供。

**usefirmwarepcisettings** \[ **yes** | **no** \]  
启用或禁用使用 BIOS 配置的外围组件互连 (PCI) 资源。

**useplatformclock** \[ **yes** | **no** \]  
强制使用平台时钟作为系统的性能计数器。

> [!NOTE]
> 此选项应仅用于调试。

**uselegacyapicmode** \[ **yes** | **no** \]  
用于强制旧的 APIC 模式，即使处理器和芯片集支持扩展 APIC 模式也是如此。

**useplatformtick** \[ **yes** | **no** \]  
强制时钟由平台源备份，不允许合成计时器。 该选项从 Windows 8 和 Windows Server 2012 开始提供。

> [!NOTE]
> 此选项应仅用于调试。

**vga** \[ **on** | **off** \]  
强制使用安全分辨率。 例如，在运行 Windows 7 的计算机上，此选项强制使用 640x480 分辨率。 在运行 Windows 8 的计算机上，此选项强制使用 800x600 分辨率（如果可用）；如果没有，则强制使用 640x480 分辨率。

**xsavedisable** \[ **0** | **1** \]  
设置为零 (0) 以外的值时，禁用内核中的 XSAVE 处理器功能。

**x2apicpolicy** \[ **enable** | **disable** \]  
启用或禁用扩展 APIC 模式（如果支持）。 如果系统可用，则默认使用扩展的 APIC 模式。

### <a name="comments"></a>备注

有关特定 BCD 元素和启动选项的详细信息，可以使用命令 BCDEdit /?OSLOADER 和 BCDEdit /?TYPES OSLOADER。

若要查看当前启动项及其设置，请使用 bcdedit /enum 命令。 此命令显示可用启动项及其关联的全局唯一标识符 (GUID)。 使用带有 /set 命令的标识符来配置特定启动项的选项。

若要删除已设置的启动选项值，请使用 /deletevalue 选项。 该命令的语法如下：

**bcdedit** /**deletevalue** \[ **{ID}** \] *datatatype*

例如，如果将处理器组选项 groupsize 更改为用于测试目的的新值，则可以通过键入以下命令，然后重启计算机，恢复到默认值 64。

``` syntax
bcdedit /deletevalue groupsize
```

对启动选项的任何更改都需要重启才能生效。 有关常用 BCDEdit 命令的详细信息，请参阅[引导配置数据编辑器常见问题](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc721886(v=ws.10))。

## <a name="requirements"></a>要求

**支持的最低客户端版本**：Windows Vista

**支持的最低服务器版本**：Windows Server 2008

****： 


## <a name="see-also"></a>另请参阅

- [BCDEdit /deletevalue](bcdedit--deletevalue.md)