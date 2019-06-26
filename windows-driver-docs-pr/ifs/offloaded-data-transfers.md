---
title: 卸载的数据传输
description: 计算机之间或在同一台计算机传输数据是常见的文件系统活动。
ms.assetid: 66006CC0-8902-47CD-8E7C-187FE5BA71EF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eaa44e190ea34938970806c4c27410e73fdbe0b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386074"
---
# <a name="offloaded-data-transfers"></a>卸载的数据传输


计算机之间或在同一台计算机传输数据是常见的文件系统活动。 使用标准**ReadFile**并**WriteFile**函数的工作方式也从功能角度看，但它涉及到通过所有级别的繁重的数据移动的系统和可能的网络。 这会影响在传输和网络连接系统中所涉及的系统可用性。 适用于多个存储子系统的高级的功能提供更高效的方法来执行数据移动该繁重任务。

从 Windows 8 开始，应用程序可以充分利用这些功能，可帮助将卸载的数据移动到的存储子系统过程。 文件系统筛选器通常可以监视这些操作通过截获读取和写入请求发送到卷。 其他操作所需的筛选器需要注意的卸载的数据传输。

## <a name="span-idtypicaldatatransfersspanspan-idtypicaldatatransfersspanspan-idtypicaldatatransfersspantypical-data-transfers"></a><span id="Typical_Data_Transfers"></span><span id="typical_data_transfers"></span><span id="TYPICAL_DATA_TRANSFERS"></span>典型的数据传输


移动数据的应用程序方案中现在是非常简单。 这涉及到的读取到本地内存中，然后将其写数据返回到新位置。 下图说明了这种情况。

此方案涉及到复制在两个不同的文件服务器，每个都有其自身公开通过智能存储阵列 (ISA) 的虚拟磁盘上的两个位置之间的文件。 初始系统首先需要从源虚拟磁盘将数据读入的本地缓冲区。 然后，它打包，并通过一些传输和协议 （比如通过 1GbE 的 SMB) 到第二个系统，然后接收数据并将其输出到的本地缓冲区将数据传输。 然后，在目标系统将数据写入目标虚拟磁盘。 此方案中描述数据传输每天都执行多个时间由许多不同的应用程序的非常典型读/写的方法。

![典型的数据传输](images/odx-scenario-1.png)

尽管标准读取和写入工作也在大多数情况下，想要复制的数据可能位于相同的智能存储阵列由管理的虚拟磁盘上。 这意味着，在移动数据时从数组到服务器，跨网络传输，到另一台服务器上并恢复到同一数组再一次。 服务器内和跨网络传输将数据移操作可能会显著影响这两个系统; 的可用性更不必说这一事实的数据移动吞吐量受吞吐量和网络的可用性。

## <a name="span-idoffloadeddatatransfersodxspanspan-idoffloadeddatatransfersodxspanspan-idoffloadeddatatransfersodxspanoffloaded-data-transfers-odx"></a><span id="Offloaded_Data_Transfers__ODX_"></span><span id="offloaded_data_transfers__odx_"></span><span id="OFFLOADED_DATA_TRANSFERS__ODX_"></span>卸载的数据传输 (ODX)


### <a name="span-idoffloadingthedatatransferspanspan-idoffloadingthedatatransferspanspan-idoffloadingthedatatransferspanoffloading-the-data-transfer"></a><span id="Offloading_the_Data_Transfer"></span><span id="offloading_the_data_transfer"></span><span id="OFFLOADING_THE_DATA_TRANSFER"></span>卸载数据传输

简化的卸载数据传输方法的 Windows 8 中引入了两个新 FSCTLs。 这会转而离开服务器为 bit 以智能方式出现在存储子系统的移动的位移动的负担。 可视化命令语义的最佳方法是将它们视为类似于无缓冲的读取和无缓冲的写入。

<span id="FSCTL_OFFLOAD_READ"></span><span id="fsctl_offload_read"></span>[**FSCTL\_OFFLOAD\_READ**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-read)  
此控件请求需要执行内要读取的文件和所需的长度中的偏移量[ **FSCTL\_卸载\_读取\_输入**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_input)结构。 如果支持，托管文件的存储子系统接收相关联的卸载读取存储命令，并生成一个令牌，这是用于在读取命令卸载时读取的数据的逻辑表示形式。 此标记的字符串返回给调用方在[ **FSCTL\_卸载\_读取\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_output)结构。

<span id="FSCTL_OFFLOAD_WRITE"></span><span id="fsctl_offload_write"></span>[**FSCTL\_OFFLOAD\_WRITE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-write)  
此控件请求花费的要写入到的文件、 所需的长度的写入和要写入的数据的逻辑表示形式的令牌内的偏移量。 如果支持，托管要写入的文件的存储子系统将收到相关联的卸载写入存储命令。 它首先尝试识别给定的令牌，并随后会在可能的情况执行写入操作。 写操作完成下 Windows，并且因此文件系统和存储堆栈上的组件不会看到数据移动。 数据移动完成后，写入的字节数返回给调用方。

![卸载数据传输](images/odx-scenario-2.png)

类似于第一个关系图，将显示两个不同的服务器上的两个虚拟磁盘之间的简单文件副本。 而不是执行一般的读取和写入，我们解除繁重的位移动到存储阵列。 第一个系统会发出读取操作，请求数组来生成令牌表示的第一个虚拟磁盘的区域内读取的数据的时间点视图卸载。 然后，第一个系统传输到第二个系统，又卸载的问题都写入具有令牌的第二个虚拟磁盘的操作的令牌。 数组然后解释该令牌，并尝试执行的虚拟磁盘之间的数据移动。 您会注意到实际的数据传输在智能存储阵列中和在两个主机之间不会发生。 这显著提高了几乎消除了在系统之间的网络流量时的两个系统的可用性。

### <a name="span-idintegrationwiththecopyenginespanspan-idintegrationwiththecopyenginespanspan-idintegrationwiththecopyenginespanintegration-with-the-copy-engine"></a><span id="Integration_with_the_Copy_Engine"></span><span id="integration_with_the_copy_engine"></span><span id="INTEGRATION_WITH_THE_COPY_ENGINE"></span>与复制引擎的集成

使用 Windows 中的核心复制引擎**CopyFile**和相关函数。 从 Windows 8 开始，复制引擎将以透明方式尝试使用卸载数据传输之前传统复制文件的代码路径中。 由于复制 Api 由大多数应用程序，实用程序，并且通过在 shell 中，这些调用方，可以使用卸载数据传输功能默认情况下很少或者，如果有，因此代码修改或用户干预。

以下步骤总结了如何复制引擎将尝试卸载的数据传输：

1.  复制引擎问题[ **FSCTL\_卸载\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-read)上源文件以获取读取的令牌。
2.  如果检索读取的令牌的过程中出现错误，复制引擎将回退到传统的读取和写入 （传统复制文件的代码路径）。 如果失败指示源卷不支持卸载，复制引擎还会将标记每个过程缓存中的卷。 复制引擎不会尝试卸载再为每个过程缓存中的卷。
3.  如果成功检索令牌，复制引擎将尝试发出[ **FSCTL\_卸载\_编写**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-write)上是大型的区块，直到所有的数据中的目标文件的命令标记以逻辑方式表示已编写的卸载。
4.  关闭 （其中读取或写入被截断） 结束从其中卸载代码路径中执行卸载的任何错误在读取或写入结果回退到传统的代码路径的读取和写入，复制引擎。 如果失败指示的目标卷不支持卸载，或源卷不能达到的目标量，复制引擎会更新相同的每个进程缓存，因此它不会尝试卸载这些卷上。 将定期重置此每个进程缓存。

以下函数支持卸载的数据传输：

-   **CopyFile**
-   **CopyFileEx**
-   **MoveFile**
-   **MoveFileEx**
-   **CopyFile2**

以下函数执行不支持卸载数据传输操作：

-   **CopyFileTransacted**
-   **MoveFileTransacted**

### <a name="span-idsupportedoffloaddatatransferscenariosspanspan-idsupportedoffloaddatatransferscenariosspanspan-idsupportedoffloaddatatransferscenariosspansupported-offload-data-transfer-scenarios"></a><span id="Supported_Offload_Data_Transfer_Scenarios"></span><span id="supported_offload_data_transfer_scenarios"></span><span id="SUPPORTED_OFFLOAD_DATA_TRANSFER_SCENARIOS"></span>支持的卸载数据传输方案

在 HYPER-V 存储堆栈和 Windows SMB 文件服务器中提供的卸载操作的支持。 在后备物理存储支持 ODX 操作，调用方可以发出[ **FSCTL\_卸载\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-read)并[ **FSCTL\_卸载\_编写**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-write)到驻留在 Vhd 上或远程文件共享上，文件是从虚拟机中还是在物理硬件上。 下图说明的卸载的数据传输的最基本支持的源和目标。

![卸载数据传输方案](images/odx-scenario-3.png)

## <a name="span-idfilesystemfilteropt-inmodelandimpacttoapplicationsspanspan-idfilesystemfilteropt-inmodelandimpacttoapplicationsspanspan-idfilesystemfilteropt-inmodelandimpacttoapplicationsspanfile-system-filter-opt-in-model-and-impact-to-applications"></a><span id="File_System_Filter_Opt-In_Model_and_Impact_to_Applications"></span><span id="file_system_filter_opt-in_model_and_impact_to_applications"></span><span id="FILE_SYSTEM_FILTER_OPT-IN_MODEL_AND_IMPACT_TO_APPLICATIONS"></span>文件系统筛选器选择模型和对应用程序的影响


筛选器管理器，从 Windows 8 开始，若要指定为受支持的功能的卸载功能的筛选器。 如果卸载某项操作受支持或不; 统称为可以确定连接到此卷的文件系统筛选器如果不是，操作将失败并返回相应的错误代码。

筛选器必须指示它支持[ **FSCTL\_卸载\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-read)并[ **FSCTL\_卸载\_编写** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-write)通过注册表**DWORD**名为值**SupportedFeatures**，它位于驱动程序服务定义的注册表中： HKEY\_本地\_机器\\系统\\CurrentControlSet\\Services\\&lt;筛选器驱动程序名称&gt;\\。 此值包含 bits，确定哪些功能是选择中，并应在筛选器安装过程中设置的位域。

目前的定义的位均为：

| Flag                                               | 含义                               |
|----------------------------------------------------|---------------------------------------|
| 支持\_FS\_功能\_卸载\_读取的 0x00000001  | 筛选器支持 FSCTL\_卸载\_读取  |
| 支持\_FS\_功能\_卸载\_写 0x00000002 | 筛选器支持 FSCTL\_卸载\_编写 |

 

筛选器选择模型可以启用或禁用基于 HKEY 中存在的值\_本地\_MACHINE\\系统\\CurrentControlSet\\控制\\FileSystem\\FilterSupportedFeaturesMode 注册表项，具有以下值：

| FilterSupportedFeaturesMode 值 | 含义                                                                             |
|-----------------------------------|-------------------------------------------------------------------------------------|
| 0 （默认值）                       | 执行操作正常参加处理。                                                        |
| 1                                 | 永远不会参加 （等效于设置为 0 上的所有筛选器 SupportedFeatures 附加） |

 

### <a name="span-idtestingspanspan-idtestingspanspan-idtestingspantesting"></a><span id="Testing"></span><span id="testing"></span><span id="TESTING"></span>测试

若要检查堆栈的受支持的功能，没有 fltmc 实用程序中的更新的命令。 运行**fltmc 实例 – v\[卷\]:** 作为提升的用户，并检查*SprtFtrs*列。 如果*SprtFtrs*筛选器的值设置为 0，则意味着该筛选器正在阻止此卷上的卸载。 如果*SprtFtrs*字段设置为 3，支持这两个卸载操作。

### <a name="span-idcheckingfeaturesupportinirpprocessingspanspan-idcheckingfeaturesupportinirpprocessingspanspan-idcheckingfeaturesupportinirpprocessingspanchecking-feature-support-in-irp-processing"></a><span id="Checking_Feature_Support_in_IRP__Processing"></span><span id="checking_feature_support_in_irp__processing"></span><span id="CHECKING_FEATURE_SUPPORT_IN_IRP__PROCESSING"></span>检查 IRP 处理中支持的功能

作为 IRP 处理的一部分[ **FsRtlGetSupportedFeatures** ](https://msdn.microsoft.com/library/windows/hardware/hh920378)例程检索聚合**SupportedFeatures**状态的所有筛选器附加到给定卷堆栈。 组件，如 I/O 管理器和 SRV (SMB) 调用来验证此例程**SupportedFeatures**在堆栈上的所有筛选器的状态。 回滚其自己的组件卸载 Irp 应调用此函数可验证选择支持该操作。

### <a name="span-idconsiderationsforfilterdriversspanspan-idconsiderationsforfilterdriversspanspan-idconsiderationsforfilterdriversspanconsiderations-for-filter-drivers"></a><span id="Considerations_for_Filter_Drivers"></span><span id="considerations_for_filter_drivers"></span><span id="CONSIDERATIONS_FOR_FILTER_DRIVERS"></span>有关筛选器驱动程序的注意事项

卸载的数据传输是在数据中心中移动数据的新方法。 由于卸载逻辑核心复制引擎中的集成，默认情况下的许多应用程序会执行卸载的数据移动，而无需显式选择加入的功能。 因此，筛选器开发人员需要了解这些新操作如何影响筛选器。 不完全了解这些操作或不计算新数据可能导致不一致或损坏会导致数据的方案流。 以下列表总结了一的组项的筛选器开发人员需要特别注意的与卸载的操作：

-   了解新的数据流、 对筛选器和筛选器能够支持这些卸载的操作的影响。
-   更新筛选器安装程序，以添加 REG\_DWORD 值**SupportedFeatures** hklm\\系统\\CurrentControlSet\\Services\\ \[筛选器\]子项。 初始化，以便指定卸载功能。
-   对于想要对其执行操作的筛选器卸载操作、 更新注册到**IRP\_MJ\_文件\_系统\_控制**来处理[ **FSCTL\_卸载\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-read)并[ **FSCTL\_卸载\_编写**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-write)。
-   阻止卸载的操作所需的筛选器返回状态代码状态\_不\_支持从筛选器中。 不依赖注册表值以强制执行阻止卸载操作，因为最终用户可以更改它。 筛选器应显式允许或禁止卸载操作。

## <a name="span-idcopytokensspanspan-idcopytokensspanspan-idcopytokensspancopy-tokens"></a><span id="Copy_Tokens"></span><span id="copy_tokens"></span><span id="COPY_TOKENS"></span>复制令牌


与卸载操作的文件数据是未检测到 I/O 堆栈。 相反，它被视为是逻辑的代理服务器的数据的 512 字节令牌。 此令牌为特定于供应商的格式生成的存储子系统的不透明和唯一字符串，也可以是一个已知的类型来表示数据 （如逻辑上等同于零的数据范围） 的模式。 对令牌的代理的数据的修改将会导致使无效令牌，或为存储子系统，以保留某些供应商特定的原始数据意味着 (例如通过快照机制)。 后续卸载读取请求的文件中指定范围内唯一的令牌中的结果。

有一些标记，表示一种模式是定义完善的数据的类。 最常见的已知令牌是零令牌等效于零。 当令牌被定义为熟知令牌**TokenType**中的成员**存储\_卸载\_令牌**结构将设置为存储\_卸载\_令牌\_类型\_良好\_已知。 当设置此字段时， **WellKnownPattern**成员确定哪种模式的数据标记为。

-   当**WellKnownPattern**字段设置为存储\_卸载\_模式\_零个或存储\_卸载\_模式\_零\_与\_保护\_信息，它表示零令牌。 返回此令牌时[ **FSCTL\_卸载\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-read)操作，它指示包含所需的文件范围内的数据为逻辑上等同于零。 当此令牌提供给[ **FSCTL\_卸载\_编写**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-write)操作，它指示要写入到的文件所需的范围应逻辑上归零。
-   非零标记有当前定义的任何其他熟知令牌的模式。 不建议用户定义其自己熟知令牌模式。

## <a name="span-idtruncationspanspan-idtruncationspanspan-idtruncationspantruncation"></a><span id="Truncation"></span><span id="truncation"></span><span id="TRUNCATION"></span>截断


与 Windows 进行通信的基础存储子系统可以处理更少了中的卸载操作所需的数据。 这称为截断。 支持卸载读取，这意味着返回的令牌表示的数据的较小的值，请求的范围。 这将由**TransferLength**中的成员[ **FSCTL\_卸载\_读取\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_output)结构，它是从要读取的文件的范围开始处的字节数。 对于卸载写截断指示超过了所需编写较少的数据。 这将由**LengthWritten**中的成员[ **FSCTL\_卸载\_编写\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_write_output)结构，它是从要写入的文件的范围开始处的字节数。 命令处理或限制中较大的区域，在堆栈中的错误导致截断。

有两种情况下读取或写入 NTFS 截断要进行卸载的范围：

1.  复制范围将被截断为有效的数据长度 (VDL) 如果 VDL 低于结尾的文件 (EOF)。 这将假定，VDL 与逻辑扇区边界对齐，否则请参阅方案。

    ![vdl eof 之前出现](images/odx-vdl-1.png)

    期间[ **FSCTL\_卸载\_读取**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-read)操作，该标志卸载\_读取\_标志\_所有\_零\_超出\_当前\_中设置范围[ **FSCTL\_卸载\_读取\_输出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsctl_offload_read_output) ，该值指示结构该文件的剩余部分包含零，并且**TransferLength**成员将被截断为 VDL。

2.  类似于方案 1 中，但当 VDL 未对齐到逻辑扇区边界，所需范围由 NTFS 截断为下一个逻辑扇区边界。

    ![vdl 扇区边界与未对齐](images/odx-vdl-2.png)

## <a name="span-idlimitationsspanspan-idlimitationsspanspan-idlimitationsspanlimitations"></a><span id="Limitations"></span><span id="limitations"></span><span id="LIMITATIONS"></span>限制


-   卸载支持仅在 NTFS 卷上的操作。
-   卸载支持的操作的远程文件服务器的远程共享是否 NTFS 卷，如果服务器正在运行 Windows Server 2012 （假设远程堆栈还支持卸载操作）。
-   NTFS 不支持的卸载 FSCTLs 执行使用 Bitlocker 或 NTFS 加密 (EFS)、 执行重复数据删除的文件、 压缩的文件、 驻留的文件、 稀疏文件加密的文件或文件参与 TxF 事务。
-   NTFS 不支持的卸载 FSCTLs volsnap 快照中的文件执行。
-   如果所需的文件范围未对齐到源设备上的逻辑扇区大小或所需的文件范围是目标设备上的逻辑扇区大小未对齐，NTFS 将失败卸载 FSCTL。 这遵循非缓存 IO 的语义相同。
-   目标文件必须是预分配 (**SetEndOfFile**而不**SetAllocation**) 之前[ **FSCTL\_卸载\_写**](https://docs.microsoft.com/windows-hardware/drivers/ifs/fsctl-offload-write).
-   在处理卸载读取和卸载写入时，首先调用 NTFS [ **CcCoherencyFlushAndPurgeCache** ](https://msdn.microsoft.com/library/windows/hardware/ff539032)提交任何修改系统缓存中的数据。 这是相同的语义为非缓存 IO。

 

 




