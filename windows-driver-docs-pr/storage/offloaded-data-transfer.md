---
title: 卸载了数据传输
description: 卸载了数据传输
ms.assetid: EDFA6AFB-7D14-44F8-A105-E74182D26398
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5ba3fad840820d8c772e645220f3d12fd0705be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389422"
---
# <a name="offloaded-data-transfer"></a>卸载了数据传输


## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概述


卸载数据传输 (ODX) 引入了存储设备上移动数据的已标记化的操作。 源文件和目标文件可以位于同一个卷、 两个不同的卷由在同一台计算机、 本地卷和通过 SMB2，远程卷承载或通过 SMB2 两个不同的计算机上的两个卷上。 Windows 8 中引入了卸载数据传输。

下面是使用 ODX 复制卸载操作的过程。

1.  复制卸载应用程序发送到源存储设备的复制管理器卸载读取的请求。
2.  应用程序将接收卸载读取的结果请求发送到的复制管理器，并返回令牌。 该标记是数据要复制的表示形式。
3.  应用程序将与令牌的卸载写入请求发送到目标存储设备的复制管理器。
4.  应用程序将接收卸载写入结果请求发送到的复制管理器。 复制管理器将数据从源系统移到目标，并卸载写入结果返回到应用程序。

## <a name="span-ididentifyanodx-capablesourceanddestinationspanspan-ididentifyanodx-capablesourceanddestinationspanspan-ididentifyanodx-capablesourceanddestinationspanidentify-an-odx-capable-source-and-destination"></a><span id="Identify_an_ODX-Capable_Source_and_Destination"></span><span id="identify_an_odx-capable_source_and_destination"></span><span id="IDENTIFY_AN_ODX-CAPABLE_SOURCE_AND_DESTINATION"></span>确定支持 ODX 的源和目标


若要支持 ODX，存储阵列必须实现相关的 T10 标准规范。 标识是支持 ODX 的存储阵列，卸载读取和写入操作，并卸载具有已知标记编写。 在 LUN 设备枚举 （系统启动或即插即用 play 事件）。 Windows 收集或更新 ODX 功能信息的存储目标设备完成以下步骤。

1.  查询副本卸载功能。
2.  收集有关复制所需的参数将卸载操作和限制。

默认情况下，Windows ODX 路径首次尝试复制操作的源和目标 Lun 是否支持 ODX。 如果存储设备失败初始 ODX 请求，Windows 将标记的源和目标 LUN 组合为"不 ODX 支持"路径。

## <a name="span-idodxreadwriteoperationsspanspan-idodxreadwriteoperationsspanspan-idodxreadwriteoperationsspanodx-readwrite-operations"></a><span id="ODX_Read_Write_Operations"></span><span id="odx_read_write_operations"></span><span id="ODX_READ_WRITE_OPERATIONS"></span>ODX 读/写操作


### <a name="span-idsynchronouscommandadoptionandapisspanspan-idsynchronouscommandadoptionandapisspanspan-idsynchronouscommandadoptionandapisspansynchronous-command-adoption-and-apis"></a><span id="Synchronous_Command_Adoption_and_APIs"></span><span id="synchronous_command_adoption_and_apis"></span><span id="SYNCHRONOUS_COMMAND_ADOPTION_AND_APIS"></span>同步命令采用和 Api

Windows 同步卸载读取和写入操作。 使用以下算法来确保可靠同步卸载写入拆分大型卸载写入请求。

-   如果目标存储设备不提供最佳的传送大小，最佳的传送大小设置为 64 MB。
-   指定的存储目标设备的最佳的传送大小 — 最佳的传送大小是大于零且小于 256 MB。
-   设置目标设备的最佳的传送大小是否大于 256 MB，最佳的传送大小设置为 256 MB。

同步卸载读取和卸载编写 SCSI 命令降低了复杂的 MPIO 和群集故障转移方案。 Windows 需要复制管理器在 4 秒内完成同步卸载读/写 SCSI 命令。

应用程序可以使用 FSCTL、 DSM IOCTL 或 SCSI\_传递\_通过 Api 来与存储阵列进行交互并执行复制卸载操作。 若要避免数据损坏或系统不稳定，Windows 将限制从直接写入由文件系统，而第一个获取独占访问卷未装载的卷的应用程序。 这是因为写入该卷可能与文件系统写入操作发生冲突的条件。 此类冲突发生时，卷的内容可能会处于不一致的状态。

### <a name="span-idoffloadreadoperationsspanspan-idoffloadreadoperationsspanspan-idoffloadreadoperationsspanoffload-read-operations"></a><span id="Offload_Read_Operations"></span><span id="offload_read_operations"></span><span id="OFFLOAD_READ_OPERATIONS"></span>卸载读取操作

卸载读取请求的应用程序可以指定的令牌生存期 （非活动超时）。 如果应用程序将令牌生存期设置为零，则默认的非活动计时器用作令牌生存期。 存储阵列的复制管理器维护，并验证该令牌根据其非活动超时值和凭据。 Windows 主机还限制为 64 的文件碎片的数量。 如果卸载读取的请求包含 64 个以上的片段，Windows 副本卸载请求失败，并将回退到传统的复制操作。

完成卸载读取请求后，复制管理器接收卸载读取的结果命令准备数据 (ROD) 标记的表示形式。 ROD 令牌字段指定用户数据和保护信息的时间点表示形式。 ROD 可以是"以独占方式打开"或"使用共享打开"格式中的用户数据。 复制管理器可以使根据其 ROD 策略设置令牌失效。 如果 ROD 处于打开状态的副本以独占方式卸载操作，可以使 ROD 令牌失效时杆是修改或移动。 如果 ROD 处于"打开与共享"的格式，修改 ROD 时 ROD 令牌保持有效。

| 大小 （字节） | 令牌的内容 |
|---------------|----------------|
| 4             | ROD 标记类型 |
| 508           | ROD 令牌 ID   |

 

ROD 令牌授予并仅使用存储阵列，因为其格式是不透明、 唯一的且高度安全。 如果令牌修改，不进行验证，或已过期，复制管理器可以使令牌失效期间卸载写入操作。 卸载从返回的 ROD 令牌读取操作的非活动超时值，以指示复制管理器必须保持该令牌有效的下一步编写使用的令牌使用情况的秒数。

### <a name="span-idoffloadwriteoperationsspanspan-idoffloadwriteoperationsspanspan-idoffloadwriteoperationsspanoffload-write-operations"></a><span id="Offload_Write_Operations"></span><span id="offload_write_operations"></span><span id="OFFLOAD_WRITE_OPERATIONS"></span>卸载写入操作

从复制管理器收到 ROD 令牌之后, 该应用程序将卸载写入请求与 ROD 令牌发送到存储阵列的复制管理器。 当同步卸载写命令发送到目标设备时，Windows 将需要在 4 秒内完成该命令的复制管理器。 如果该命令由于命令超时或其他错误条件而终止，Windows 将失败命令。 应用程序将回退到旧的复制操作根据返回的状态代码。

可以使用一个或多个接收卸载写入结果命令完成卸载写入请求。 如果已部分完成卸载写入，复制管理器返回具有估计的延迟和传输数计数指示复制进度。 传输计数的数字指定已写入没有错误从源到目标媒体的连续逻辑块的数目。 在顺序卸载写入或散播-聚集模式，可以执行复制管理器。

写入错误发生时，复制进度计数连续的逻辑块从第一个逻辑块的失败块。 客户端应用程序或复制引擎将恢复从写入失败块卸载写入。 完成卸载写后，复制管理器完成将设置为 0 和 100%的数据传输计数的进度的估计的状态更新延迟接收 ROD 令牌信息命令。 如果要接收卸载写入结果返回的数据传输计数相同进度，Windows 会失败回应用程序后四次重试复制操作。

客户端应用程序还可以执行卸载写操作使用的已知 ROD 令牌。 这是预定义的： ROD 令牌使用已知的数据模式和令牌格式。 一种常见实现被调用的零个令牌。 客户端应用程序可以使用零标记来填充一个或多个范围逻辑块零。 如果不支持的已知标记或可识别，复制管理器无法卸载写入请求并"无效令牌"。

| 大小 （字节） | 令牌的内容     |
|---------------|--------------------|
| 4             | ROD 标记类型     |
| 2             | 常见模式 |
| 506           | ROD 令牌 ID       |

 

在使用的已知 ROD 令牌的卸载写入，客户端应用程序无法使用读取请求的已知令牌卸载。 复制管理器验证并维护的已知的 ROD 令牌，根据自己的策略。

### <a name="span-idperformancetuningparametersofodximplementationspanspan-idperformancetuningparametersofodximplementationspanspan-idperformancetuningparametersofodximplementationspanperformance-tuning-parameters-of-odx-implementation"></a><span id="Performance_Tuning_Parameters_of_ODX_Implementation"></span><span id="performance_tuning_parameters_of_odx_implementation"></span><span id="PERFORMANCE_TUNING_PARAMETERS_OF_ODX_IMPLEMENTATION"></span>性能优化的 ODX 实现参数

ODX 性能不依赖于服务器和存储阵列之间的传输链接速度的客户端-服务器网络或 SAN。 通过复制管理器和设备的存储阵列的服务器移动数据。

不是每个副本将卸载从 ODX 技术的优势。 例如，1 千兆位 iSCSI 存储阵列的复制管理器无法在 10 秒内完成的 3 GB 文件副本和将大于 300 MB / 秒的数据传输速率。 数据传输速率已优于 1 千兆位以太网接口的最大的理论传输速度。

不是每个文件大小副本卸载将获得从 Windows ODX 技术优势。 很可能某些大小的文件的复制性能可能会不受益于 ODX 技术。 若要优化性能，ODX 使用可以是受限制到允许的最小文件大小和最大复制长度。 若要优化的 ODX 性能，请调整以下参数。

Windows 设置副本的最小文件大小要求卸载操作。 目前，最小副本卸载文件大小为 256 KB 设置复制引擎中。 如果文件是小于 256 KB，则复制引擎回退到旧的复制过程中。

Windows 主机使用的令牌的最大传输大小和要准备卸载最佳的传送大小的最佳传输计数读取或写入 SCSI 命令。 数据块数量的总传输大小不得超过令牌的最大传输大小。 如果存储阵列未报告的最佳传输计数，Windows 将使用默认计数为 64 MB。

最佳和最大传输长度参数指定一个范围描述符中的块的最佳和最大数目。 复制卸载应用程序可以符合这些参数可获得最佳的文件的传输性能。

## <a name="span-idodxerrorhandlingandhighavailabilitysupportspanspan-idodxerrorhandlingandhighavailabilitysupportspanspan-idodxerrorhandlingandhighavailabilitysupportspanodx-error-handling-and-high-availability-support"></a><span id="ODX_Error_Handling_and_High_Availability_Support"></span><span id="odx_error_handling_and_high_availability_support"></span><span id="ODX_ERROR_HANDLING_AND_HIGH_AVAILABILITY_SUPPORT"></span>ODX 错误处理和高可用性支持


当的 ODX 操作失败时文件复制请求时，复制引擎和 Windows 文件系统 (NTFS) 回退到旧的复制操作。 如果要复制卸载中间卸载写入操作将失败，复制引擎和 NTFS 将恢复与卸载写操作中从第一个故障点 （旧） 复制操作。

下面是使用 ODX 复制卸载操作的算法。

### <a name="span-idodxerrorhandlingspanspan-idodxerrorhandlingspanspan-idodxerrorhandlingspanodx-error-handling"></a><span id="ODX_Error_Handling"></span><span id="odx_error_handling"></span><span id="ODX_ERROR_HANDLING"></span>ODX 错误处理

ODX 使用可靠的错误处理根据存储阵列功能的算法。 如果要复制卸载 odx 兼容的路径中的失败，Windows 主机需要要故障回复到旧的复制操作的应用程序。 在此情况下，Windows 复制引擎已实现"回退到传统的副本"的机制。 复制卸载失败后，NTFS 将标记的源和目标 LUN 为不支持 ODX 的三分钟。 通过这段时间后，Windows 将复制引擎重试 ODX 操作。 存储阵列可以使用此功能在高度紧张的操作的情况下临时禁用 ODX 支持中的某些路径。

### <a name="span-idodxfailoverinmpioandclusterserverconfigurationsspanspan-idodxfailoverinmpioandclusterserverconfigurationsspanspan-idodxfailoverinmpioandclusterserverconfigurationsspanodx-failover-in-mpio-and-cluster-server-configurations"></a><span id="ODX_Failover_in_MPIO_and_Cluster_Server_Configurations"></span><span id="odx_failover_in_mpio_and_cluster_server_configurations"></span><span id="ODX_FAILOVER_IN_MPIO_AND_CLUSTER_SERVER_CONFIGURATIONS"></span>ODX MPIO 和群集服务器配置中的故障转移

卸载读取和写入操作必须已完成或取消从相同的存储链接 (我\_T nexus)。

MPIO 或群集服务器故障转移同步卸载过程中发生时读取或写入操作，Windows 处理使用以下算法的故障转移。

1.  同步卸载读/写命令。
2.  使用 MPIO 配置 — Windows 在 MPIO 路径故障转移后重试失败的命令。 如果该命令再次失败，Windows 执行以下操作。
    -   如果不使用群集服务器故障转移选项 – Windows 发出 LUN 重置为存储设备，并返回应用程序的 I/O 故障状态。
    -   使用群集服务器故障转移选项 – Windows 启动群集服务器节点故障转移。

3.  使用群集服务器配置 — 群集存储服务将故障转移到下一个首选的群集节点，然后恢复群集存储服务。 卸载应用程序必须是群集感知，以便能够在群集存储空间服务故障转移后重试卸载读/写命令。

如果卸载读取或写入命令失败 MPIO 路径和群集节点故障转移后，Windows 会发出故障转移后重置为存储设备的 LUN。 存储设备将终止所有未完成的命令和挂起的 LUN 下的操作。

目前，Windows 不发出异步卸载读取或写入从存储堆栈的 SCSI 命令。

## <a name="span-idodxusagemodelsspanspan-idodxusagemodelsspanspan-idodxusagemodelsspanodx-usage-models"></a><span id="ODX_Usage_Models"></span><span id="odx_usage_models"></span><span id="ODX_USAGE_MODELS"></span>ODX 使用模型


### <a name="span-idodxacrossphysicaldiskvirtualharddiskandsmbshareddiskspanspan-idodxacrossphysicaldiskvirtualharddiskandsmbshareddiskspanspan-idodxacrossphysicaldiskvirtualharddiskandsmbshareddiskspanodx-across-physical-disk-virtual-hard-disk-and-smb-shared-disk"></a><span id="ODX_across_Physical_Disk__Virtual_Hard_Disk_and_SMB_Shared_Disk"></span><span id="odx_across_physical_disk__virtual_hard_disk_and_smb_shared_disk"></span><span id="ODX_ACROSS_PHYSICAL_DISK__VIRTUAL_HARD_DISK_AND_SMB_SHARED_DISK"></span>ODX 跨物理磁盘、 虚拟硬盘和 SMB 共享磁盘

若要执行 ODX 操作，应用程序服务器必须具有对源 LUN 和使用读/写权限的目标 LUN 的访问权限。 复制卸载应用程序发出读取请求与源 LUN 卸载并从复制管理器的源 LUN 将收到一个令牌。 复制将卸载应用程序使用令牌向目标 LUN 发出卸载写入请求。 复制管理器然后将数据移动 LUN 从源到目标 LUN 通过存储网络。

### <a name="span-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanodx-operation-with-one-server"></a><span id="ODX_Operation_with_One_Server"></span><span id="odx_operation_with_one_server"></span><span id="ODX_OPERATION_WITH_ONE_SERVER"></span>一台服务器的 ODX 操作

在单服务器配置中，复制将卸载卸载中读取和写入请求相同的服务器系统的应用程序问题。

### <a name="span-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanspan-idodxoperationwithoneserverspanodx-operation-with-one-server"></a><span id="ODX_Operation_with_One_Server"></span><span id="odx_operation_with_one_server"></span><span id="ODX_OPERATION_WITH_ONE_SERVER"></span>一台服务器的 ODX 操作

在单服务器配置中，复制将卸载卸载中读取和写入请求相同的服务器系统的应用程序问题。

在上图中，Server1 或虚拟机 1 有权访问源 LUN （VHD1 或物理 Disk1） 和目标 LUN （VHD2 或物理 Disk2）。 复制卸载卸载读取到源 LUN 请求并接收来自源 LUN，令牌的应用程序问题以及副本然后卸载应用程序使用令牌向目标 LUN 发出卸载写入请求。 复制管理器将数据从源 LUN 移动到同一存储阵列中目标 LUN。

### <a name="span-idodxoperationwithtwoserversspanspan-idodxoperationwithtwoserversspanspan-idodxoperationwithtwoserversspanodx-operation-with-two-servers"></a><span id="ODX_Operation_with_Two_Servers"></span><span id="odx_operation_with_two_servers"></span><span id="ODX_OPERATION_WITH_TWO_SERVERS"></span>具有两个服务器的 ODX 操作

在两台服务器配置中，有两个服务器和多个相同副本管理器管理的存储阵列。

-   Server1 或虚拟机 1 是源 LUN 的主机和 Server2 或虚拟机 2 是目标 LUN 的主机。 Server1 与应用程序客户端通过 SMB 协议共享 LUN 的源和 Server2 还允许通过 SMB 协议的应用程序客户端会与目标 LUN。 应用程序客户端有权访问 LUN 的源和目标 LUN。
-   源和目标存储阵列管理的 SAN 配置中的相同副本管理器。
-   从应用程序客户端系统，该副本将卸载卸载读取到源 LUN 请求和接收来自源 LUN 的令牌以及然后到目标 LUN 与令牌颁发卸载写入请求的应用程序问题。 复制管理器将数据从源 LUN 移动到跨两个不同位置中的两个不同的存储阵列目标 LUN。

### <a name="span-idmassivedatamigrationspanspan-idmassivedatamigrationspanspan-idmassivedatamigrationspanmassive-data-migration"></a><span id="Massive_Data_Migration"></span><span id="massive_data_migration"></span><span id="MASSIVE_DATA_MIGRATION"></span>大规模的数据迁移

大规模的数据迁移是将大量的数据库记录、 电子表格、 文本文件、 扫描的文档和图像等数据导入到新系统的过程。 数据迁移可能造成存储系统升级、 新的数据库引擎或应用程序或业务流程中的更改。 ODX 可将数据从旧存储系统迁移到新的存储系统，如果旧存储系统可由复制管理器的新的存储系统。

-   Server1 是旧存储系统的主机和 Server2 是新的存储系统的主机。 Server1 作为数据迁移应用程序客户端通过 SMB 协议共享 LUN 的源和 Server2 作为数据迁移应用程序客户端通过 SMB 协议共享目标 LUN。 应用程序客户端有权访问的源和目标 LUN。
-   由 SAN 配置中的相同副本管理器管理的旧存储系统和新的存储系统。
-   数据迁移的应用程序客户端系统中，从该副本将卸载卸载读取到源 LUN 请求和接收来自源 LUN 的令牌以及然后到目标 LUN 与令牌颁发卸载写入请求的应用程序问题。 复制管理器将数据从源 LUN 移动到目标 LUN 跨两个不同位置的两个不同的存储系统。
-   大规模的数据迁移无法与一个服务器上的相同位置也运营。

### <a name="span-idhost-controlleddatatransferwithinatieredstoragedevicespanspan-idhost-controlleddatatransferwithinatieredstoragedevicespanspan-idhost-controlleddatatransferwithinatieredstoragedevicespanhost-controlled-data-transfer-within-a-tiered-storage-device"></a><span id="Host-Controlled_Data_Transfer_within_a_Tiered_Storage_Device"></span><span id="host-controlled_data_transfer_within_a_tiered_storage_device"></span><span id="HOST-CONTROLLED_DATA_TRANSFER_WITHIN_A_TIERED_STORAGE_DEVICE"></span>分层的存储设备内的主机控制数据传输

分层的存储设备对数据进行分类到不同类型的存储介质，以降低成本、 提高性能，并满足容量问题。 类别可以基于所需的保护级别、 性能要求、 使用情况的频率和其他注意事项。

数据迁移策略分层的存储策略的最终结果中扮演着重要角色。 ODX，允许主机控制的数据迁移在分层的存储设备中。 下图是分层的存储设备中的 ODX 示例

-   服务器是分层的存储系统的主机。 源 LUN 是层级 1 存储设备，并且目标 LUN 是第 2 层存储设备。
-   由相同的复制管理器管理所有分层的存储设备。
-   从服务器系统中，数据迁移应用程序发出读取请求与源 LUN 卸载和接收来自源 LUN 的令牌，然后到目标 LUN 与令牌颁发卸载写入请求。 复制管理器将数据从源 LUN 移动到目标 LUN 跨两个不同的层存储设备。
-   完成数据迁移任务后，应用程序从层级 1 存储设备中删除数据，并回收存储空间。

 

 




