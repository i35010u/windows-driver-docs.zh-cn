---
title: 威胁建模，驱动程序
description: 驱动程序编写人员和架构师应进行威胁建模的任何驱动程序的设计过程的组成部分。 本文提供有关创建威胁模型对于 Microsoft Windows 系列操作系统的驱动程序的指南。
ms.assetid: 77FB242E-A07C-4298-80ED-866F8D80118C
ms.date: 06/27/2018
ms.localizationpriority: medium
ms.openlocfilehash: b4a5479671ebb9a7cd00bada0b60450895891de5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522954"
---
# <a name="threat-modeling-for-drivers"></a>威胁建模，驱动程序

驱动程序编写人员和架构师应进行威胁建模的任何驱动程序的设计过程的组成部分。 本主题提供有关创建威胁模型对于 Windows 驱动程序的指南。

安全性应是任何驱动程序的基本设计点。 任何成功的产品是目标。 如果要为 Windows 编写驱动程序，您必须假定，一段时间，在某处，有人将尝试使用您的驱动程序危及系统安全。

设计安全的驱动程序包括：

-   识别驱动程序可能易受攻击的点。
-   正在分析可安装在每个此类点的攻击的类型。
-   确保该驱动程序旨在方式可防止此类攻击。

威胁建模是这些重要的设计任务的结构化的方法。 威胁模型是一种分类和分析威胁到资产。 从驱动程序编写者的角度来看，所用资产是硬件、 软件和网络的计算机上的数据。

威胁模型回答以下问题：

-   哪些资产需要保护？
-   到哪些威胁是易受攻击的资产？
-   如何重要或可能是每个威胁？
-   如何消除威胁？

威胁建模是软件设计的重要组成部分，因为它可确保安全是内置于产品，而不是以事后才进行寻址。 良好的威胁模型可以帮助您查找和防止设计过程中的 bug，从而消除了可能会严重影响修补程序的更高版本以及可能对你的组织的声誉受损。

本部分适用的威胁建模到驱动程序设计原则，并提供示例的驱动程序可能会受到影响的威胁。 有关威胁建模为软件设计的更完整说明，请参阅这些资源。

-   Microsoft SDL 网站：

    <https://www.microsoft.com/sdl>

-   Microsoft SDL 的简化的实现：

    [下载白皮书](https://go.microsoft.com/?linkid=9708425)

-   此博客文章介绍如何下载的免费副本*安全开发生命周期：SDL*，作者为 Michael Howard 和 Steve Lipner:

    <https://blogs.msdn.microsoft.com/microsoft_press/2016/04/19/free-ebook-the-security-development-lifecycle/>


## <a name="span-idcreateathreatmodelspanspan-idcreateathreatmodelspanspan-idcreateathreatmodelspancreate-threat-models-for-drivers"></a><span id="Create_a_threat_model"></span><span id="create_a_threat_model"></span><span id="CREATE_A_THREAT_MODEL"></span>创建驱动程序的威胁模型

创建威胁模型需要全面了解驱动程序的设计、 类型的威胁到可能会公开该驱动程序，以及利用特定威胁的安全攻击的后果。 创建驱动程序的威胁模型后，您可以确定如何减少潜在威胁。

威胁建模是在驱动程序设计过程中，而不是随意在编码期间执行的方式组织，结构化时最有效。 结构化的方法会增加你会发现漏洞在设计中，从而有助于确保模型全面的可能性。

组织风险建模工作的一种方法是执行以下步骤：

1.  创建结构化关系图显示通过驱动程序的数据流。 包括驱动程序执行的所有可能的任务的源和目标的所有输入和输出进行驱动程序。 正式数据流关系图或类似结构化关系图中，可以帮助您分析的数据通过您的驱动程序的路径，并能够确定驱动程序的外部接口、 边界和交互。 
2.  分析基于数据流关系图的潜在安全威胁。
3.  评估您在上一步中标识的威胁，并确定如何缓解这些问题。

## <a name="span-idcreateadataflowdiagramspanspan-idcreateadataflowdiagramspanspan-idcreateadataflowdiagramspancreate-a-data-flow-diagram"></a><span id="Create_a_data_flow_diagram"></span><span id="create_a_data_flow_diagram"></span><span id="CREATE_A_DATA_FLOW_DIAGRAM"></span>创建数据流关系图

驱动程序与它进行交互的外部实体之间的数据流在概念窗体中显示数据流关系图-通常在操作系统中，一个用户的过程和设备。 正式数据数据流关系图使用以下符号：

![符号](images/dataflowdiagramsymbols.gif)

下图显示了示例数据流关系图假设内核模式的 Windows 驱动程序模型 (WDM) 驱动程序。 无论你的特定类型的驱动程序的体系结构、 概念模型是相同： 显示所有数据路径并确定每个进入或退出该驱动程序的数据源。

![假设的内核模式驱动程序的示例数据数据流关系图](images/sampledataflowdiagramkernelmodedriver.gif)

**请注意**  上图显示了用户进程和驱动程序，之间直接流动的数据并省略中间的任何驱动程序。 但是，实际上，所有请求通过 I/O 管理器，并且可能会在到达特定驱动程序之前经过一个或多个更高级别的驱动程序。 该图将忽略这些中间步骤来强调数据的原始源和提供数据的线程上下文的重要性。 内核模式驱动程序必须验证源自在用户模式下的数据。

信息从操作系统请求从用户的进程，因为请求进入该驱动程序或请求 （通常会中断） 从设备。

上图中的驱动程序从多个类型的请求中的操作系统接收数据：

-   请求驱动程序和其设备，通过调用执行管理任务**DriverEntry**， **DriverUnload**，并**AddDevice**例程
-   即插即用的请求 (IRP\_MJ\_PNP)
-   电源管理请求 (IRP\_MJ\_POWER)
-   内部设备 I/O 控制请求 (IRP\_MJ\_内部\_设备\_控件)

这些请求的响应，数据流从驱动程序返回到操作系统作为状态信息。 在图中的驱动程序将从以下类型的请求中的用户进程接收数据：

-   创建、 读取和写入请求 (IRP\_MJ\_创建、 IRP\_MJ\_读取或 IRP\_MJ\_编写)
-   公共设备 I/O 控制请求 (IRP\_MJ\_设备\_控件)

在响应这些请求，输出数据和状态信息从驱动程序返回到流用户进程。

最后，该驱动程序接收数据从设备由于设备 I/O 操作或更改设备状态的用户操作 （如打开 CD 驱动器上的送纸器）。 同样，该驱动程序中的数据流向设备在 I/O 操作和设备状态变化。

上图显示了驱动程序数据流向在广泛的概念级别。 每个圆圈表示相对较大的任务和缺少详细信息。 在某些情况下，如该示例的一个级别关系图是足够了解的数据源和路径。 如果您的驱动程序处理的 I/O 请求来自不同源的许多不同的类型，可能需要创建一个或多个其他图表，其中显示更多详细信息。 例如，可能会将标记为"处理 I/O 请求"的圆圈扩展到单独的关系图，类似于下图。

![扩展的数据流关系图的 i/o 请求](images/expandeddataflowdiagramiorequests.gif)

第二个图显示了第一个关系图中的每种类型的 I/O 请求的单独任务。 （为简单起见，到设备的数据路径已省略。）

外部实体和类型的输入和关系图所示的输出可能有所不同，具体取决于设备的类型。 例如，Windows 提供了许多常见的设备类型的类驱动程序。 系统提供的类驱动程序适用于供应商提供微型驱动程序，这通常是包含一组回调例程的动态链接库 (DLL)。 用户 I/O 请求将定向到的类驱动程序，后者随后调用微型驱动程序执行特定任务中的例程。 微型驱动程序通常不会收到整个 I/O 请求数据包作为输入;相反，每个回调例程只接收的数据所需的特定任务。

创建数据流关系图时，请记住不同的驱动程序请求的源。 用户的计算机运行任何代码可能生成 I/O 请求到驱动程序，从免费软件，获得共享件、 诸如 Microsoft Office 之类的已知应用程序和 Web 下载的潜在可疑来源。 具体取决于你的特定设备，你可能还需要考虑媒体编解码器或你的公司提供以支持其设备的第三方筛选器。 可能的数据源包括：

-   IRP\_MJ\_XXX 驱动程序处理的请求
-   Ioctl，该驱动程序定义或处理
-   该驱动程序调用的 Api
-   回调例程
-   该驱动程序公开的任何其他接口
-   该驱动程序读取或写入，包括那些在安装过程中使用的文件
-   该驱动程序读取或写入的注册表项
-   配置属性页和用户驱动程序使用提供的任何其他信息

您的模型还应该介绍驱动程序安装和更新过程。 包括所有文件、 目录和注册表项读取或写入在驱动程序安装过程。 此外请考虑在设备安装程序、 共同安装程序和属性页中公开的接口。

可能容易受到攻击的驱动程序交换数据与外部实体的任何点。

## <a name="span-idanalyzepotentialthreatsspanspan-idanalyzepotentialthreatsspanspan-idanalyzepotentialthreatsspananalyze-potential-threats"></a><span id="Analyze_potential_threats"></span><span id="analyze_potential_threats"></span><span id="ANALYZE_POTENTIAL_THREATS"></span>分析潜在威胁

确定驱动程序可能易受攻击的点后，可以确定哪些类型的威胁可能出现在每个点。 请考虑以下类型的问题：

-   可以保护的每个资源有何种安全机制？
-   所有转换和适当的安全设置的接口都？
-   一项功能的使用不当可能无意中危及安全性？
-   恶意使用的一项功能可能会损害安全性？
-   默认设置是否提供足够的安全性？

## <a name="span-idthestrideapproachspanspan-idthestrideapproachspanspan-idthestrideapproachspanthe-stride-approach-to-threat-categorization"></a><span id="The_STRIDE_approach"></span><span id="the_stride_approach"></span><span id="THE_STRIDE_APPROACH"></span>STRIDE 方法进行威胁分类

首字母缩写 STRIDE 介绍了六种类别的软件的威胁。 此首字母缩略词派生自：

-   **S**poofing
-   **T**ampering
-   **R**表示拒绝
-   **我**表示信息泄露
-   **D**表示拒绝服务
-   **E**表示特权提升

使用 STRIDE 作为指南，可能会带来的驱动程序可能会作为目标的攻击类型的详细的问题。 目标是确定的攻击者可以在驱动程序中每个容易点的类型，然后创建针对每个可能的攻击的方案。

-   **欺骗**正在使用其他人的凭据来访问无法访问资产。 一个过程通过传递伪造或被盗凭据装载欺骗攻击。
-   **篡改**变化的数据来发起攻击。 例如，驱动程序可能易受篡改如果必需的驱动程序文件不充分保护的驱动程序签名和访问控制列表 (Acl)。 在此情况下，恶意用户无法更改文件，从而破坏系统安全性。
-   **不可否认**用户拒绝执行某个操作，但操作的目标不包含任何方法来证实时发生。 如果它不会记录可能会损害安全性的操作，驱动程序可能会遭受否认性威胁。 例如，如果它不会记录请求，以更改其设备，例如焦点、 扫描的区域、 捕获映像的频率、 捕获的映像和等的目标位置的特征，视频设备的驱动程序可能是易受否认性。 生成的映像可能已损坏，但系统管理员必须确定哪些用户导致问题。
-   **信息泄露**威胁是完全按照其名称所示： 泄露到没有权限查看它的用户的信息。 任何驱动程序将传递到或从用户缓冲区的信息是易受信息泄漏威胁。 若要避免信息泄露威胁，驱动程序必须验证每个用户缓冲区的长度，并写入数据之前的零初始化的缓冲区。
-   **拒绝服务**攻击威胁到有效的用户可以访问资源。 资源可以是磁盘空间、 网络连接或物理设备。 攻击该性能降低到不可接受的程度也被视为拒绝服务攻击。 如果资源消耗会妨碍其他有效的用户能够执行其任务，可使用户进程以独占系统资源时不必要的驱动程序可能会遭受拒绝服务攻击。

    例如，驱动程序可能使用信号量的 IRQL 在执行时保护数据结构 = 被动\_级别。 但是，该驱动程序必须获取并释放信号量内的**KeEnterCriticalRegion/KeLeaveCriticalRegion**对，用于禁用并重新启用的异步过程调用 (Apc) 传递。 如果该驱动程序无法使用这些例程，APC 可能导致挂起线程保存信号量的操作系统。 因此，其他进程 （包括那些由管理员创建） 将不能访问结构。

-   **提升权限**如果无特权的用户获得特权的状态，则会发生攻击。 将传递用户模式下的内核模式驱动程序的句柄**ZwXxx**例程容易受到提升权限攻击因为**ZwXxx**例程绕过安全检查。 内核模式驱动程序必须验证每个句柄，它们接收来自用户模式下调用方。

    如果依赖于内核模式驱动程序，也会发生特权提升攻击**RequestorMode** IRP 标头来确定的 I/O 请求是否来自于内核模式或用户模式下调用方的值。 在来自网络或服务器服务 (SRVSVC) 的值的 Irp **RequestorMode**是**KernelMode**，无论请求的来源。 若要避免此类攻击，驱动程序必须访问控制检查为执行此类请求而不是只需使用的值**RequestorMode**。

## <a name="span-idanalysistechspanspan-idanalysistechspandriver-analysis-techniques"></a><span id="analysistech"></span><span id="ANALYSISTECH"></span>驱动程序分析技术

组织分析的简单方法是威胁的列出的每种类型的一个或多个方案的潜在威胁以及易受攻击的部分。

若要执行彻底的分析，必须了解在驱动程序中每个潜在易受攻击点威胁的可能性。 在每个易受攻击的时候，确定每个类别的可能是可能的威胁 （欺骗、 篡改、 否认、 信息泄露、 拒绝服务和特权提升）。 然后，创建一个或多个针对每个貌似合理的威胁的攻击方案。

例如，考虑 IRP 的数据流\_MJ\_设备\_控件请求在上图中所示。 下表显示了两种类型的驱动程序可能会遇到处理此类请求时的威胁：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">易受攻击的点</th>
<th align="left">潜在的威胁 (STRIDE)</th>
<th align="left">方案</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">IRP_MJ_DEVICE_CONTROL 请求</td>
<td align="left"><p>拒绝服务</p>
<p>提升权限</p></td>
<td align="left"><p>用户进程会发出一系列 Ioctl，导致设备故障。</p>
<p>用户进程发出允许 FILE_ANY_ACCESS IOCTL。</p></td>
</tr>
</tbody>
</table>

 
一种威胁通常与另一个。 例如，利用提升权限威胁的攻击可能导致信息泄露或拒绝服务。 此外，某些类型的攻击取决于一系列事件。 恶意用户可能会首先利用特权提升威胁。 然后，使用提升的权限所附带的添加功能，用户可能会查找并利用其他漏洞。

威胁树和概述了可以在建模这种复杂的情况下很有用。

威胁树是显示威胁或漏洞; 的一个层次结构关系图从本质上讲，威胁树模仿攻击的机会的恶意用户的步骤。 攻击的最终目标是在树的顶部。 每个从属级别显示了执行攻击所需的步骤。 下图是一个简单的威胁树中前面的示例中的拒绝服务方案。

![简单的威胁树](images/simplethreattree.gif)

威胁树显示所需的步骤来装载特定攻击以及两个步骤之间的关系。 大纲是威胁树的替代方法。

概述只列出了层次结构顺序的步骤特定威胁攻击。 例如：

1.0 会导致设备停止响应。

1.1 问题 IOCTL 失败序列中。

1.1.1 确定导致失败的设备的序列。

1.1.2 获得提升的权限才能发出内部 Ioctl。

两种方法之一可以帮助您了解哪些威胁是最危险，在设计中的漏洞都是最关键。

 

## <a name="span-idfastpaththreatmodelingspanspan-idfastpaththreatmodelingspanspan-idfastpaththreatmodelingspanfast-path-threat-modeling"></a><span id="Fast_path_threat_modeling"></span><span id="fast_path_threat_modeling"></span><span id="FAST_PATH_THREAT_MODELING"></span>快速路径威胁建模

如果资源有限的而不被创建完整的威胁模型关系图，可以创建摘要大纲来帮助你评估该驱动程序的安全风险。 例如下面的文本描述一些 diagramed 在上一示例中所述的示例驱动程序中的图面区域。

该驱动程序从多个类型的请求中的操作系统接收数据：

-   请求驱动程序和其设备，通过调用执行管理任务**DriverEntry**， **DriverUnload**，并**AddDevice**例程
-   即插即用的请求 (IRP\_MJ\_PNP)
-   电源管理请求 (IRP\_MJ\_POWER)
-   内部设备 I/O 控制请求 (IRP\_MJ\_内部\_设备\_控件)

这些请求的响应，数据流从驱动程序返回到操作系统作为状态信息。 该驱动程序将从以下类型的请求中的用户进程接收数据：

-   创建、 读取和写入请求 (IRP\_MJ\_创建、 IRP\_MJ\_读取或 IRP\_MJ\_编写)
-   公共设备 I/O 控制请求 (IRP\_MJ\_设备\_控件)

在响应这些请求，输出数据和状态信息从驱动程序返回到流用户进程。

使用此基本的流的数据了解到您的驱动程序，可以检查每个输入和输出区域中查找可能的威胁。



## <a name="span-idthedreadapproachspanspan-idthedreadapproachspanspan-idthedreadapproachspanthe-dread-approach-to-threat-assessment"></a><span id="The_DREAD_approach"></span><span id="the_dread_approach"></span><span id="THE_DREAD_APPROACH"></span>威胁评估 DREAD 方法

确定如何以及在何处驱动程序可能受到攻击是不够的。 然后必须评估这些潜在威胁、 确定其相对优先级，并设计缓解策略。 

DREAD 是描述了用于评估的软件的威胁的五个条件的首字母缩写。 DREAD 代表：

-   **D**损害
-   **R**再现
-   **E**xploitability
-   **一个**可用户
-   **D**iscoverability

若要确定对您的驱动程序的威胁的优先级，排名从 1 到 10 的每个威胁在全部 5 个 DREAD 评估条件，然后添加分数并除以 5 （条件数）。 结果是一个介于 1 和 10 中的每个威胁之间的数值分数。 最高得分指示严重的威胁。

-   **损坏**。 评估可能会导致从安全攻击造成损害显然是威胁建模的关键部分。 损坏可以包括数据丢失、 硬件或介质发生故障、 符合的性能或任何类似的度量值适用于你的设备和其运行环境。
-   **可再现性**是何种频率指定的类型的攻击将成功的度量值。 比较容易再现威胁是更有可能被利用比很少出现的漏洞或不可预测。 例如，默认情况下，安装或在每个潜在的代码路径中使用的功能的威胁是高度可重现的。
-   **可利用性指数**评估的工作量和发起攻击所需的专业知识。 威胁可能受到相对缺乏经验的大学生是高度可利用。 要求具备出色技能的人员和执行成本较高的攻击是可利用较低。

    在评估可利用性指数，还考虑潜在攻击者的数量。 可通过任何远程利用的威胁，匿名用户是多个需要现场、 高度授权的用户可利用。

-   **受影响的用户**。 可能会受到攻击的用户数是在评估威胁的另一个重要因素。 对此度量值，可能会影响最多一个或两个用户的攻击评价相对较低。 相反，崩溃网络服务器的拒绝服务攻击可能会影响成千上万的用户，并因此评价高得多。
-   **可发现性**威胁会被利用的可能性。 可发现性很难准确地估计。 最安全的方法是假定的任何漏洞将最终被利用的和，因此，依赖于其他度量值来建立威胁的相对分级。

**示例：使用 DREAD 评估威胁**

继续使用上文所述的示例下, 表显示了如何设计器可能评估假设的拒绝服务攻击：

| DREAD 条件 | 分数   | 备注                                                                |
|-----------------|---------|-------------------------------------------------------------------------|
| 损坏          | 8       | 暂时，会中断工作，但会导致不会永久损坏或数据丢失。 |
| 可再现性 | 10      | 会导致设备故障每次。                                   |
| 可利用性指数  | 7       | 需要花大力的气来确定命令序列。            |
| 受影响的用户  | 10      | 会影响市场上此设备的每个模型。                       |
| 可发现性 | 10      | 假定将发现每个潜在的威胁。                 |
| **总计：**      | **9.0** | **缓解此问题是高优先级。**                           |


**缓解威胁**


您的驱动程序设计应防止您的模型公开的所有威胁。 但是，在某些情况下，缓解可能不可行。 例如，考虑攻击可能会影响极少数用户和不太可能导致丢失数据或系统可用性。 如果缓解此类威胁需要几个月的额外工作，则可以合理地选择要花费更多时间，而测试驱动程序。 不过，请记住，最终的恶意用户是有可能发现安全漏洞并发起攻击，然后该驱动程序将需要一个修补程序的问题。



## <a name="span-idincludingthreatmodelinginabroadersecuritydevelopmentlifecycleprocessspanspan-idincludingthreatmodelinginabroadersecuritydevelopmentlifecycleprocessspanspan-idincludingthreatmodelinginabroadersecuritydevelopmentlifecycleprocessspanincluding-threat-modeling-in-a-broader-security-development-lifecycle-process"></a><span id="Including_threat_modeling_in_a_broader_Security_Development_Lifecycle__process"></span><span id="including_threat_modeling_in_a_broader_security_development_lifecycle__process"></span><span id="INCLUDING_THREAT_MODELING_IN_A_BROADER_SECURITY_DEVELOPMENT_LIFECYCLE__PROCESS"></span>包括威胁建模在更广泛的安全开发生命周期过程中

请考虑包括威胁建模过程中更广泛安全开发生命周期-SDL。

Microsoft SDL 过程提供了大量的推荐的软件开发过程，可以进行修改以适应任意大小的组织包括独立的开发人员。 请考虑将 SDL 建议的组件添加到软件开发过程。

有关详细信息，请参阅[Microsoft 安全开发生命周期 (SDL) – 过程指南](https://msdn.microsoft.com/library/84aed186-1d75-4366-8e61-8d258746bopq.aspx)。

**培训和组织功能**-实施软件开发安全培训，以展开识别和修正软件漏洞的能力。

Microsoft 对其四个核心 SDL 培训课程可供下载。 [Microsoft 安全开发生命周期核心培训课程](https://go.microsoft.com/?linkid=9708478)

有关 SDL 培训的更多详细信息，请参阅本白皮书。 [Microsoft sdl 项基本的软件安全培训](https://www.microsoft.com/download/details.aspx?id=9950)

**要求和设计**-生成受信任的软件的最佳机会是在初始规划阶段的新版本或新的版本，因为开发团队可以标识键对象并将安全和隐私，最大程度减少集成对计划和计划的中断。

在此阶段主要输出是设置特定的安全目标。 例如，在决定，所有代码应通过 Visual Studio 代码分析"所有规则"具有零个警告。

**实现**-所有开发团队应定义和发布已批准的工具和其关联的安全检查，如编译器/链接器选项和警告的列表。

驱动程序开发人员最有用是工作的在此阶段中。 为其编写代码评审的潜在漏洞。 如代码分析和驱动程序验证程序的工具用于寻找可以强制写入的代码中的区域。

**验证**-验证是软件具备完整且针对安全目标要求和设计阶段中所述测试的点。

其他工具例如 binscope 和模糊测试人员可用于验证安全设计目标均已满足，并且代码已准备好交付

**发布和响应**-在发布产品的准备，最好创建事件响应计划，用于描述将执行哪些操作来应对新威胁和它如何将服务后的驱动程序已发货。 提前此操作，则意味着你将能够更快响应如果已提供的代码中标识的安全问题。

有关 SDL 过程的详细信息，请参阅以下附加资源：

-   这是主要的 Microsoft SDL 网站，并提供的 SDL 概述。 <https://www.microsoft.com/sdl>

-   此博客介绍了如何下载的免费副本*安全开发生命周期：SDL*，作者为 Michael Howard 和 Steve Lipner。 <https://blogs.msdn.microsoft.com/microsoft_press/2016/04/19/free-ebook-the-security-development-lifecycle/>

-   此页提供指向其他 SDL 出版物。 <https://www.microsoft.com/SDL/Resources/publications.aspx>



## <a name="span-idcalltoactionspanspan-idcalltoactionspanspan-idcalltoactionspancall-to-action"></a><span id="Call_to_action"></span><span id="call_to_action"></span><span id="CALL_TO_ACTION"></span>行动号召

有关驱动程序开发人员：

-   使威胁建模驱动程序设计的一部分。
-   采取措施来有效地减轻驱动程序代码中的威胁。
-   熟悉适用于您的驱动程序和设备类型的安全性和可靠性问题。 有关详细信息，请参阅特定于设备的部分的 Windows 设备驱动程序工具包 (WDK)。
-   了解哪种检查操作系统、 I/O 管理器和任何更高级别的驱动程序执行用户请求到达您的驱动程序之前，并且它会检查它们不会执行。
-   使用从 WDK，如驱动程序验证程序进行测试和验证您的驱动程序的工具。
-   查看公共数据库的已知的威胁和软件漏洞。

其他驱动程序安全资源，请参阅[驱动程序安全核对清单](driver-security-checklist.md)。


## <a name="span-idresourcesspanspan-idresourcesspanspan-idresourcesspansoftware-security-resources"></a><span id="Resources"></span><span id="resources"></span><span id="RESOURCES"></span>软件安全资源

**丛书**

*编写安全代码*，第二版作者为 Michael Howard 和 David LeBlanc

*24 Deadly Sins 的软件安全：编程缺陷以及如何解决这些问题*，由 Michael Howard、 David LeBlanc 和 John viega 合著的第一版

*软件安全评估的艺术： 识别和防止出现软件漏洞*，作者标记 Dowd、 John McDonald 和 Justin Schuh

**Microsoft 硬件和驱动程序开发人员信息**

[常见驱动程序的可靠性问题](https://download.microsoft.com/download/5/7/7/577a5684-8a83-43ae-9272-ff260a9c20e2/drvqa.doc)白皮书

[取消 Windows 驱动程序中的逻辑](https://msdn.microsoft.com/library/windows/hardware/dn653289)白皮书

[Windows 安全模型： 需要知道的每个驱动程序编写器](windows-security-model.md)

**Microsoft Windows 驱动程序开发工具包 (DDK)**

请参阅[驱动程序的编程技术](https://msdn.microsoft.com/library/windows/hardware/ff544177)中[内核模式驱动程序体系结构](https://msdn.microsoft.com/library/windows/hardware/ff557560)

**测试工具**

请参阅[Windows 硬件实验室套件](https://msdn.microsoft.com/library/windows/hardware/dn930814)中[性能和兼容性测试](https://msdn.microsoft.com/windows/hardware/commercialize/test/index)

**已知的威胁和软件漏洞的公共数据库**

若要扩展您的软件的威胁的知识，查看已知的威胁和软件漏洞的可用公共数据库。

-   常见漏洞和披露 (CVE): <https://cve.mitre.org/>
-   通用漏洞枚举： <https://cwe.mitre.org/>
-   常见的攻击模式枚举和分类： <https://capec.mitre.org/index.html>
-   NIST 维护站点介绍了如何编录漏洞： <https://samate.nist.gov/BF/>


 





