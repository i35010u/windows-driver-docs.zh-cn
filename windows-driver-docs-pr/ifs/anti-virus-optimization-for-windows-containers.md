---
title: 用于 Windows 容器的防病毒优化
description: 本主题中描述的防病毒产品可以利用 Windows 容器中运行时的优化。
ms.assetid: 101BC08B-EE63-4468-8B12-C8C8B0E99FC5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9b5552ba5db2b5e4ad041ecf2d07e382238d0af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322287"
---
# <a name="span-idifskanti-virusoptimizationforwindowscontainersspananti-virus-optimization-for-windows-containers"></a><span id="ifsk.anti-virus_optimization_for_windows_containers"></span>用于 Windows 容器的防病毒优化


**适用于：**
-   Windows 10 版本 1607
-   Windows Server 2016
-   在主机上运行的防病毒产品

本主题中描述的防病毒产品可以利用以避免陈旧 Windows 容器文件的电子邮件，帮助改进容器启动时间的优化。

## <a name="span-idcontaineroverviewspanspan-idcontaineroverviewspanspan-idcontaineroverviewspancontainer-overview"></a><span id="Container_overview"></span><span id="container_overview"></span><span id="CONTAINER_OVERVIEW"></span>容器概述


Windows 容器功能旨在简化分发和部署应用程序。 有关详细信息，请参阅简介[Windows 容器](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)。

容器是从任意数量的包层构造的。 Windows 基本操作系统程序包窗体的第一层。

每个容器都有一个独立的卷表示该容器的系统卷。 容器隔离筛选器 (**wcifs.sys**) 提供了包到此容器的卷上的图层的虚拟叠加。 被实现在覆盖区上的使用 （重新分析点） 的占位符。 该卷将植入占位符之前容器第一次访问 overlain 的路径。 读取的文件会被定向到支持包文件的占位符。 这种方式在多个容器卷可以访问同一个基础包文件数据流。

如果容器修改一个文件，隔离筛选器执行写入时复制，并使用包文件的内容替换占位符。 这将中断到该特定容器的包文件"链接"。

## <a name="span-idreadredirectionspanspan-idreadredirectionspanspan-idreadredirectionspanread-redirection"></a><span id="Read_redirection"></span><span id="read_redirection"></span><span id="READ_REDIRECTION"></span>读取重定向


从占位符文件的读取会重定向到相应的包层隔离筛选器。 在筛选器的级别执行重定向。 下面的 AV 范围是筛选器，因为 AV 筛选器不会读取重定向。 AV 也不会执行，以设置重定向的包文件的打开。

AV 筛选器也有容器系统卷上的所有操作的完整视图。 它会看到对占位符文件，以及文件修改或新文件添加的操作。

## <a name="span-idredundantscanningproblemspanspan-idredundantscanningproblemspanspan-idredundantscanningproblemspanredundant-scanning-problem"></a><span id="Redundant_scanning_problem"></span><span id="redundant_scanning_problem"></span><span id="REDUNDANT_SCANNING_PROBLEM"></span>冗余扫描问题


可能会根据相同的包层的多个容器。 给定的包文件在同一数据流将多个容器的系统卷上的占位符为提供数据。 因此，可能会为每个容器中的相同数据的冗余 AV 扫描。 这对容器的性能有不必要的负面影响。 假设容器需要快速启动和可能是短暂性的这是 signification 成本。

## <a name="span-idrecommendedapproachspanspan-idrecommendedapproachspanspan-idrecommendedapproachspanrecommended-approach"></a><span id="Recommended_approach"></span><span id="recommended_approach"></span><span id="RECOMMENDED_APPROACH"></span>建议的方法


若要避免在容器上的冗余扫描建议 AV 产品修改其行为，如下所述。 负责 AV 产品，以确定向其客户对于这种方法的风险/奖励权益。 有关详细信息，请参阅[好处和风险](#benefits-risks)。

### <a name="span-id1packageinstallspanspan-id1packageinstallspanspan-id1packageinstallspan1-package-install"></a><span id="1._Package_install"></span><span id="1._package_install"></span><span id="1._PACKAGE_INSTALL"></span>1.包安装

在包安装期间管理工具将布置层根目录下的包中的文件。 AV 筛选器应继续扫描的文件，如在被放入的包根目录和正常运行。 这可确保所有层中的文件最初是相对于恶意软件清除。

### <a name="span-id2containstartandexecutionspanspan-id2containstartandexecutionspanspan-id2containstartandexecutionspan2-container-start-and-execution"></a><span id="2._Contain_start_and_execution"></span><span id="2._contain_start_and_execution"></span><span id="2._CONTAIN_START_AND_EXECUTION"></span>2.容器启动和执行

用于容器的卷的实时扫描，Av 应扫描中来避免冗余。 占位符文件需要考虑一些特殊事项。 因此冗余扫描并不是问题，修改按容器或容器中创建的新文件的文件未被重定向。

若要避免冗余扫描，AV 筛选器首先需要确定容器卷和这些卷上的占位符。 由于各种原因而 AV 筛选器来查询给定的文件是否占位符文件卷是容器卷，或者没有直接的方法。 隔离筛选器 （某些应用程序执行表现不正确，如果他们知道他们所访问的重新分析点） 的应用程序兼容性原因隐藏占位符重分析点。 此外，卷是容器卷容器正在运行时。 容器可能已停止，而且该卷可能仍存在重新装载。 相反，在预创建、 AV 筛选器必须查询以确定它容器的上下文中正在打开的文件对象。 然后可以将附加和 ECP 进行创建和接收创建完成后的占位符状态。

以下更改是 AV 产品中的需求：

-   **在预先创建容器卷上，将 ECP 附加到将接收的占位符信息创建 CallbackData 中。** 这些创建可以通过查询中的文件对象使用的接收器参数标识**IoGetSiloParameters**。 请注意筛选器必须指定的大小以**WCIFS\_重定向\_ECP\_上下文**结构。 所有其他字段都是找出如果确认在 ECP 设置的字段。

-   **在创建后，如果确认在 ECP，检查 ECP 重定向标志。** 这些标志将指示打开已提供服务，从包层或暂存根 （新的或修改文件）。 如果注册包层以及是否为远程，还能够指明标志。

    -   对于远程层提供服务的打开、 AV 应跳过扫描文件。 这会指示通过重定向标志：

        `WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_LAYER && WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_REMOTE_LAYER`

        可以假定远程层已扫描远程主机上。 HYPER-V 容器包是远程连接到实用工具 VM 托管容器。 这些包将会扫描通常的 HYPER-V 主机上通过 SMB 上的 VM 环回实用工具进行访问时。

        由于 VolumeGUID 和 FileId 不适用于通过远程，因此不会设置这些字段。

    -   对于从已注册的层提供服务的打开、 AV 应跳过扫描文件。 这会指示通过重定向标志：

        `WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_LAYER        &&  WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_REGISTERED_LAYER`

        在包安装期间和签名更新后，应以异步方式扫描已注册的层。

        **请注意**  已注册层可能不能识别的系统在将来。 在这种情况下，本地层文件必须单独进行标识最后一个项目符号中所述。

         

    -   对于从本地包层提供服务的随即打开，AV 应使用提供 VolumeGUID 和 FileId 层文件以确定是否需要扫描该文件。 这可能需要 AV 用于生成按卷 GUID 和 FileId 进行索引扫描的文件的缓存。 通过重定向标记来表示：

        `WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_LAYER`

    -   对于新的/修改文件暂存位置，AV 产品应扫描的文件并执行其正常的修正。 通过重定向标记来表示：

        `WCIFS_REDIRECTION_FLAGS_CREATE_SERVICED_FROM_SCRATCH`

        由于存在这种情况下不层文件，因此，系统将不设置 VolumeGUID 和 FileId。

-   **不将保存其流的上下文中的永久标记为"此文件提供服务层从"。** 创建后可修改从层根最初提供服务的文件。 在这种情况下，可能指示后续创建的同一个文件提供服务从容器卷创建。 AV 筛选器需要了解，发生这种情况。

## <a name="span-iddontusethelayerrootlocationsregistrykeyspanspan-iddontusethelayerrootlocationsregistrykeyspanspan-iddontusethelayerrootlocationsregistrykeyspandont-use-the-layerrootlocations-registry-key"></a><span id="Don_t_use_the_LayerRootLocations_registry_key"></span><span id="don_t_use_the_layerrootlocations_registry_key"></span><span id="DON_T_USE_THE_LAYERROOTLOCATIONS_REGISTRY_KEY"></span>不要使用 LayerRootLocations 注册表项


在过去，我们建议使用`LayerRootLocations`注册表项以获取基本映像的位置。 AV 产品不应再使用此注册表项。 相反，使用本主题中的建议的方法以避免冗余扫描。

已使用注册包层注册表位置：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\Virtualization\LayerRootLocations`

## <a name="span-idbenefits-risksspanspan-idbenefits-risksspanbenefits-and-risks"></a><span id="benefits-risks"></span><span id="BENEFITS-RISKS"></span>优势和风险


请考虑以下好处和风险的 AV 产品中使用这些新的优化。

### <a name="span-idbenefitsspanspan-idbenefitsspanspan-idbenefitsspanbenefits"></a><span id="Benefits"></span><span id="benefits"></span><span id="BENEFITS"></span>优势

-   对容器启动或执行时间 （甚至适用于第一个容器中） 没有任何影响。
-   可避免扫描的多个容器中的相同内容。
-   适用于 Windows Server 容器。 HYPER-V 容器，这适用于包，但需要为运行容器的额外的工作。 

### <a name="span-idrisksspanspan-idrisksspanspan-idrisksspanrisks"></a><span id="Risks"></span><span id="risks"></span><span id="RISKS"></span>风险

如果启动一个容器在签名之间的时间更新并在下一个计划主动的反恶意软件扫描，容器中执行的文件未扫描相对于最新的反恶意软件签名。 若要缓解此风险，AV 产品无法扫描的重定向文件只有当跳过最后一个主动扫描以来，尚未签名更新。 这将限制容器性能下降，直到主动扫描已完成，但最新的签名。 （可选） AV 产品可以触发主动扫描在此情况下，以便后续容器启动的效率更高。

 

 




