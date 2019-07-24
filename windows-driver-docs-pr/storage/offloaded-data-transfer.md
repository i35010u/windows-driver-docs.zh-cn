---
title: 卸载了数据传输
description: 卸载了数据传输
appliesto:
- Windows Server 2019
- Windows Server 2016
ms.assetid: EDFA6AFB-7D14-44F8-A105-E74182D26398
ms.date: 07/19/2019
ms.localizationpriority: medium
ms.openlocfilehash: 95d9f5311a5a67f8883ad992bf1954dfc6f8926f
ms.sourcegitcommit: 69261fa09a48b70a681bec0b4cf7afa8b84c73b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68415098"
---
# <a name="offloaded-data-transfer"></a>卸载了数据传输


## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概述


卸载的数据传输 (ODX) 引入了一个标记化操作, 用于在存储设备上移动数据。 源文件和目标文件可以在同一卷上, 也可以在同一台计算机上托管两个不同的卷, 本地卷和远程卷通过 SMB2, 或者通过 SMB2 在两个不同的计算机上有两个卷。 Windows 8 中引入了卸载数据传输。

下面是使用 ODX 的复制卸载操作的过程。

1.  复制卸载应用程序将卸载读取请求发送到源存储设备的复制管理器。
2.  应用程序将接收卸载读取结果请求发送到复制管理器, 并返回令牌。 标记是要复制的数据的表示形式。
3.  应用程序将带有令牌的卸载写入请求发送到目标存储设备的复制管理器。
4.  应用程序将接收卸载写入结果请求发送到复制管理器。 复制管理器将数据从源移动到目标, 并将卸载写入结果返回到应用程序。

## <a name="span-ididentifyanodx-capablesourceanddestinationspanspan-ididentifyanodx-capablesourceanddestinationspanspan-ididentifyanodx-capablesourceanddestinationspanidentify-an-odx-capable-source-and-destination"></a><span id="Identify_an_ODX-Capable_Source_and_Destination"></span><span id="identify_an_odx-capable_source_and_destination"></span><span id="IDENTIFY_AN_ODX-CAPABLE_SOURCE_AND_DESTINATION"></span>标识支持 ODX 的源和目标


为了支持 ODX, 存储阵列必须实现相关的 T10 标准规范。 标识为 ODX 的存储阵列、卸载的读取和写入操作以及具有众所周知令牌的卸载写入。 LUN 设备枚举期间 (系统启动或即插即用事件)。 Windows 通过以下步骤收集或更新存储目标设备的 ODX 功能信息。

1.  查询复制卸载功能。
2.  收集复制卸载操作所需的参数和限制。

默认情况下, 如果源和目标 Lun 都支持 ODX, 则 Windows 首先会尝试使用 ODX 路径进行复制操作。 如果存储设备未通过初始 ODX 请求, 则 Windows 会将源和目标 LUN 的组合标记为 "不能 ODX 的" 路径。

## <a name="span-idodxreadwriteoperationsspanspan-idodxreadwriteoperationsspanspan-idodxreadwriteoperationsspanodx-readwrite-operations"></a><span id="ODX_Read_Write_Operations"></span><span id="odx_read_write_operations"></span><span id="ODX_READ_WRITE_OPERATIONS"></span>ODX 读/写操作


### <a name="span-idsynchronouscommandadoptionandapisspanspan-idsynchronouscommandadoptionandapisspanspan-idsynchronouscommandadoptionandapisspansynchronous-command-adoption-and-apis"></a><span id="Synchronous_Command_Adoption_and_APIs"></span><span id="synchronous_command_adoption_and_apis"></span><span id="SYNCHRONOUS_COMMAND_ADOPTION_AND_APIS"></span>同步命令采用和 Api

Windows 同步卸载的读取和写入操作。 使用以下算法拆分大型卸载写入请求, 以确保可靠的同步卸载写入。

-   如果目标存储设备未提供最佳传输大小, 请将最佳传输大小设置为 64 MB。
-   存储目标设备指定的最佳传输大小-最佳传输大小大于零且小于 256 MB。
-   如果目标设备设置的最佳传输大小大于 256 MB, 则将最佳传输大小设置为 256 MB。

同步卸载读取和卸载写入 SCSI 命令降低了 MPIO 和群集故障转移方案的复杂性。 Windows 要求副本管理器在4秒内完成同步卸载读取/写入 SCSI 命令。

应用程序可以通过 api 使用 FSCTL、DSM IOCTL\_或\_SCSI PASS 来与存储阵列交互, 并执行复制卸载操作。 若要避免数据损坏或系统不稳定, Windows 会将应用程序限制为直接写入到文件系统装入的卷, 而无需首先获取对卷的独占访问权限。 这是由于对卷的写入可能与文件系统写入操作发生冲突的情况。 发生此类冲突时, 卷的内容可能处于不一致状态。

### <a name="span-idoffloadreadoperationsspanspan-idoffloadreadoperationsspanspan-idoffloadreadoperationsspanoffload-read-operations"></a><span id="Offload_Read_Operations"></span><span id="offload_read_operations"></span><span id="OFFLOAD_READ_OPERATIONS"></span>卸载读取操作

应用程序的卸载读取请求可以指定令牌生存期 (非活动超时)。 如果应用程序将令牌生存期设置为零, 则默认的非活动计时器将用作令牌生存期。 存储阵列的复制管理器根据令牌的非活动超时值和凭据来维护和验证令牌。 Windows 主机还将文件碎片数限制为64。 如果卸载读取请求包含64个以上的片段, 则 Windows 将无法进行复制卸载请求, 并回退到传统的复制操作。

完成卸载读取请求后, 复制管理器将准备接收卸载读取结果命令的数据 (杆) 标记的表示形式。 "杆标记" 字段指定用户数据和保护信息的时间点表示形式。 杆可以是 "以独占方式打开" 或 "以共享方式打开" 格式的用户数据。 复制管理器可能会根据令牌的 "杆" 策略设置使令牌失效。 如果对复制卸载操作仅打开了杆, 则在修改或移动杆时, 杆令牌可能会失效。 如果杆处于 "以共享方式打开" 格式, 则在修改杆后, 杆标记仍有效。

| 大小 (字节) | 令牌内容 |
|---------------|----------------|
| 4             | 杆标记类型 |
| 508           | 杆标记 ID   |

 

由于杆令牌仅被存储阵列授予并使用, 因此它的格式是不透明的、唯一的和高度安全的。 如果令牌已修改、未验证或已过期, 则复制管理器可能会在卸载写入操作过程中使令牌失效。 从卸载读取操作返回的杆令牌具有非活动的超时值, 以指示复制管理器必须使用令牌使用情况来使令牌对下一次写入有效。

### <a name="span-idoffloadwriteoperationsspanspan-idoffloadwriteoperationsspanspan-idoffloadwriteoperationsspanoffload-write-operations"></a><span id="Offload_Write_Operations"></span><span id="offload_write_operations"></span><span id="OFFLOAD_WRITE_OPERATIONS"></span>卸载写入操作

从复制管理器接收杆令牌后, 应用程序将带有杆令牌的卸载写入请求发送到存储阵列的复制管理器。 将同步卸载写入命令发送到目标设备后, Windows 要求副本管理器在4秒内完成该命令。 如果命令由于命令超时或其他错误条件而终止, Windows 将无法执行该命令。 根据返回的状态代码, 应用程序将回退到旧的复制操作。

可以通过一个或多个接收卸载写入结果命令来完成卸载写入请求。 如果卸载写入已部分完成, 则复制管理器将返回, 并显示估计的延迟时间和传输计数以指示复制进度。 传输计数的数目指定从源到目标媒体写入时不会发生错误的连续逻辑块的数量。 复制管理器可以按顺序或分散/收集模式执行卸载写入。

发生写入失败时, 复制进度会将从第一个逻辑块到故障块的连续逻辑块计数。 客户端应用程序或复制引擎从写入失败块恢复卸载写入。 完成卸载写入后, 复制管理器将完成 "接收杆令牌信息" 命令, 并将 "估计状态更新延迟" 设置为 "零", 并将数据传输计数的进度设置为 100%。 如果接收卸载写入结果返回相同的数据传输计数进度, 则在四次重试后, Windows 将无法将复制操作返回到应用程序。

客户端应用程序还可以使用众所周知的杆令牌执行卸载写入操作。 这是具有已知的数据模式和标记格式的预定义杆标记。 一个常见的实现称为零标记。 客户端应用程序可以使用零标记来使用零填充一个或多个逻辑块范围。 如果已知令牌不受支持或无法识别, 则复制管理器会将卸载写入请求失败并带有 "令牌无效"。

| 大小 (字节) | 令牌内容     |
|---------------|--------------------|
| 4             | 杆标记类型     |
| 2             | 众所周知的模式 |
| 506           | 杆标记 ID       |

 

在具有已知杆令牌的卸载程序中, 客户端应用程序不能使用卸载读取来请求众所周知的令牌。 复制管理器根据其自己的策略验证并维护知名的杆令牌。

### <a name="span-idperformancetuningparametersofodximplementationspanspan-idperformancetuningparametersofodximplementationspanspan-idperformancetuningparametersofodximplementationspanperformance-tuning-parameters-of-odx-implementation"></a><span id="Performance_Tuning_Parameters_of_ODX_Implementation"></span><span id="performance_tuning_parameters_of_odx_implementation"></span><span id="PERFORMANCE_TUNING_PARAMETERS_OF_ODX_IMPLEMENTATION"></span>ODX 实现的性能优化参数

ODX 的性能不依赖于客户端-服务器网络或服务器与存储阵列之间的 SAN 的传输链接速度。 数据由复制管理器和存储阵列的设备服务器移动。

并非每个复制卸载都有 ODX 技术的优势。 例如, 1 Gb iSCSI 存储阵列的复制管理器可以在10秒内完成 3 GB 文件复制, 并且数据传输速率将大于 300 MB/秒。 数据传输速率已经超出了 1 Gb 以太网接口的最大理论传输速度。

并非每个文件大小的复制卸载都可以获得 Windows ODX 技术的优势。 对于特定大小的文件, 复制性能可能无法从 ODX 技术受益。 若要优化性能, 可将 ODX 的使用限制为允许的最小文件大小和最大副本长度。 若要优化 ODX 的性能, 请调整以下参数。

Windows 设置复制卸载操作的最小文件大小要求。 目前, 复制引擎的最小复制卸载文件大小设置为 256 KB。 如果文件小于 256 KB, 复制引擎将回退到旧的复制过程。

Windows 主机使用最大令牌传输大小和最佳传输计数来准备卸载读取或写入 SCSI 命令的最佳传输大小。 块数量中的总传输大小不得超过最大令牌传输大小。 如果存储阵列未报告最佳传输计数, Windows 将使用 64 MB 作为默认计数。

最佳和最大传输长度参数指定一个范围描述符中的最佳和最大块数。 复制卸载应用程序可以遵循这些参数来实现最佳文件传输性能。

## <a name="span-idodxerrorhandlingandhighavailabilitysupportspanspan-idodxerrorhandlingandhighavailabilitysupportspanspan-idodxerrorhandlingandhighavailabilitysupportspanodx-error-handling-and-high-availability-support"></a><span id="ODX_Error_Handling_and_High_Availability_Support"></span><span id="odx_error_handling_and_high_availability_support"></span><span id="ODX_ERROR_HANDLING_AND_HIGH_AVAILABILITY_SUPPORT"></span>ODX 错误处理和高可用性支持


当 ODX 操作对文件复制请求失败时, 复制引擎和 Windows 文件系统 (NTFS) 将回退到旧的复制操作。 如果在卸载写入操作过程中复制卸载失败, 则复制引擎和 NTFS 将从卸载写入中的第一个故障点恢复为旧的复制操作。

下面是使用 ODX 的复制卸载操作的算法。

### <a name="span-idodxerrorhandlingspanspan-idodxerrorhandlingspanspan-idodxerrorhandlingspanodx-error-handling"></a><span id="ODX_Error_Handling"></span><span id="odx_error_handling"></span><span id="ODX_ERROR_HANDLING"></span>ODX 错误处理

ODX 根据存储阵列的功能使用稳健的错误处理算法。 如果在支持 ODX 的路径中复制卸载失败, 则 Windows 主机会要求应用程序回退到旧的复制操作。 此时, Windows 复制引擎已经实现了 "回退到传统副本" 机制。 复制卸载失败后, NTFS 会将源和目标 LUN 标记为不支持 ODX 的时间为三分钟。 经过此时间段后, Windows 复制引擎会重试 ODX 操作。 在高度压力情况下, 存储阵列可以使用此功能在某些路径中暂时禁用 ODX 支持。

### <a name="span-idodxfailoverinmpioandclusterserverconfigurationsspanspan-idodxfailoverinmpioandclusterserverconfigurationsspanspan-idodxfailoverinmpioandclusterserverconfigurationsspanodx-failover-in-mpio-and-cluster-server-configurations"></a><span id="ODX_Failover_in_MPIO_and_Cluster_Server_Configurations"></span><span id="odx_failover_in_mpio_and_cluster_server_configurations"></span><span id="ODX_FAILOVER_IN_MPIO_AND_CLUSTER_SERVER_CONFIGURATIONS"></span>MPIO 和群集服务器配置中的 ODX 故障转移

必须在同一存储链接 (I\_T 结点) 中完成或取消对卸载的读取和写入操作。

当在同步卸载读取或写入操作过程中发生 MPIO 或群集服务器故障转移时, Windows 将使用以下算法处理故障转移。

1.  同步卸载读取/写入命令。
2.  通过 MPIO 配置-Windows 在 MPIO 路径故障转移后重试失败的命令。 如果命令再次失败, 则 Windows 将执行以下操作。
    -   无需群集服务器故障转移选项– Windows 会向存储设备发出 LUN 重置, 并向应用程序返回 i/o 故障状态。
    -   利用群集服务器故障转移选项– Windows 将启动群集服务器节点故障转移。

3.  对于群集服务器配置, 群集存储服务将故障转移到下一个首选群集节点, 然后恢复群集存储服务。 卸载应用程序必须能够识别群集, 才能在群集存储服务故障转移后重试卸载读/写命令。

如果卸载读取或写入命令在 MPIO 路径和群集节点故障转移后失败, 则 Windows 将在故障转移后向存储设备发出 LUN 重置。 存储设备在 LUN 下终止所有未完成的命令和挂起的操作。

目前, Windows 不会发出异步卸载从存储堆栈读取或写入 SCSI 命令的功能。

## <a name="span-idodxusagemodelsspanspan-idodxusagemodelsspanspan-idodxusagemodelsspanodx-usage-models"></a><span id="ODX_Usage_Models"></span><span id="odx_usage_models"></span><span id="ODX_USAGE_MODELS"></span>ODX 使用模型


### <a name="span-idodxacrossphysicaldiskvirtualharddiskandsmbshareddiskspanspan-idodxacrossphysicaldiskvirtualharddiskandsmbshareddiskspanspan-idodxacrossphysicaldiskvirtualharddiskandsmbshareddiskspanodx-across-physical-disk-virtual-hard-disk-and-smb-shared-disk"></a><span id="ODX_across_Physical_Disk__Virtual_Hard_Disk_and_SMB_Shared_Disk"></span><span id="odx_across_physical_disk__virtual_hard_disk_and_smb_shared_disk"></span><span id="ODX_ACROSS_PHYSICAL_DISK__VIRTUAL_HARD_DISK_AND_SMB_SHARED_DISK"></span>跨物理磁盘、虚拟硬盘和 SMB 共享磁盘的 ODX

若要执行 ODX 操作, 应用程序服务器必须能够访问具有读/写权限的源 LUN 和目标 LUN。 复制卸载应用程序向源 LUN 发出卸载读取请求, 并从源 LUN 的复制管理器接收令牌。 复制卸载应用程序使用该令牌向目标 LUN 发出卸载写入请求。 然后, 复制管理器通过存储网络将数据从源 LUN 移动到目标 LUN。

### <a name="span-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanodx-operation-with-one-server"></a><span id="ODX_Operation_with_One_Server"></span><span id="odx_operation_with_one_server"></span><span id="ODX_OPERATION_WITH_ONE_SERVER"></span>包含一台服务器的 ODX 操作

在单服务器配置中, 复制卸载应用程序会发出来自同一服务器系统的卸载读写请求。

### <a name="span-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanodx-operation-with-one-server"></a><span id="ODX_Operation_with_One_Server"></span><span id="odx_operation_with_one_server"></span><span id="ODX_OPERATION_WITH_ONE_SERVER"></span>包含一台服务器的 ODX 操作

在单服务器配置中, 复制卸载应用程序会发出来自同一服务器系统的卸载读写请求。

在上图中, Server1 或 Virtual Machine1 具有对源 LUN (VHD1 或物理 Disk1) 和目标 LUN (VHD2 或物理 Disk2) 的访问权限。 复制卸载应用程序向源 LUN 发出卸载读取请求, 并从源 LUN 接收令牌, 然后复制卸载应用程序使用该令牌向目标 LUN 发出卸载写入请求。 复制管理器将源 LUN 中的数据移至同一存储阵列中的目标 LUN。

### <a name="span-idodxoperationwithtwoserversspanspan-idodxoperationwithtwoserversspanspan-idodxoperationwithtwoserversspanodx-operation-with-two-servers"></a><span id="ODX_Operation_with_Two_Servers"></span><span id="odx_operation_with_two_servers"></span><span id="ODX_OPERATION_WITH_TWO_SERVERS"></span>具有两个服务器的 ODX 操作

在双服务器配置中, 有两个服务器和多个存储阵列由同一个复制管理器管理。

-   Server1 或 Virtual Machine1 是源 LUN 的主机, Server2 或 Virtual Machine2 是目标 LUN 的主机。 Server1 通过 SMB 协议与应用程序客户端共享源 LUN, Server2 还通过 SMB 协议与应用程序客户端共享目标 LUN。 应用程序客户端可以访问源 LUN 和目标 LUN。
-   源和目标存储阵列由 SAN 配置中的同一复制管理器进行管理。
-   在应用程序客户端系统中, 复制卸载应用程序向源 LUN 发出卸载读取请求, 并从源 LUN 接收令牌, 然后使用令牌向目标 LUN 发出卸载写入请求。 复制管理器跨两个不同位置的两个不同存储阵列将数据从源 LUN 移动到目标 LUN。

### <a name="span-idmassivedatamigrationspanspan-idmassivedatamigrationspanspan-idmassivedatamigrationspanmassive-data-migration"></a><span id="Massive_Data_Migration"></span><span id="massive_data_migration"></span><span id="MASSIVE_DATA_MIGRATION"></span>大规模数据迁移

大规模数据迁移是将大量数据 (如数据库记录、电子表格、文本文件、扫描的文档和图像) 导入到新系统的过程。 数据迁移可能是由存储系统升级、新的数据库引擎或应用程序或业务流程中的更改引起的。 如果旧存储系统可以由新存储系统的复制管理器进行管理, 则可以使用 ODX 将数据从旧的存储系统迁移到新的存储系统。

-   Server1 是旧存储系统的主机, Server2 是新存储系统的主机。 Server1 通过 SMB 协议将源 LUN 作为数据迁移应用程序客户端进行共享, 并且 Server2 通过 SMB 协议共享目标 LUN 作为数据迁移应用程序客户端。 应用程序客户端可以访问源 LUN 和目标 LUN。
-   旧式存储系统和新存储系统由 SAN 配置中的同一复制管理器进行管理。
-   在数据迁移应用程序客户端系统中, 复制卸载应用程序向源 LUN 发出卸载读取请求, 并从源 LUN 接收令牌, 然后向目标 LUN 发出带有令牌的卸载写入请求。 在两个不同的存储系统上, 复制管理器将源 LUN 中的数据移动到目标 LUN。
-   也可以在同一位置的一台服务器上操作大规模数据迁移。

### <a name="span-idhost-controlleddatatransferwithinatieredstoragedevicespanspan-idhost-controlleddatatransferwithinatieredstoragedevicespanspan-idhost-controlleddatatransferwithinatieredstoragedevicespanhost-controlled-data-transfer-within-a-tiered-storage-device"></a><span id="Host-Controlled_Data_Transfer_within_a_Tiered_Storage_Device"></span><span id="host-controlled_data_transfer_within_a_tiered_storage_device"></span><span id="HOST-CONTROLLED_DATA_TRANSFER_WITHIN_A_TIERED_STORAGE_DEVICE"></span>分层存储设备中受主机控制的数据传输

分层存储设备将数据分类为不同类型的存储媒体, 以降低成本、提高性能并解决容量问题。 类别可以基于所需的保护级别、性能要求、使用频率和其他注意事项。

数据迁移策略在分层存储策略的最终结果中扮演着重要的角色。 ODX 在分层存储设备中启用主机控制的数据迁移。 下图是分层存储设备中的 ODX 示例

-   服务器是分层存储系统的主机。 源 LUN 是 Tier1 存储设备, 目标 LUN 是 Tier2 存储设备。
-   所有分层存储设备由同一个复制管理器进行管理。
-   在服务器系统中, 数据迁移应用程序向源 LUN 发出卸载读取请求, 并从源 LUN 接收令牌, 然后使用令牌向目标 LUN 发出卸载写入请求。 复制管理器跨两个不同的层存储设备将数据从源 LUN 移动到目标 LUN。
-   完成数据迁移任务后, 应用程序将从 Tier1 存储设备中删除数据, 并回收存储空间。

 

 




