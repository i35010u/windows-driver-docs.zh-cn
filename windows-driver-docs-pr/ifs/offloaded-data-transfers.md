---
title: 卸载的数据传输
description: 在同一台计算机之间传输数据是一种频繁的文件系统活动。
ms.assetid: 66006CC0-8902-47CD-8E7C-187FE5BA71EF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95dfef3ec9a62345a117ce956b5925a4e61691ce
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063302"
---
# <a name="offloaded-data-transfers"></a>卸载的数据传输


在同一台计算机之间传输数据是一种频繁的文件系统活动。 使用标准的 **ReadFile** 和 **WriteFile** 函数可以很好地从功能角度进行工作，但它涉及到所有系统级别的数据移动，并可能跨网络。 这可能会影响传输和网络连接系统的可用性。 许多存储子系统提供的高级功能提供了更高效的方法来执行数据移动的 "繁重的任务"。

从 Windows 8 开始，应用程序可以利用这些功能来帮助卸载到存储子系统的数据移动过程。 文件系统筛选器通常可以通过将读取和写入请求拦截到卷来监视这些操作。 筛选器需要其他操作来识别卸载的数据传输。

## <a name="span-idtypical_data_transfersspanspan-idtypical_data_transfersspanspan-idtypical_data_transfersspantypical-data-transfers"></a><span id="Typical_Data_Transfers"></span><span id="typical_data_transfers"></span><span id="TYPICAL_DATA_TRANSFERS"></span>典型数据传输


今天在应用程序方案中移动数据非常简单。 它涉及到将数据读入本地内存，然后将数据写回到新位置。 下图说明了这种情况。

此方案涉及在两个不同文件服务器上的两个位置之间复制文件，每个位置都具有通过智能存储阵列公开的虚拟磁盘 (ISA) 。 初始系统首先需要将源虚拟磁盘中的数据读入本地缓冲区。 然后，它将通过某些传输和协议 (（例如 SMB over) 1GbE）将数据打包并传输到第二个系统，后者随后接收数据并将数据输出到本地缓冲区。 然后，目标系统将数据写入目标虚拟磁盘。 此方案描述了一种非常典型的数据传输读取/写入方法，这些方法每天由许多不同的应用程序执行多次。

![典型数据传输](images/odx-scenario-1.png)

虽然标准的读取和写入操作在大多数情况下非常有效，但要复制的数据可能位于由同一智能存储阵列管理的虚拟磁盘上。 这意味着数据将从阵列移出到服务器，通过网络传输传输到另一台服务器，并再次回到同一阵列中。 在服务器内和跨网络传输移动数据的操作会显著影响这些系统的可用性;不要说，数据移动的吞吐量受网络吞吐量和可用性的限制。

## <a name="span-idoffloaded_data_transfers__odx_spanspan-idoffloaded_data_transfers__odx_spanspan-idoffloaded_data_transfers__odx_spanoffloaded-data-transfers-odx"></a><span id="Offloaded_Data_Transfers__ODX_"></span><span id="offloaded_data_transfers__odx_"></span><span id="OFFLOADED_DATA_TRANSFERS__ODX_"></span>卸载的数据传输 (ODX) 


### <a name="span-idoffloading_the_data_transferspanspan-idoffloading_the_data_transferspanspan-idoffloading_the_data_transferspanoffloading-the-data-transfer"></a><span id="Offloading_the_Data_Transfer"></span><span id="offloading_the_data_transfer"></span><span id="OFFLOADING_THE_DATA_TRANSFER"></span>卸载数据传输

Windows 8 中引入了两个新的 FSCTLs，可帮助你卸载数据传输。 这会将位移动的负担从服务器转移到在存储子系统中智能地进行的位移动。 可视化命令语义的最佳方式是将其视为类似于未缓冲的读取和无缓冲的写入。

<span id="FSCTL_OFFLOAD_READ"></span><span id="fsctl_offload_read"></span>[**FSCTL \_ 卸载 \_ 读取**](./fsctl-offload-read.md)  
此控制请求在要读取的文件中获取偏移量，并在 [**FSCTL \_ 卸载 \_ 读取 \_ 输入**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_input) 结构中获取所需的长度。 如果支持，则承载该文件的存储子系统将接收关联的卸载读取存储命令，并生成一个令牌，该令牌是在卸载读取命令时要读取的数据的逻辑表示形式。 此标记字符串在 [**FSCTL \_ 卸载 \_ 读取 \_ 输出**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_output) 结构中返回给调用方。

<span id="FSCTL_OFFLOAD_WRITE"></span><span id="fsctl_offload_write"></span>[**FSCTL \_ 卸载 \_ 写入**](./fsctl-offload-write.md)  
此控制请求在要写入的文件中获取偏移量、所需的写入长度以及作为要写入的数据的逻辑表示形式的标记。 如果支持，则承载要写入的文件的存储子系统将收到关联的卸载写入存储命令。 它首先尝试识别给定的令牌，然后执行写操作（如果可能）。 在 Windows 下完成了写入操作，因此文件系统和存储堆栈上的组件将看不到数据移动。 数据移动完成后，写入的字节数将返回给调用方。

![卸载的数据传输](images/odx-scenario-2.png)

类似于第一个关系图，在两个不同的服务器上显示两个虚拟磁盘之间的简单文件副本。 我们不会执行正常的读取和写入操作，而是将位移动的重提升量卸载到存储阵列。 第一个系统发出卸载读取操作，请求数组生成一个标记，表示要在第一个虚拟磁盘区域内读取的数据的时间点视图。 然后，第一个系统将令牌传输到第二个系统，后者将使用令牌向第二个虚拟磁盘发出卸载写入操作。 然后，该数组将解释令牌并尝试执行虚拟磁盘之间的数据移动。 你会注意到，实际数据传输发生在智能存储阵列中，而不是在两个主机之间。 这显著提高了两个系统的可用性，同时几乎消除了系统之间的网络流量。

### <a name="span-idintegration_with_the_copy_enginespanspan-idintegration_with_the_copy_enginespanspan-idintegration_with_the_copy_enginespanintegration-with-the-copy-engine"></a><span id="Integration_with_the_Copy_Engine"></span><span id="integration_with_the_copy_engine"></span><span id="INTEGRATION_WITH_THE_COPY_ENGINE"></span>与复制引擎集成

**CopyFile**和相关函数使用 Windows 中的核心复制引擎。 从 Windows 8 开始，复制引擎将在传统的复制文件代码路径之前以透明方式尝试使用卸载的数据传输。 由于复制 Api 由大多数应用程序、实用程序和 shell 使用，因此，默认情况下，如果有任何代码修改或用户干预，则这些调用方可以使用卸载的数据传输功能。

以下步骤总结了 copy 引擎如何尝试卸载的数据传输：

1.  复制引擎会在源文件上发出 [**FSCTL \_ 卸载 \_ 读取**](./fsctl-offload-read.md) ，以获取读取令牌。
2.  如果检索读取令牌时出现故障，复制引擎将回退到传统的读取和写入 (传统的复制文件代码路径) 。 如果故障表明源卷不支持卸载，则复制引擎还会在每个进程缓存中标记该卷。 对于每个进程的缓存中的卷，复制引擎将不尝试重新卸载。
3.  如果已成功检索令牌，则复制引擎会尝试在大块区中的目标文件上发出 [**FSCTL \_ 卸载 \_ 写入**](./fsctl-offload-write.md) 命令，直到该令牌以逻辑方式表示的所有数据已被卸载写入。
4.  执行卸载读取或写入操作时出现的任何错误都会导致复制引擎回退到读写的传统代码路径，从该位置开始卸载代码路径 () 截断读取或写入的位置。 如果故障表明目标卷不支持卸载，或源卷无法访问目标卷，则复制引擎会更新相同的每个进程缓存，以便不会在这些卷上尝试卸载。 此每进程缓存将定期重置。

以下函数支持卸载的数据传输：

-   **CopyFile**
-   **CopyFileEx**
-   **MoveFile**
-   **MoveFileEx**
-   **CopyFile2**

以下函数不支持卸载的数据传输：

-   **CopyFileTransacted**
-   **MoveFileTransacted**

### <a name="span-idsupported_offload_data_transfer_scenariosspanspan-idsupported_offload_data_transfer_scenariosspanspan-idsupported_offload_data_transfer_scenariosspansupported-offload-data-transfer-scenarios"></a><span id="Supported_Offload_Data_Transfer_Scenarios"></span><span id="supported_offload_data_transfer_scenarios"></span><span id="SUPPORTED_OFFLOAD_DATA_TRANSFER_SCENARIOS"></span>支持的卸载数据传输方案

Hyper-v 存储堆栈和 Windows SMB 文件服务器中提供了对卸载操作的支持。 当后备物理存储支持 ODX 操作时，调用方可以向驻留在 Vhd 或远程文件共享上的文件发出 [**FSCTL \_ 卸载 \_ 读取**](./fsctl-offload-read.md) 和 [**FSCTL \_ 卸载 \_ 写入**](./fsctl-offload-write.md) 操作，无论是从虚拟机内部还是在物理硬件上。 下图说明了卸载数据传输的最基本的受支持源和目标目标。

![卸载的数据传输方案](images/odx-scenario-3.png)

## <a name="span-idfile_system_filter_opt-in_model_and_impact_to_applicationsspanspan-idfile_system_filter_opt-in_model_and_impact_to_applicationsspanspan-idfile_system_filter_opt-in_model_and_impact_to_applicationsspanfile-system-filter-opt-in-model-and-impact-to-applications"></a><span id="File_System_Filter_Opt-In_Model_and_Impact_to_Applications"></span><span id="file_system_filter_opt-in_model_and_impact_to_applications"></span><span id="FILE_SYSTEM_FILTER_OPT-IN_MODEL_AND_IMPACT_TO_APPLICATIONS"></span>文件系统筛选器选择模式和对应用程序的影响


从 Windows 8 开始，筛选器管理器允许筛选器将卸载功能指定为支持的功能。 附加到卷的文件系统筛选器可以共同确定是否支持某个卸载的操作;如果不是，则操作将失败，并出现相应的错误代码。

筛选器[**必须通过名 \_ \_ **](./fsctl-offload-write.md)为**SupportedFeatures**的注册表**DWORD**值（位于 FSCTL 的注册表中的驱动程序服务定义），在 HKEY [** \_ \_ **](./fsctl-offload-read.md) \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ \\ &lt; &gt; \\ 此值包含位域，其中位确定选择加入的功能，并且应在筛选器安装过程中设置。

目前，定义的位是：

| Flag                                               | 含义                               |
|----------------------------------------------------|---------------------------------------|
| 支持的 \_ FS \_ 功能 \_ 卸载 \_ 读取0x00000001  | 筛选器支持 FSCTL \_ 卸载 \_ 读取  |
| 支持的 \_ FS \_ 功能 \_ 卸载 \_ 写入0x00000002 | 筛选器支持 FSCTL \_ 卸载 \_ 写入 |

 

可以根据 HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Control \\ FileSystem \\ FilterSupportedFeaturesMode 注册表项（其值包含以下值）中提供的值来启用或禁用筛选器选择模型：

| FilterSupportedFeaturesMode 值 | 含义                                                                             |
|-----------------------------------|-------------------------------------------------------------------------------------|
| 0（默认值）                       | 执行正常的选择正在处理。                                                        |
| 1                                 | 从不选择加入 (等效于在所有附加的筛选器上将 SupportedFeatures 设置为 0)  |

 

### <a name="span-idtestingspanspan-idtestingspanspan-idtestingspantesting"></a><span id="Testing"></span><span id="testing"></span><span id="TESTING"></span>测试

若要检查堆栈支持的功能，请在 fltmc 实用程序中提供一个已更新的命令。 运行 **fltmc 实例– v \[ 卷 \] ：** 作为提升的用户，并检查 *SprtFtrs* 列。 如果筛选器的 *SprtFtrs* 值设置为0，则表示该筛选器在此卷上阻塞卸载。 如果 " *SprtFtrs* " 字段设置为3，则同时支持这两种卸载操作。

### <a name="span-idchecking_feature_support_in_irp__processingspanspan-idchecking_feature_support_in_irp__processingspanspan-idchecking_feature_support_in_irp__processingspanchecking-feature-support-in-irp-processing"></a><span id="Checking_Feature_Support_in_IRP__Processing"></span><span id="checking_feature_support_in_irp__processing"></span><span id="CHECKING_FEATURE_SUPPORT_IN_IRP__PROCESSING"></span>检查 IRP 处理中的功能支持

作为 IRP 处理的一部分， [**FsRtlGetSupportedFeatures**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-fsrtlgetsupportedfeatures) 例程检索附加到给定卷堆栈的所有筛选器的聚合 **SupportedFeatures** 状态。 组件（如 i/o 管理器和 SRV (SMB) 调用此例程来验证堆栈上所有筛选器的 **SupportedFeatures** 状态。 滚动自己的卸载 Irp 的组件应调用此函数来验证对该操作的选择支持。

### <a name="span-idconsiderations_for_filter_driversspanspan-idconsiderations_for_filter_driversspanspan-idconsiderations_for_filter_driversspanconsiderations-for-filter-drivers"></a><span id="Considerations_for_Filter_Drivers"></span><span id="considerations_for_filter_drivers"></span><span id="CONSIDERATIONS_FOR_FILTER_DRIVERS"></span>筛选器驱动程序的注意事项

卸载数据传输是在数据中心内移动数据的一种新方法。 由于在核心复制引擎中集成了卸载逻辑，因此，默认情况下，很多应用程序能够执行卸载的数据移动，而无需明确选择加入。 因此，筛选器开发人员需要了解这些新操作对筛选器的影响。 不了解这些操作完全或不能评估新数据流可能会导致数据不一致或损坏的情况。 下面的列表汇总了一组操作项，供筛选器开发人员记下进行卸载：

-   了解新的数据流、对筛选器的影响，以及支持这些卸载操作的筛选器的功能。
-   更新筛选器安装程序，将 SupportedFeatures 的 REG \_ DWORD **SupportedFeatures**值添加到 HKLM \\ System \\ CurrentControlSet \\ Services \\ \[ filter \] 子项。 将其初始化以指定卸载功能。
-   对于想要执行卸载操作的筛选器，请将注册更新为 **IRP \_ MJ \_ 文件 \_ 系统 \_ 控制** 来处理 [**FSCTL \_ 卸载 \_ 读取**](./fsctl-offload-read.md) 和 [**FSCTL \_ 卸载 \_ 写入**](./fsctl-offload-write.md)操作。
-   对于需要阻止卸载操作的筛选器，返回 \_ 筛选器中不支持的状态代码状态 \_ 。 不要依赖于注册表值来强制阻止卸载操作，因为最终用户可以对其进行更改。 筛选器应显式允许或禁止卸载操作。

## <a name="span-idcopy_tokensspanspan-idcopy_tokensspanspan-idcopy_tokensspancopy-tokens"></a><span id="Copy_Tokens"></span><span id="copy_tokens"></span><span id="COPY_TOKENS"></span>复制令牌


使用卸载操作时，i/o 堆栈不会显示文件数据。 相反，它被视为数据的逻辑代理作为512字节的标记。 此令牌是存储子系统生成的特定于供应商的格式的不透明且唯一的字符串，也可以是众所周知的类型来表示数据的模式 (例如逻辑上等于零) 的数据范围。 对标记是其代理的数据进行的修改将导致令牌无效，或使存储子系统按特定于供应商的 (方式（例如通过快照机制) ）保存原始数据。 对于文件中指定范围的后续卸载读取请求将生成唯一标记。

有类标记表示定义良好的数据模式。 最常见的已知标记是与零等效的零标记。 当令牌被定义为众所周知的令牌时，**存储 \_ 卸载 \_ 令牌**结构中的**TOKENTYPE**成员将设置为存储 \_ 卸载 \_ 令牌 \_ 类型 \_ 众所周知的 \_ 。 设置此字段时， **WellKnownPattern** 成员确定标记的数据模式。

-   当 **WellKnownPattern** 字段设置为存储 \_ 卸载 \_ 模式 \_ 零或存储 \_ 卸载 \_ 模式 \_ 为零时 \_ ，将 \_ \_ 显示零标记。 当 [**FSCTL \_ 卸载 \_ 读取**](./fsctl-offload-read.md) 操作返回此令牌时，它表示所需文件范围内包含的数据在逻辑上等于零。 向 [**FSCTL \_ 卸载 \_ 写入**](./fsctl-offload-write.md) 操作提供此令牌时，它指示要写入的文件的所需范围应在逻辑上归零。
-   除了零标记，当前还没有定义其他已知的标记模式。 不建议用户定义自己的已知标记模式。

## <a name="span-idtruncationspanspan-idtruncationspanspan-idtruncationspantruncation"></a><span id="Truncation"></span><span id="truncation"></span><span id="TRUNCATION"></span>短


Windows 与之通信的基础存储子系统可以处理卸载操作所需的更少数据。 这称为 "截断"。 使用 "卸载" 读取时，这意味着返回的令牌表示比请求的数据范围少的数据。 这由[**FSCTL \_ 卸载 \_ 读取 \_ 输出**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_output)结构中的**TransferLength**成员指示，该结构是从要读取的文件范围的开头开始的字节计数。 对于卸载写入，截断表明写入的数据量小于所需的数据量。 这由[**FSCTL \_ 卸载 \_ 写入 \_ 输出**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_output)结构中的**LengthWritten**成员指示，后者是要写入的文件范围开头的字节计数。 命令处理中的错误或大型范围内堆栈限制会导致截断。

在以下两种情况下，NTFS 会截断要读取或写入的范围：

1.  如果 VDL 在文件结尾 (EOF) 之前，则复制范围将被截断为有效数据长度 (VDL) 。 这假定 VDL 与逻辑扇区边界对齐，否则请参阅方案。

    ![eof 之前发生的 vdl](images/odx-vdl-1.png)

    在[**FSCTL \_ 卸载 \_ 读取**](./fsctl-offload-read.md)操作过程中，在 \_ \_ \_ \_ FSCTL 卸载读取输出的结构中设置了标志卸载读取标志全部为零，这 \_ \_ \_ 表示文件的其余部分包含零，而**TransferLength**成员被截断为 VDL。 [** \_ \_ \_ **](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_read_output)

2.  类似于方案1，但当 VDL 未与逻辑扇区边界对齐时，所需范围将被 NTFS 截断到下一个逻辑扇区边界。

    ![vdl 与扇区边界未对齐](images/odx-vdl-2.png)

## <a name="span-idlimitationsspanspan-idlimitationsspanspan-idlimitationsspanlimitations"></a><span id="Limitations"></span><span id="limitations"></span><span id="LIMITATIONS"></span>限制


-   仅 NTFS 卷支持卸载操作。
-   如果远程共享为 NTFS 卷，并且服务器正在运行 Windows Server 2012，则支持通过远程文件服务器来执行卸载操作 (假设远程堆栈还支持) 的卸载操作。
-   NTFS 不支持对用 Bitlocker 或 NTFS 加密 (的文件执行的卸载 FSCTLs EFS) ，消除重复的文件、压缩文件、常驻文件、稀疏文件或参与了 TxF 事务处理的文件。
-   NTFS 不支持对 volsnap 快照中的文件执行的卸载 FSCTLs。
-   如果所需的文件范围与源设备上的逻辑扇区大小不对齐，或所需的文件范围与目标设备上的逻辑扇区大小不对齐，则 NTFS 将无法卸载 FSCTL。 这与非缓存 IO 遵循相同的语义。
-   在[**FSCTL \_ 卸载 \_ 写入**](./fsctl-offload-write.md)之前，目标文件必须预先分配 (**SetEndOfFile** ，而不是**SetAllocation**) 。
-   在处理卸载读取和卸载写入时，NTFS 首先调用 [**CcCoherencyFlushAndPurgeCache**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-cccoherencyflushandpurgecache) 以提交系统缓存中任何已修改的数据。 这与非缓存 IO 的语义相同。

 

