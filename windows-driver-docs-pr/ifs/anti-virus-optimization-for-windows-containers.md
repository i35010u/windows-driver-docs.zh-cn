---
title: 用于 Windows 容器的防病毒优化
description: 本主题介绍防病毒产品在 Windows 容器中运行时可使用的优化。
ms.assetid: 101BC08B-EE63-4468-8B12-C8C8B0E99FC5
ms.date: 03/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: cb32050e0171207446f461cdbf31d24d1c0d8092
ms.sourcegitcommit: 5e5f3491e29f99b11a12b45da870043e0e92ddc5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86949031"
---
# <a name="anti-virus-optimization-for-windows-containers"></a>用于 Windows 容器的防病毒优化

**此页上的信息适用于：**
- Windows 10 版本1607及更高版本
- Windows Server 2016 及更高版本
- 主机上运行的防病毒（AV）产品

本主题介绍 AV 产品可用于避免对 Windows 容器文件的冗余扫描，并帮助改进容器启动时间的优化。

## <a name="container-overview"></a>容器概述

Windows 容器功能旨在简化应用程序的分发和部署。 有关详细信息，请参阅[Windows 容器](https://docs.microsoft.com/virtualization/windowscontainers/about/about_overview)简介。

从任意数量的包层构造容器。 Windows 基本操作系统包构成第一层。

每个容器都有一个独立的卷，它表示该容器的系统卷。 容器隔离筛选器（*wcifs.sys*）可将包层的虚拟覆盖到此容器卷上。 使用占位符（重新分析点）实现覆盖。 该卷在容器第一次访问 overlain 路径之前带有占位符。 占位符文件的读取被定向到后备包文件。 通过这种方式，多个容器卷可以访问相同的基础包文件数据流。

如果容器修改文件，隔离筛选器将执行写入时复制，并将占位符替换为包文件的内容。 这会将 "链接" 拆分为该特定容器的包文件。

## <a name="read-redirection"></a>读取重定向

隔离筛选器会将对占位符文件的读取重定向到适当的包层。 重定向在筛选器级别执行。 由于筛选器低于 AV 范围，因此 AV 筛选器将不会看到读取重定向。 AV 也不会看到为设置重定向而执行的包文件的打开。

AV 筛选器确实具有容器系统卷上所有操作的完整视图。 它会查看占位符文件上的操作以及文件修改或添加新的文件。

## <a name="redundant-scanning-problem"></a>冗余扫描问题

可能会有多个容器，具体取决于相同的包层。 给定包文件的相同数据流将为多个容器系统卷上的占位符提供数据。 因此，对于每个容器中的相同数据，都有可能进行冗余 AV 扫描。 对于容器的性能，这会产生不必要的负面影响。 这是一种 signification 的成本，因为容器预计会迅速启动，而且可能会缩短生存期。

## <a name="recommended-approach"></a>推荐的方法

为了避免在容器上进行冗余扫描，建议 AV 产品按如下所述修改其行为。 这取决于 AV 产品，为其客户确定此方法的风险/回报权益。 有关详细信息，请参阅本页底部的**权益和风险**部分。

### <a name="1-package-install"></a>1. 包安装

在包安装期间，管理工具将在层根下对包中的文件进行布局。 AV 筛选器应在文件放在包根目录中时继续扫描文件，这通常是这样。 这可确保层中的所有文件最初都与恶意软件有关。

### <a name="2-container-start-and-execution"></a>2. 容器启动和执行

对于容器卷的实时扫描，AVs 应以避免冗余的方式进行扫描。 占位符文件需要特别注意。 容器修改的文件或在容器中创建的新文件不会重定向，因此不需要进行冗余扫描。

为了避免冗余扫描，AV 过滤器首先需要识别这些卷上的容器卷和占位符。 由于各种原因，AV 过滤器无直接的方法来查询卷是否为容器卷，或者给定文件是否为占位符文件。 隔离筛选器出于应用程序兼容性原因隐藏了占位符重新分析点（某些应用程序意识到访问重新分析点时的行为不正确）。 此外，在容器运行时，卷只是容器卷。 容器可能已停止，卷可能仍在重新装入。 相反，在预创建中，AV 筛选器必须查询文件对象，以确定是否在容器的上下文中打开它。 然后，可以将和 ECP 附加到创建，并在创建完成时接收占位符状态。

AV 产品中需要进行以下更改：

- **在容器卷上预先创建的过程中，将 ECP 附加到将接收占位符信息的创建 CallbackData。** 可以通过使用**IoGetSiloParameters**从 fileobject 中查询接收器参数来识别这些创建。 请注意，筛选器必须在**WCIFS_REDIRECTION_ECP_CONTEXT**结构中指定大小。 如果已确认 ECP，则所有其他字段均设置为 out。

- **在 "创建后" 中，如果已确认 ECP，请检查 ECP 重定向标志。** 标志将指示是从包层还是从临时根（新文件或已修改的文件）为打开的服务。 标志还会指示包层是否已注册以及它是否为远程。

  - *对于从远程层提供服务的打开*，AV 应跳过扫描文件。 重定向标志表明这一点：`WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_LAYER && WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_REMOTE_LAYER`

    可以假定远程层已在远程主机上进行扫描。 Hyper-v 容器包与托管容器的实用工具 VM 远程。 当实用工具 VM 通过 SMB 环回对这些包进行访问时，它们将在 Hyper-v 主机上正常扫描。

    由于 VolumeGUID 和 FileId 不适用于远程，因此将不会设置这些字段。

  - *对于从已注册层提供服务的打开*，AV 应跳过扫描文件。 重定向标志表明这一点：`WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_LAYER &&  WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_REGISTERED_LAYER`

    包安装期间和签名更新之后，应以异步方式扫描已注册的层。

    >[!NOTE]
    > 将来，系统可能不会标识已注册的层。 在这种情况下，必须对本地层文件进行单独标识，如最后一个项目符号中所述。

  - *对于从本地包层提供服务的打开*，AV 应使用所提供的层文件的 VolumeGUID 和 FileId 来确定是否需要扫描该文件。 这可能需要 AV 构建按卷 GUID 和 FileId 索引的扫描文件的缓存。 重定向标志表明这一点：`WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_LAYER`

  - *对于暂存位置中的新文件/修改后的文件*，AV 产品应该扫描文件并执行其常规的修正。 重定向标志表明这一点：`WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_SCRATCH`

    由于在这种情况下没有层文件，因此将不设置 VolumeGUID 和 FileId。

  - 请勿将 "此文件从层服务作为其流上下文中的永久标记进行服务"。 在创建后，可以修改从层根最初提供服务的文件。 在这种情况下，同一文件的后续创建可能表示正在从容器卷为创建提供服务。 AV 过滤器需要了解这种情况可能发生。

## <a name="dont-use-the-layerrootlocations-registry-key"></a>请勿使用 LayerRootLocations 注册表项

过去，我们建议使用 `LayerRootLocations` 注册表项来获取基本映像的位置。 AV 产品不应再使用此注册表项。 相反，请使用本主题中建议的方法来避免冗余扫描。

已用于注册包层的注册表位置：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Virtualization\LayerRootLocations`

## <a name="benefits-and-risks"></a>优点和风险

为 AV 产品使用这些新的优化时，请考虑以下好处和风险。

### <a name="benefits"></a>优势

- 不影响容器的开始或执行时间（即使是第一个容器）。
- 避免在多个容器中扫描相同的内容。
- 适用于 Windows Server 容器。 对于 Hyper-v 容器，这适用于包，但需要额外的工作来运行容器。

### <a name="risks"></a>风险

如果在签名更新和下一次计划的主动反恶意软件扫描之间的时间启动容器，则在容器中执行的文件将不会扫描到最新的反恶意软件签名。 为了降低这种风险，AV 产品只有自上次主动扫描后尚未进行签名更新，才能跳过对重定向文件的扫描。 这会限制容器性能降低，直到使用最新的签名完成主动扫描为止。 在这种情况下，AV 产品可以根据需要触发主动扫描，以便后续的容器启动更有效率。
