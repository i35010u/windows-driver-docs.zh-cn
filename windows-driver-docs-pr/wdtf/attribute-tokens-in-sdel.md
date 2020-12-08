---
title: SDEL 中的特性标记
description: 介绍用于定义目标设备和计算机的特征的 SDEL 特性标记。
keywords:
- SDEL
- 特性标记
ms.date: 09/03/2020
ms.localizationpriority: medium
ms.openlocfilehash: cb532cce5bd2b707e2f9abf45bb5daadfa7d592e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823663"
---
# <a name="attribute-tokens-in-sdel"></a>SDEL 中的特性标记

SDEL 语言使用目标属性令牌来定义目标设备和计算机的特征。

## <a name="root-attribute-tokens-for-all-targets"></a>所有目标的根特性标记

下表描述了根命名空间中对所有目标有效的属性。

|关键字|VARIANT 类型|描述|
|----|----|----|
|类型|VT_BSTR|定义目标的类型。 此值可以是 "System" 或 "Device"。|

## <a name="root-attribute-tokens-for-a-device-target"></a>设备目标的根特性标记

下表描述了根命名空间中仅对设备类型目标有效的属性。

>[!NOTE]
>以下大多数属性都是通过 SetupDi Api 从操作系统检索的。 有关此 Api 的详细信息，请参阅 SetupDiGetDeviceRegistryProperty。

|关键字|VARIANT 类型|描述|
|----|----|----|
|地址|VT_I4|特定于类的 (或特定于总线的) 地址。|
|BusNumber|VT_I4|设备的总线号。|
|功能|VT_I4|设备的功能。|
|字符|VT_I4|DWORD 中设备特性标志的按位 "或"。  (SPDRP_CHARACTERISTICS) |
|类|VT_BSTR|设备的类。|
|ClassGUID|VT_BSTR|设备的类（以 GUID 形式）。 使用本地化版本时，请使用此关键字而不是类字段。|
|CompatIDs|VT_ARRAY 具有 VT_BSTR 的变体|为此设备定义的所有兼容 Id。|
|ConfigFlags|VT_I4|设备的配置标志。|
|描述|VT_BSTR|设备描述。|
|DeviceID|VT_BSTR|设备标识符，包括设备的实例标识符。 此字符串是系统中每个设备的唯一字符串。|
|DeviceStatusString|VT_BSTR|同时包含 StatusString 和 ProblemCodeString 中的一个字符串。|
|DevInst|VT_I4|设备实例的不透明句柄。|
|DevType|VT_I4|表示设备的类型。  (SPDRP_DEVTYPE) |
|DisplayName|VT_BSTR|解析为从左到右 (找到的第一个值) 以下属性： FriendlyName、Description 或 DeviceID。|
|驱动程序|VT_BSTR|HKLM\System\CurrentControlSet\Control\Class\ 中的一个密钥，用于保存有关驱动程序的详细信息。|
|DriverBinaryNames|VT_ARRAY 具有 VT_BSTR 的变体|聚合来自 UpperClassFilters、UpperFilters、LowerFilters、LowerClassFilters 和 Service 的所有数据。|
|枚举器|VT_BSTR|设备的枚举器的名称。  (SPDRP_ENUMERATOR_NAME) |
|排他|VT_I4|指示用户是否可以独占使用设备的数字。  (SPDRP_EXCLUSIVE) |
|筛选器|VT_ARRAY 具有 VT_BSTR 的变体|聚合来自 UpperClassFilters、UpperFilters、LowerFilters 和 LowerClassFilters 的所有数据。|
|FriendlyName|VT_BSTR|设备的友好名称。|
|HardwareIDs|VT_ARRAY 具有 VT_BSTR 的变体|为此设备定义的所有硬件 Id。|
|IsAttached|VT_BOOL|与 IsPhantom 属性相反的。 此关键字等效于 "IsPhantom = False"。|
|IsDisableable|VT_BOOL|从状态标志中提取 DN_DISABLEABLE 标志。 值 VARIANT_TRUE 表示设备声称可以禁用它。 此关键字等效于 "status&0x00002000"。|
|IsDisabled|VT_BOOL|检查 ProblemCode 属性中的 CM_PROB_DISABLED 值。 值 VARIANT_TRUE 表示设备已禁用，必须先启用，然后才能使用。 此关键字等效于 "ProblemCode = 0x00000016"。|
|IsFailedStart|VT_BOOL|检查 ProblemCode 标志以外的 CM_PROB_FAILED_START 标志。 值 VARIANT_TRUE 表示设备驱动程序启动失败。 此关键字等效于 "ProblemCode = 0x0000000A"。|
|IsFailedInstall|VT_BOOL|检查 ProblemCode 标志以外的 CM_PROB_FAILED_INSTALL 标志。 值 VARIANT_TRUE 表示设备驱动程序无法安装在设备上。 此关键字等效于 "ProblemCode = 0x0000001C"。|
|IsFiltered|VT_BOOL|从状态标志中提取 DN_FILTERED 标志。 此关键字等效于 "status&0x00000800"。|
|IsManual|VT_BOOL|从状态标志中提取 DN_MANUAL 标志。 此关键字等效于 "status&0x00000010"。|
|IsMoved|VT_BOOL|从状态标志中提取 DN_MOVED 标志。 此关键字等效于 "status&0x00001000"。|
|IsPhantom|VT_BOOL|值 VARIANT_TRUE 表示设备当前未插入到系统中或已卸载。|
|IsRebootNeeded|VT_BOOL|从状态标志中提取 DN_NEED_RESTART 标志。 值 VARIANT_TRUE 表示设备的共同安装程序声明需要重新启动计算机，设备才能完成删除或安装操作。 此关键字等效于 "status&0x00000100"。|
|IsReinstallNeeded|VT_BOOL|从 ConfigFlags 属性中提取 CONFIGFLAG_REINSTALL 标志。 值 VARIANT_TRUE 表示设备声称可删除它。 此关键字等效于 "ConfigFlags&0x00000020"。|
|IsRemovable|VT_BOOL|从状态标志中提取 DN_REMOVABLE 标志。 值 VARIANT_TRUE 表示设备声称可删除它。 此关键字等效于 "status&0x00004000"。|
|IsRemovePending|VT_BOOL|从状态标志中提取 DN_WILL_BE_REMOVED 标志。 此关键字等效于 "status&0x00040000"。|
|IsRootEnumerated|VT_BOOL|从状态标志中提取 DN_ROOT_ENUMERATED 标志。 值 VARIANT_TRUE 指示设备的父项为 RootDevice。 此关键字等效于 "status&0x00000001"。|
|IsStarted|VT_BOOL|从状态标志中提取 DN_STARTED 标志。 值 VARIANT_TRUE 指示当前已配置设备。 此关键字等效于 "status&0x00000008"。|
|LegacyBusType|VT_I4|旧的总线类型。|
|位置|VT_BSTR|有关设备的物理位置的详细信息。|
|LocationPaths|VT_ARRAY 具有 VT_BSTR 的变体|设备实例在设备树中的位置。|
|LowerClassFilters|VT_ARRAY 具有 VT_BSTR 的变体|作为目标设备上的较低类筛选器附加的每个驱动程序的服务名称。|
|LowerClassFiltersBinaryNames|VT_ARRAY 具有 VT_BSTR 的变体|设备目标的所有较低类筛选器驱动程序的二进制文件的名称。|
|LowerFilters|VT_ARRAY 具有 VT_BSTR 的变体|作为目标设备上的较低筛选器附加的每个驱动程序的服务名称。|
|LowerFiltersBinaryNames|VT_ARRAY 具有 VT_BSTR 的变体|设备目标的所有较低筛选器驱动程序的名称。|
|制造商|VT_BSTR|设备制造商。|
|PDO|VT_BSTR|内核中的物理设备对象的名称。|
|ProblemCode|VT_I4|设备的问题代码。 在 Cfg 中定义的其中一个 CM_PROB_ 前缀的问题值。|
|ProblemCodeString|VT_BSTR|ProblemCode 的字符串表示形式。|
|RemovalPolicy|VT_I4|设备的当前删除策略。  (SPDRP_REMOVAL_POLICY) |
|RemovalPolicyHWDefault|VT_I4|硬件-已指定设备的默认删除策略。  (SPDRP_REMOVAL_POLICY_HW_DEFAULT) |
|RemovalPolicyOverride|VT_I4|覆盖) 设备的删除策略 (。  (SPDRP_REMOVAL_POLICY_OVERRIDE) |
|服务|VT_BSTR|设备的驱动程序的服务名称。|
|ServiceBinaryName|VT_BSTR|设备目标的函数驱动程序的名称。|
|状态|VT_I4|设备的状态标志。|
|StatusString|VT_BSTR|设备状态字符串。|
|SymbolicLink|VT_BSTR|可用于通过使用 Microsoft Win32 CreateFile 方法打开设备的名称。 不能以这种方式使用所有设备。 大多数具有可编程接口的设备都有可用的 SymbolicLink。|
|UIFormat|VT_BSTR|用于显示 UINumber 值的字符串。  (SPDRP_UI_NUMBER_DESC_FORMAT) |
|UINumber|VT_I4|设备的 UINumber。|
|UpperClassFilters|VT_ARRAY 具有 VT_BSTR 的变体|在目标设备上作为上层类筛选器附加的每个驱动程序的服务名称。|
|UpperClassFiltersBinaryNames|VT_ARRAY 具有 VT_BSTR 的变体|设备目标的所有高级类筛选器驱动程序的二进制文件的名称。|
|UpperFilters|VT_ARRAY 具有 VT_BSTR 的变体|作为目标设备上的上限筛选器附加的每个驱动程序的服务名称。||
|UpperFiltersBinaryNames|VT_ARRAY 具有 VT_BSTR 的变体|设备目标的所有上限筛选器驱动程序的名称|

## <a name="root-keywords-for-a-system-target"></a>系统目标的根关键字

下表描述了根命名空间中仅对系统类型目标有效的属性。

|关键字|VARIANT 类型|描述|
|----|----|----|
|IsPhantom|VT_BOOL|指定当前是否可以使用系统。|
|IsRemote|VT_BOOL|指定目标是否为远程系统。|
|PageSize|VT_I4|目标系统硬件的页面大小。|
|ProcArch|VT_BSTR|目标系统硬件的处理器体系结构。 此字段可以包含 "x86"、"IA64" 或 "x64"。|
|OSMajorVersion|VT_I4|指定操作系统的主版本号。|
|OSMinorVersion|VT_I4|指定操作系统的次版本号。|

## <a name="disk-namespace-keywords"></a>磁盘命名空间关键字

下表描述了仅对磁盘设备有效的磁盘命名空间中的属性。

>[!NOTE]
>磁盘命名空间中的大多数属性都是通过 IOCTL 从操作系统检索到磁盘本身。 有关详细信息，请参阅 [STORAGE_DEVICE_DESCRIPTOR](/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_device_descriptor)。

|关键字|VARIANT 类型|描述|
|----|----|----|
|BusType|VT_I4|STORAGE_DEVICE_DESCRIPTOR。BusType 字段。|
|DeviceType|VT_I4|STORAGE_DEVICE_DESCRIPTOR。DeviceTypeModifier 字段。|
|IsRemovable|VT_BOOL|指定设备是否包含可移动介质。|
|IsCommandQueuing|VT_BOOL|STORAGE_DEVICE_DESCRIPTOR CommandQueueing 字段。|
|数字|VT_UI4|磁盘编号 (可能与地址字段) 相同。|
|ProductID|VT_BSTR|产品标识符。|
|ProductRev|VT_BSTR|产品修订值。|
|SerialNumber|VT_BSTR|序列号。|
|大小|VT_I8|磁盘的总大小（以字节为单位）。|
|VendorID|VT_BSTR|供应商标识符。|

## <a name="volume-namespace-keywords"></a>卷命名空间关键字

下表描述了只对卷设备有效的卷命名空间中的属性。

|关键字|VARIANT 类型|描述|
|----|----|----|
|启动|VT_BOOL|确定卷是否为启动分区。 值 VARIANT_TRUE 表示该卷是启动分区。 启动分区是包含 Windows 操作系统文件的分区。|
|DeviceName|VT_BSTR|此卷的 MS-DOS 设备名称的当前映射。|
|磁盘|VT_BSTR|此卷的 MS-DOS 设备名称的当前映射。|
|DriveLetter|VT_BSTR|卷的驱动器号，包括尾随斜杠 (\\) 。|
|ExtentCount|VT_I4|卷扩展的磁盘数。|
|ExtentDiskNumbers|VT_ARRAY 具有 VT_I4 的变体|一个数组，其中包含卷所扩展到的每个 Disk：： Number 值。 数组具有 ExtentCount 的元素，且为0索引。 数组与另一个区区 * 数组具有相同的排序顺序。|
|ExtentLengths|VT_ARRAY 具有 VT_I8 的变体|一个数组，该数组包含卷扩展到的每个单独范围的长度。 数组具有 ExtentCount 的元素，且为0索引。 数组与另一个区区 * 数组具有相同的排序顺序。|
|ExtentOffsets|VT_ARRAY 具有 VT_I8 的变体|一个数组，该数组包含卷扩展到的每个单独范围的起始偏移量。 数组具有 ExtentCount 的元素，且为0索引。 数组与另一个区区 * 数组具有相同的排序顺序。|
|FileSystem|VT_BSTR|卷的文件系统的名称。  (GetVolumeInformation) |
|FreeSize|VT_I8|卷上的可用空间总量（以字节为单位）。|
|GBFreeSize|VT_I4|e 用户可用的磁盘上的可用 gb (GB) 总数。|
|GBTotalSize|VT_I4|可供用户使用的卷上的 gb (GB) 总数。|
|HasFiles|VT_BOOL|确定卷上是否有文件。 值 VARIANT_TRUE 指示卷上有文件。|
|IsMediaPresent|VT_BOOL|确定卷是否存在介质。 值 VARIANT_TRUE 指示卷上有介质。|
|IsMediaRemovable|VT_BOOL|确定卷媒体是否可移动。 值为 VARIANT_TRUE 指示卷媒体是可移动的。|
|Label|VT_BSTR|卷标。  (GetVolumeInformation) |
|MBFreeSize|VT_I8|可供用户使用的磁盘上的可用兆字节 (MB) 总数。|
|MBTotalSize|VT_I8|可供用户使用的卷上的兆字节 (MB) 总数。  (GetDiskFreeSpaceEx) |
|MountPaths|VT_BSTR|此卷的所有装载路径。|
|PagePath|VT_BOOL|确定卷是否包含活动的页面文件。 值 VARIANT_TRUE 指示卷包含一个活动的页面文件。|
|SerialNumber|VT_I4|卷的序列号。|
|系统|VT_BOOL|确定卷是否为系统分区。 值 VARIANT_TRUE 指示卷包含 Windows 系统分区。 系统分区包含与硬件相关的文件 (可启动代码) ，可启动 Windows 启动管理器 (bootmgr) 。|
|TotalSize|VT_I8|卷的总大小（以字节为单位）。|
|类型|VT_I4|从 Getdrivetype 功能 (驱动器号) 返回的值。 有关详细信息，请参阅 MSDN Library 中的 Getdrivetype 功能。|

## <a name="power-namespace-keywords"></a>Power 命名空间关键字

下表描述了仅对电源设备有效的 Power 命名空间中的属性。

|关键字|VARIANT 类型|描述|
|----|----|----|
|SupportedDeviceUnits|VT_ARRAY 具有 VT_BSTR 的变体|可用于查询的 PowerUnit 命名空间数组。|

## <a name="powerdevice-powercomponentx-powerprocessor-and-powersoc-namespace-keywords"></a>PowerDevice、PowerComponentX、PowerProcessor 和 PowerSoC 命名空间关键字

下表描述了各种 PowerUnit 命名空间中的属性。

|关键字|VARIANT 类型|描述|
|----|----|----|
|SupportedStates|VT_ARRAY 具有 VT_BSTR 的变体|电源状态的命名空间数组 (C0 – C6，D0 – D3，F0 – F9，SWIS0 – SWIS3) |
|CoveredStates|VT_ARRAY 具有 VT_BSTR 的变体|涵盖状态的命名空间数组。 仅包括具有非零命中计数的状态|

## <a name="powerprocessorcx-powerdevicedx-powercomponentxfy-powersocswisx-namespace-keywords"></a>PowerProcessorCX、PowerDeviceDX、PowerComponentXFY、PowerSoCSWISX 命名空间关键字

下表描述了各种 PowerState 命名空间中的属性。

|关键字|VARIANT 类型|描述|
|----|----|----|
|点击次数|VT_UI4|在测试期间输入给定电源状态的次数。|
|持续时间|VT_UI4|给定电源状态所用的时间段（以毫秒为单位）。|
|百分比|VT_UI4|给定电源状态所用的时间百分比。|

## <a name="interface-namespace-keywords"></a>接口命名空间关键字

下表描述了各种接口命名空间中的属性。

|关键字|VARIANT 类型|说明|
|----|----|----|
|全部|VT_BSTR|单个设备支持的所有设备接口 GUID 的所有设备接口。|
|卷|VT_BSTR|GUID_DEVINTERFACE_VOLUME GUID 的接口。|
|DISK|VT_BSTR|GUID_DEVINTERFACE_DISK GUID 的接口。|
|CDROM|VT_BSTR|GUID_DEVINTERFACE_CDROM GUID 的接口。|
|GUID|VT_BSTR|单个接口 GUID 的接口。|

## <a name="cap-namespace-keywords"></a>CAP 命名空间关键字

下表描述了各种 CAP (功能) 命名空间的属性。

|关键字|VARIANT 类型|描述|
|----|----|----|
|LockSupported|VT_BOOL|指定设备是否支持阻止设备弹出的物理设备锁定。  (CM_DEVCAP_LOCKSUPPORTED) |
|EjectSupported|VT_BOOL|指定当系统处于 PowerSystemWorking 状态时，设备是否支持软件控制的设备弹出。  (CM_DEVCAP_EJECTSUPPORTED) |
|可移动|VT_BOOL|指定是否可以从其直接父项动态删除设备。  (CM_DEVCAP_REMOVABLE) |
|DockDevice|VT_BOOL|指定设备是否为插接外设。  (CM_DEVCAP_DOCKDEVICE) |
|UniqueId|VT_BOOL|指定设备的实例 ID 在整个系统范围内是否唯一。  (CM_DEVCAP_UNIQUEID) |
|SilentInstall|VT_BOOL|指定设备管理器是否应禁止显示所有安装对话框。  (CM_DEVCAP_SILENTINSTALL) |
|RawDeviceOK|VT_BOOL|指定基础总线的驱动程序是否可以在没有功能驱动程序的情况驱动器上驱动设备。  (CM_DEVCAP_RAWDEVICEOK) |
|SurpriseRemovalOK|VT_BOOL|指定设备的函数驱动程序是否可以处理在 Windows 可以向其发送 IRP_MN_QUERY_REMOVE_DEVICE 之前删除设备的情况。  (CM_DEVCAP_SURPRISEREMOVALOK) |
|HardwareDisabled|VT_BOOL|指定设备的硬件是否被禁用。  (CM_DEVCAP_HARDWAREDISABLED) |
|非动态|VT_BOOL|留待将来使用。  (CM_DEVCAP_NONDYNAMIC) |

## <a name="inf-namespace-keywords"></a>INF 命名空间关键字

下表描述了各种 INF 命名空间中的属性。

|关键字|VARIANT 类型|描述|
|----|----|----|
|FileName|VT_BSTR|INF 文件名。|
|FileNamePath|VT_BSTR|INF 文件名路径。|
|SectionName|VT_BSTR|INF 部分名称。|
|Date|VT_BSTR|INF 日期。|
|OriginalInfFileName|VT_BSTR|原始 INF 文件名。|

## <a name="net-namespace-keywords"></a>NET 命名空间关键字

下表描述了各种网络命名空间中的属性。

|关键字|VARIANT 类型|描述|
|----|----|----|
|AdapterName|VT_BSTR|IP_ADAPTER_ADDRESSES 结构中的 AdapterName 字段。|
|IPV6Address|VT_BSTR|IP_ADAPTER_ADDRESSES 结构中的 FirstUnicastAddress 字段。|
|FirstAnycastAddress|VT_BSTR|IP_ADAPTER_ADDRESSES 结构中的 FirstAnycastAddress 字段。|
|FirstMulticastAddress|VT_BSTR|IP_ADAPTER_ADDRESSES 结构中的 FirstMulticastAddress 字段。|
|FirstDnsServerAddress|VT_BSTR|IP_ADAPTER_ADDRESSES 结构中的 FirstDnsServerAddress 字段。|
|FirstPrefix|VT_BSTR|IP_ADAPTER_ADDRESSES 结构中的 FirstPrefix 字段。|
|PrimaryWINSServer|VT_BSTR|IP_ADAPTER_ADDRESSES 结构中的 FirstWinsServerAddress 字段。|
|FirstGatewayAddress|VT_BSTR|IP_ADAPTER_ADDRESSES 结构中的 FirstGatewayAddress 字段。|
|ConnectionSpecificDNSSuffix|VT_BSTR|IP_ADAPTER_ADDRESSES 结构中的 DnsSuffix 字段|
|描述|VT_BSTR|IP_ADAPTER_ADDRESSES 结构中的说明字段。|
|FriendlyName|VT_BSTR|IP_ADAPTER_ADDRESSES 结构中的 FriendlyName 字段。|
|PhysicalAddress|VT_BSTR|IP_ADAPTER_ADDRESSES 结构中的 MacAddress 字段|
|Flags|VT_UI4|IP_ADAPTER_ADDRESSES 结构中的标志字段|
|单位|VT_UI4|IP_ADAPTER_ADDRESSES 结构中的 Mtu 字段。|
|IfType|VT_UI4|IP_ADAPTER_ADDRESSES 结构中的 IfType 字段。|
|OperStatus|VT_UI4|IP_ADAPTER_ADDRESSES 结构中的 OperStatus 字段|
|OperationalStatusString|VT_BSTR|与 IP_ADAPTER_ADDRESSES 结构中的 OperStatus 字段等效的字符串|
|Ipv6IfIndex|VT_UI4|IP_ADAPTER_ADDRESSES 结构中的 Ipv6IfIndex 字段|
|TransmitLinkSpeedMbps|VT_UI4|IP_ADAPTER_ADDRESSES 结构中的 TransmitLinkSpeedGpbs 字段。|
|ReceiveLinkSpeedMbps|VT_UI4|IP_ADAPTER_ADDRESSES 结构中的 ReceiveLinkSpeedMbps 字段。|
|Ipv4Metric|VT_UI4|IP_ADAPTER_ADDRESSES 结构中的 Ipv4Metric 字段。|
|Ipv6Metric|VT_UI4|IP_ADAPTER_ADDRESSES 结构中的 Ipv6Metric 字段。|
|DHCPServer|VT_BSTR|IP_ADAPTER_ADDRESSES 结构中的 Dhcpv4Server 字段。|
|CompartmentId|VT_UI4|IP_ADAPTER_ADDRESSES 结构中的 CompartmentId 字段。|
|NetworkGuid|VT_BSTR|IP_ADAPTER_ADDRESSES 结构中的 NetworkGuid 字段。|
|ConnectionType|VT_UI4|IP_ADAPTER_ADDRESSES 结构中的 ConnectionType 字段。|
|TunnelType|VT_UI4|IP_ADAPTER_ADDRESSES 结构中的 TunnelType 字段。|
|Dhcpv6ClientDuidLength|VT_UI4|IP_ADAPTER_ADDRESSES 结构中的 Dhcpv6ClientDuidLength 字段。|
|Dhcpv6Iaid|VT_UI4|IP_ADAPTER_ADDRESSES 结构中的 Dhcpv6Iaid 字段。|
|IsOperational|VT_BOOL|是否可操作。|
|PhysicalMediaType|VT_UI4|网络设备的物理媒体类型。|
|MediaType|VT_UI4|网络设备的物理媒体类型。|

## <a name="opticalmedia-namespace-keywords"></a>OpticalMedia 命名空间关键字

下表描述了各种 OpticalMedia 命名空间中的属性。

|关键字|VARIANT 类型|描述|
|----|----|----|
|IsMediaPresent|VT_BOOL|如果介质存在或不在光学媒体设备中。|
|类型|VT_UI4|从 IOCTL_CDROM_GET_CONFIGURATION GET_CONFIGURATION_HEADER 中返回的当前配置文件类型号。|
|ClassTypeString|VT_BSTR|光学媒体类的类型。|
|TypeString|VT_BSTR|光学媒体的类型。|

## <a name="storagemedia-namespace-keywords"></a>StorageMedia 命名空间关键字

下表描述了各种 StorageMedia 命名空间中的属性。

|关键字|VARIANT 类型|描述|
|----|----|----|
|DeviceType|VT_UI4|指定一个系统定义的 FILE_DEVICE_XXX 常数，表示设备的类型。|
|DeviceTypeString|VT_BSTR|设备类型关联的字符串。|
|计数|VT_UI4|包含 Mediainfo.xml 中的 DEVICE_MEDIA_INFO 结构的数目。|
|SupportedTypes|VT_UI4|指定所有 MEDIA_TYPE 或 STORAGE_MEDIA_TYPE 值，该值指示可移动磁盘的类型。|
|有效|VT_BOOL|如果此设备的 gatherer 包含有效数据，则为。|

## <a name="windows-namespace-keywords"></a>Windows 命名空间关键字

下表描述了各种 Windows 命名空间中的属性。

|关键字|VARIANT 类型|描述|
|----|----|----|
|IsDriverVerifierEnabled|VT_BOOL|如果为 True 或 False，则指示是否已对此设备的所有驱动程序启用至少具有标准设置的驱动程序验证程序。|
|IsKernelDebugDevice|VT_BOOL|True 或 False，指示内核调试器是否正在使用此设备。|
