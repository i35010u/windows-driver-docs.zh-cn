---
title: 驱动程序的威胁建模
description: 驱动程序编写者和架构师在任何驱动程序的设计过程中都应当进行威胁建模。 本文提供了有关为 Microsoft Windows 系列操作系统的驱动程序创建威胁模型的准则。
ms.assetid: 77FB242E-A07C-4298-80ED-866F8D80118C
ms.date: 06/27/2018
ms.localizationpriority: medium
ms.openlocfilehash: 445953946548dbea708b0d666678869f3944dd44
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215654"
---
# <a name="threat-modeling-for-drivers"></a>驱动程序的威胁建模

驱动程序编写者和架构师在任何驱动程序的设计过程中都应当进行威胁建模。 本主题提供有关为 Windows 驱动程序创建威胁模型的准则。

安全应是任何驱动程序的基本设计要点。 任何成功的产品都是目标。 如果你正在编写适用于 Windows 的驱动程序，则必须假定在某个时间，有人会尝试使用你的驱动程序来损害系统安全性。

设计安全驱动程序涉及：

-   确定驱动程序可能易受到攻击的点。
-   分析每个这样的点可能会装载的攻击类型。
-   确保该驱动程序的设计方式旨在防范此类攻击。

威胁建模是这些重要设计任务的结构化方法。 威胁模型是一种对资产的威胁进行分类和分析的方式。 从驱动程序编写者的角度来看，资产是计算机或网络上的硬件、软件和数据。

威胁模型回答了以下问题：

-   哪些资产需要保护？
-   资产有哪些威胁？
-   每种威胁有多重要？
-   如何缓解威胁？

威胁建模是软件设计的重要组成部分，因为它可以确保将安全内置于产品中，而不是将其视为事后。 良好的威胁模型有助于在设计过程中查找和阻止 bug，进而消除潜在的昂贵修补程序，并可能会损坏你的组织声誉。

本部分将威胁建模原则应用于驱动程序设计，并提供驱动程序可能会受到攻击的威胁的示例。 有关软件设计的威胁建模的更完整说明，请参阅以下资源。

-   Microsoft SDL 网站：

    <https://www.microsoft.com/sdl>

-   简化的 Microsoft SDL 实现：

    [下载白皮书](https://go.microsoft.com/?linkid=9708425)

-   此博客文章介绍了如何下载 *安全开发生命周期*的免费副本： SDL、Michael Howard 和 Steve Lipner：

    <https://blogs.msdn.microsoft.com/microsoft_press/2016/04/19/free-ebook-the-security-development-lifecycle/>


## <a name="span-idcreate_a_threat_modelspanspan-idcreate_a_threat_modelspanspan-idcreate_a_threat_modelspancreate-threat-models-for-drivers"></a><span id="Create_a_threat_model"></span><span id="create_a_threat_model"></span><span id="CREATE_A_THREAT_MODEL"></span>为驱动程序创建威胁模型

创建威胁模型需要透彻地理解驱动程序的设计、驱动程序可能会公开到的威胁类型以及利用特定威胁的安全攻击的后果。 为驱动程序创建威胁模型后，您可以确定如何缓解潜在威胁。

在驱动程序设计期间以组织的结构化方式执行威胁建模是最有效的方式，而不是在编码过程中随意。 结构化方法会增加您在设计中发现漏洞的可能性，从而帮助确保模型全面。

组织威胁建模工作的一种方法是执行以下步骤：

1.  创建显示通过驱动程序的数据流的结构化关系图。 包含驱动程序执行的所有可能的任务以及驱动程序的所有输入和输出的源和目标。 正式的数据流关系图或类似的结构化关系图可帮助您通过驱动程序分析数据的路径，以及确定驱动程序的外部接口、边界和交互。 
2.  基于数据流关系图分析潜在的安全威胁。
3.  评估你在上一步中标识的威胁，并确定如何减轻这些威胁。

## <a name="span-idcreate_a_data_flow_diagramspanspan-idcreate_a_data_flow_diagramspanspan-idcreate_a_data_flow_diagramspancreate-a-data-flow-diagram"></a><span id="Create_a_data_flow_diagram"></span><span id="create_a_data_flow_diagram"></span><span id="CREATE_A_DATA_FLOW_DIAGRAM"></span>创建数据流关系图

数据流关系图以概念形式显示了驱动程序和与之交互的外部实体之间的数据流，通常是操作系统、用户进程和设备。 正式数据流关系图使用以下符号：

![symbols](images/dataflowdiagramsymbols.gif)

下图显示了假设的内核模式 Windows 驱动模型 (WDM) 驱动程序的示例数据流关系图。 无论特定类型的驱动程序的体系结构如何，概念模型都是相同的：显示所有数据路径，并识别进入或退出驱动程序的每个数据源。

![假设内核模式驱动程序的示例数据流图表](images/sampledataflowdiagramkernelmodedriver.gif)

**注意**   上图显示了直接在用户进程与驱动程序之间流动的数据，并省略了任何中间驱动程序。 但实际上，所有请求都将通过 i/o 管理器，并可能在到达特定驱动程序之前遍历一个或多个更高级别的驱动程序。 此图省略了这些中间步骤，强调数据的原始源和提供数据的线程的上下文的重要性。 内核模式驱动程序必须验证在用户模式下产生的数据。

信息进入驱动程序的原因是，来自操作系统的请求、用户进程发出的请求或请求 (通常会中断设备) 。

上图中的驱动程序从操作系统接收多种类型的请求中的数据：

-   通过调用 **DriverEntry**、 **DriverUnload**和 **AddDevice** 例程对驱动程序及其设备执行管理任务的请求
-   即插即用请求 (IRP \_ MJ \_ PNP) 
-    (IRP \_ MJ \_ power) 的电源管理请求
-   内部设备 i/o 控制请求 (IRP \_ MJ \_ 内部 \_ 设备 \_ 控制) 

作为对这些请求的响应，数据将从驱动程序流回操作系统作为状态信息。 图中的驱动程序接收来自用户进程的来自以下类型请求的数据：

-    (IRP \_ mj \_ CREATE、irp \_ MJ \_ 读取或 irp \_ mj \_ 写入来创建、读取和写入请求) 
-    (IRP \_ MJ 设备控制的公共设备 i/o 控制 \_ 请求 \_) 

为响应这些请求，输出数据和状态信息将从驱动程序流向用户进程。

最后，驱动程序从设备接收数据，因为设备 i/o 操作或用户操作 (例如打开 CD 驱动器上的托盘) 更改设备状态。 同样，驱动程序中的数据会在 i/o 操作过程中流入设备，并会更改设备状态。

上图以广泛的概念级别显示了驱动程序数据流。 每个圆圈表示一个相对较大的任务，缺少详细信息。 在某些情况下，单个级别的关系图（如示例）足以理解数据源和路径。 如果你的驱动程序处理来自不同源的多种不同类型的 i/o 请求，你可能需要创建一个或多个显示更多详细信息的其他关系图。 例如，标记为 "处理 i/o 请求" 的圆圈可能展开为单独的关系图，如下图所示。

![i/o 请求的扩展数据流关系图](images/expandeddataflowdiagramiorequests.gif)

第二个关系图显示了第一个关系图中每种类型的 i/o 请求的单独任务。  (为简单起见，省略了设备的数据路径。 ) 

根据设备类型，关系图中显示的外部实体和输入和输出类型可能会有所不同。 例如，Windows 提供多种常见设备类型的类驱动程序。 系统提供的类驱动程序与供应商提供的微型驱动程序一起使用，后者通常是包含一组回调例程的动态链接库 (DLL) 。 用户 i/o 请求会定向到类驱动程序，后者随后调用微型驱动程序中的例程来执行特定任务。 微型驱动程序通常不会接收整个 i/o 请求数据包作为输入;相反，每个回调例程只接收特定任务所需的数据。

创建数据流关系图时，请记住驱动程序请求的各种来源。 在用户计算机上运行的任何代码都可以生成对驱动程序的 i/o 请求，从众所周知的应用程序（例如 Microsoft Office 到免费软件、共享程序和可能可疑的 Web 下载）。 根据特定设备，你可能还需要考虑公司提供的媒体编解码器或第三方筛选器，以支持其设备。 可能的数据源包括：

-   该 \_ \_ 驱动程序处理的 IRP MJ XXX 请求
-   驱动程序定义或处理的 IOCTLs
-   驱动程序调用的 Api
-   回调例程
-   驱动程序公开的任何其他接口
-   驱动程序读取或写入的文件，包括在安装过程中使用的文件
-   驱动程序读取或写入的注册表项
-   配置属性页和驱动程序使用的用户提供的任何其他信息

模型还应涵盖驱动程序安装和更新过程。 包含驱动程序安装过程中读取或写入的所有文件、目录和注册表项。 还应考虑在设备安装程序、共同安装程序和属性页中公开的接口。

驱动程序与外部实体交换数据的任何点都可能会受到攻击。

## <a name="span-idanalyze_potential_threatsspanspan-idanalyze_potential_threatsspanspan-idanalyze_potential_threatsspananalyze-potential-threats"></a><span id="Analyze_potential_threats"></span><span id="analyze_potential_threats"></span><span id="ANALYZE_POTENTIAL_THREATS"></span>分析潜在威胁

确定某一驱动程序可能会受到攻击的点后，您可以确定在每个点上可能发生的威胁类型。 请考虑以下类型的问题：

-   保护每个资源的安全机制有哪些？
-   是否所有转换和接口都得到了正确的保护？
-   无意中非法使用了某项功能，安全漏洞？
-   是否恶意利用了功能安全漏洞？
-   默认设置是否提供足够的安全性？

## <a name="span-idthe_stride_approachspanspan-idthe_stride_approachspanspan-idthe_stride_approachspanthe-stride-approach-to-threat-categorization"></a><span id="The_STRIDE_approach"></span><span id="the_stride_approach"></span><span id="THE_STRIDE_APPROACH"></span>威胁分类的步幅方法

首字母缩写步幅介绍了对软件的六类威胁。 此首字母缩写词派生自：

-   **S**表示欺骗
-   **T**表示篡改
-   **R**表示拒绝
-   **我**璝泄露
-   **D**表示拒绝服务
-   **E**表示特权提升权限

使用 STRIDE 作为指导，你可以提出有关可针对驱动程序的攻击类型的详细问题。 目标是确定驱动程序中每个容易受到攻击的点可能可能出现的攻击类型，然后为每个可能的攻击创建一个方案。

-   **欺骗** 使用其他人的凭据来访问其他无法访问的资产。 进程通过传递伪造或被盗的凭据来装入欺骗攻击。
-   **篡改** 是指更改数据以装入攻击。 例如，如果所需的驱动程序文件未使用驱动程序签名和访问控制列表 (Acl) ，驱动程序可能很容易受到篡改。 在这种情况下，恶意用户可能会改变文件，从而破坏系统安全性。
-   当用户拒绝执行某个操作时，但该操作的目标无法以其他方式进行验证时，会发生**抵赖**。 如果驱动程序没有记录可能危及安全的操作，则可能会容易遭受抵赖威胁。 例如，如果视频设备的驱动程序未记录更改其设备特征的请求（如焦点、扫描区域、映像捕获频率、捕获映像的目标位置等），则该驱动程序的驱动程序将容易受到抵赖。 生成的映像可能已损坏，但系统管理员无法确定哪个用户导致了该问题。
-   **信息泄露** 威胁完全如名称所示：向不具有查看权限的用户公开信息。 向用户缓冲区传递信息的任何驱动程序都易受到信息泄露威胁的攻击。 为了避免信息泄露威胁，驱动程序必须在写入数据之前验证每个用户缓冲区的长度，并对缓冲区进行零初始化。
-   **拒绝服务** 攻击威胁了有效用户访问资源的能力。 资源可以是磁盘空间、网络连接或物理设备。 导致性能降低到不可接受级别的攻击也被视为拒绝服务攻击。 如果资源消耗阻碍其他有效用户执行任务的能力，则允许用户进程不必要地独占系统资源的驱动程序可能容易遭受拒绝服务攻击。

    例如，驱动程序可能使用信号量来保护数据结构，同时以 IRQL = 被动级别执行 \_ 。 但是，驱动程序必须在 **KeEnterCriticalRegion/KeLeaveCriticalRegion** 对中获取和释放信号量，这将禁用并重新启用异步过程调用 (apc) 的传送。 如果驱动程序无法使用这些例程，则 APC 可能会导致操作系统挂起持有信号灯的线程。 因此，其他进程 (包括管理员创建的进程) 将无法获取对该结构的访问权限。

-   如果非特权用户获得特权状态，则可能会发生 **特权提升** 攻击。 将用户模式句柄传递到 **ZwXxx** 例程的内核模式驱动程序容易遭受特权提升攻击，因为 **ZwXxx** 例程会绕过安全检查。 内核模式驱动程序必须验证它们从用户模式调用方收到的每个句柄。

    如果内核模式驱动程序依赖于 IRP 标头中的 **irp->requestormode** 值来确定 i/o 请求来自内核模式或用户模式调用方，则也可能会发生特权提升攻击。 在从网络或服务器服务到达的 Irp (SRVSVC) ，无论请求的来源是什么， **irp->requestormode** 的值都是 **KernelMode**。 若要避免此类攻击，驱动程序必须针对此类请求执行访问控制检查，而不是简单地使用 **irp->requestormode**的值。

## <a name="span-idanalysistechspanspan-idanalysistechspandriver-analysis-techniques"></a><span id="analysistech"></span><span id="ANALYSISTECH"></span>驱动程序分析技术

组织分析的一种简单方法是，列出易受攻击的区域以及潜在威胁以及每种类型的威胁的一种或多种方案。

若要执行彻底的分析，必须在驱动程序中的每个可能易受到攻击的点探索威胁的可能性。 在每个容易受到攻击的点，确定每类威胁 (欺骗、篡改、否认、信息泄露、拒绝服务和特权提升) 可能。 然后为每个变得合理威胁创建一个或多个攻击方案。

例如，请考虑 IRP \_ MJ 设备控制请求的数据流，如上 \_ \_ 图所示。 下表显示了在处理此类请求时，驱动程序可能会遇到的两种类型的威胁：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">易受攻击点</th>
<th align="left">潜在威胁 (STRIDE) </th>
<th align="left">方案</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">IRP_MJ_DEVICE_CONTROL 请求</td>
<td align="left"><p>拒绝服务</p>
<p>特权提升</p></td>
<td align="left"><p>用户进程发出导致设备失败的 IOCTLs 序列。</p>
<p>用户进程发出的 IOCTL 允许 FILE_ANY_ACCESS。</p></td>
</tr>
</tbody>
</table>

 
一个威胁通常与另一个威胁相关。 例如，利用特权提升威胁的攻击可能会导致信息泄露或拒绝服务。 此外，某些类型的攻击依赖于一系列事件。 恶意用户可能会利用特权提升威胁。 然后，在提升权限的情况下，用户可能会发现并利用其他漏洞。

威胁树和大纲在建模此类复杂方案时可能很有用。

威胁树是显示威胁或漏洞的层次结构的关系图，实质上，威胁树模拟恶意用户在发动攻击时的步骤。 攻击的最终目标是在树的顶部。 每个从属级别都显示了执行攻击所需的步骤。 下图是前面示例中的拒绝服务方案的一个简单威胁树。

![简单威胁树](images/simplethreattree.gif)

威胁树显示了用于装载特定攻击的必需步骤，以及步骤之间的关系。 大纲是威胁树的替代方法。

大纲只是以分层顺序列出了攻击特定威胁的步骤。 例如：

1.0 导致设备停止响应。

1.1 问题序列中的 IOCTLS 问题。

1.1.1 确定导致设备失败的序列。

1.1.2 获取提升权限以颁发内部 IOCTLs。

任一方法都可帮助你了解哪些威胁最危险，哪些威胁最重要。

 

## <a name="span-idfast_path_threat_modelingspanspan-idfast_path_threat_modelingspanspan-idfast_path_threat_modelingspanfast-path-threat-modeling"></a><span id="Fast_path_threat_modeling"></span><span id="fast_path_threat_modeling"></span><span id="FAST_PATH_THREAT_MODELING"></span>快速路径威胁建模

如果资源有限，则可以创建摘要大纲来帮助评估驱动程序的安全风险，而不是创建完整的威胁模型关系图。 例如，下面的文本介绍了上一示例中所述的示例驱动程序中 diagramed 的一些图面区域。

驱动程序会在以下几种类型的请求中接收来自操作系统的数据：

-   通过调用 **DriverEntry**、 **DriverUnload**和 **AddDevice** 例程对驱动程序及其设备执行管理任务的请求
-   即插即用请求 (IRP \_ MJ \_ PNP) 
-    (IRP \_ MJ \_ power) 的电源管理请求
-   内部设备 i/o 控制请求 (IRP \_ MJ \_ 内部 \_ 设备 \_ 控制) 

作为对这些请求的响应，数据将从驱动程序流回操作系统作为状态信息。 驱动程序在以下类型的请求中从用户进程接收数据：

-    (IRP \_ mj \_ CREATE、irp \_ MJ \_ 读取或 irp \_ mj \_ 写入来创建、读取和写入请求) 
-    (IRP \_ MJ 设备控制的公共设备 i/o 控制 \_ 请求 \_) 

为响应这些请求，输出数据和状态信息将从驱动程序流向用户进程。

通过对驱动程序的数据流进行基本了解，你可以检查每个输入和输出区域是否存在可能的威胁。



## <a name="span-idthe_dread_approachspanspan-idthe_dread_approachspanspan-idthe_dread_approachspanthe-dread-approach-to-threat-assessment"></a><span id="The_DREAD_approach"></span><span id="the_dread_approach"></span><span id="THE_DREAD_APPROACH"></span>威胁评估的维持方法

确定驱动程序可能受到的攻击的方式和位置不足。 然后，你必须评估这些潜在威胁，确定其相对优先级，并设计缓解策略。 

维持是一个首字母缩写词，描述用于评估对软件的威胁的五个条件。 维持代表：

-   **D**潜在
-   **R**损害
-   **E**xploitability
-   **评估用户**
-   **D**再现

若要确定驱动程序的威胁的优先级，请在所有5个维持评估条件上将每个威胁的级别设置为1到10，然后添加分数并除以 5 (条件) 数。 结果是每个威胁1到10之间的数值分数。 高分数表示严重的威胁。

-   **损坏**。 评估可能由安全攻击导致的损害显然是威胁建模的关键部分。 损坏可能包括数据丢失、硬件或介质故障、未达标准性能或任何适用于你的设备及其操作环境的相似措施。
-   **可再现性** 是指定类型的攻击成功的频率的度量值。 容易再现的威胁比极少出现或不可预测的漏洞更有可能被攻击。 例如，默认情况下安装的或在每个可能的代码路径中使用的功能的威胁是高度可重复的。
-   **可利用性** 评估了安装攻击所需的工作量和专业知识。 可能会受到相对较少的大学学生攻击的威胁非常容易受到攻击。 这种攻击需要训练有素的人员，而执行成本较低。

    在评估可利用性时，还应考虑潜在攻击者的数量。 任何远程、匿名用户都可利用的威胁比要求现场、高度授权的用户的威胁更强。

-   **受影响的用户**。 受攻击影响的用户数是评估威胁的另一个重要因素。 最多可能影响一位或两位用户的攻击在此度量值相对较低。 相反，导致网络服务器崩溃的拒绝服务攻击可能会影响数以千计的用户，从而提高速度。
-   可**发现**的是威胁受到攻击的可能性。 发现很难准确估算。 最安全的方法是假定任何漏洞最终都会利用和，从而依赖于其他措施来确定威胁的相对排名。

**示例：使用维持评估威胁**

下表介绍了前面所述的示例，下表显示了设计器如何评估假设的拒绝服务攻击：

| 维持条件 | Score   | 注释                                                                |
|-----------------|---------|-------------------------------------------------------------------------|
| 损害          | 8       | 暂时中断工作，但不会造成永久性损坏或数据丢失。 |
| 可再现性 | 10      | 导致设备每次都失败。                                   |
| 可利用性  | 7       | 要求重点确定命令序列。            |
| 受影响的用户  | 10      | 影响市场上此设备的每个模型。                       |
| 可发现性 | 10      | 假设将发现每个潜在的威胁。                 |
| **总**      | **9.0** | **缓解此问题的优先级较高。**                           |


**缓解威胁**


你的驱动程序设计应能够应对模型公开的所有威胁。 但是，在某些情况下，缓解可能不可行。 例如，假设攻击可能会影响极少的用户，并且不太可能会导致数据或系统可用性损失。 如果缓解此类威胁需要花费几个月的时间，则可能要改为使用额外时间来测试驱动程序。 尽管如此，请记住，最终恶意用户可能会发现漏洞并发动攻击，然后驱动程序将需要此问题的修补程序。



## <a name="span-idincluding_threat_modeling_in_a_broader_security_development_lifecycle__processspanspan-idincluding_threat_modeling_in_a_broader_security_development_lifecycle__processspanspan-idincluding_threat_modeling_in_a_broader_security_development_lifecycle__processspanincluding-threat-modeling-in-a-broader-security-development-lifecycle-process"></a><span id="Including_threat_modeling_in_a_broader_Security_Development_Lifecycle__process"></span><span id="including_threat_modeling_in_a_broader_security_development_lifecycle__process"></span><span id="INCLUDING_THREAT_MODELING_IN_A_BROADER_SECURITY_DEVELOPMENT_LIFECYCLE__PROCESS"></span>在更广泛的安全性开发生命周期过程中包括威胁建模

请考虑在更广泛的安全开发生命周期（SDL）中包括威胁建模过程。

Microsoft SDL 流程提供了很多建议的软件开发过程，可对其进行修改，使其适合任意规模的组织-包括单个开发人员。 请考虑将 SDL 建议的组件添加到软件开发过程。

有关详细信息，请参阅 [Microsoft 安全开发生命周期 (SDL) –过程指南](/previous-versions/windows/desktop/cc307891(v=msdn.10))。

**培训和组织功能** -采用软件开发安全培训来扩展识别和修正软件漏洞的能力。

Microsoft 使其四个核心 SDL 培训课程可供下载。 [Microsoft 安全开发生命周期核心培训课程](https://go.microsoft.com/?linkid=9708478)

有关 SDL 培训的详细信息，请参阅此白皮书。 [Microsoft SDL 的重要软件安全培训](https://www.microsoft.com/download/details.aspx?id=9950)

**要求和设计** -构建受信任的软件的最佳机会是在新版本或新版本的初始规划阶段，因为开发团队可以识别密钥对象并集成安全和隐私，从而最大程度地减少对计划和计划的中断。

此阶段中的密钥输出是设置特定的安全目标。 例如，确定你的所有代码都应将 Visual Studio 代码分析 "所有规则" 传递给零个警告。

**实现** -所有开发团队都应该定义并发布已批准工具的列表及其关联的安全检查，例如编译器/链接器选项和警告。

对于驱动程序开发人员而言，大多数有用的工作都是在此阶段完成的。 编写代码时，会检查其是否存在可能的漏洞。 代码分析和驱动程序验证器等工具用于查找代码中可强制执行的区域。

**验证** -验证是指软件在功能上完成，并根据要求和设计阶段中所述的安全目标进行测试的点。

可以使用其他工具（如 binscope 和模糊测试人员）来验证是否已满足安全设计目标并且代码已准备好交付

**发布和响应** 为发布产品做好准备，需要创建一个事件响应计划，用于描述应对新威胁所要执行的操作，以及如何在交付驱动程序后对其进行服务。 如果在随附的代码中发现安全问题，则提前执行此操作将会使你能够更快地做出响应。

有关 SDL 过程的详细信息，请参阅以下附加资源：

-   这是 Microsoft 的主要网站，并提供 SDL 的概述。 <https://www.microsoft.com/sdl>

-   此博客介绍了如何下载 *安全开发生命周期*的免费副本： SDL、Michael Howard 和 Steve Lipner。 <https://blogs.msdn.microsoft.com/microsoft_press/2016/04/19/free-ebook-the-security-development-lifecycle/>

-   本页提供了指向其他 SDL 出版物的链接。 <https://www.microsoft.com/SDL/Resources/publications.aspx>



## <a name="span-idcall_to_actionspanspan-idcall_to_actionspanspan-idcall_to_actionspancall-to-action"></a><span id="Call_to_action"></span><span id="call_to_action"></span><span id="CALL_TO_ACTION"></span>调用操作

对于驱动程序开发人员：

-   建立驱动程序设计的威胁建模。
-   采取措施有效缓解驱动程序代码中的威胁。
-   熟悉适用于你的驱动程序和设备类型的安全和可靠性问题。 有关详细信息，请参阅 Windows 设备驱动程序工具包的设备特定部分 (WDK) 。
-   了解哪些检查操作系统、i/o 管理器以及任何更高级别的驱动程序在用户请求到达您的驱动程序之前会执行，哪些检查不会执行。
-   使用 WDK 中的工具（如驱动程序验证器）来测试和验证驱动程序。
-   查看已知威胁和软件漏洞的公共数据库。

有关其他驱动程序安全资源，请参阅 [驱动程序安全清单](driver-security-checklist.md)。


## <a name="span-idresourcesspanspan-idresourcesspanspan-idresourcesspansoftware-security-resources"></a><span id="Resources"></span><span id="resources"></span><span id="RESOURCES"></span>软件安全资源

**书籍**

*编写安全代码*，Michael Howard 和 David LeBlanc 的第二个版本

*24 抱问题 Of Software Security：编程缺陷以及如何修复它们*、Michael Howard、David LeBlanc 和 John Viega 的第一版

*软件安全评估的内容：* 通过 Mark Dowd、John 麦克唐纳和 Justin Schuh 来识别和预防软件漏洞

**Microsoft 硬件和驱动程序开发人员信息**

[常见驱动程序可靠性问题](https://download.microsoft.com/download/5/7/7/577a5684-8a83-43ae-9272-ff260a9c20e2/drvqa.doc) 白皮书

[Windows 驱动程序中的取消逻辑](/previous-versions/windows/hardware/design/dn653289(v=vs.85)) 白皮书

[Windows 安全模型：每个驱动程序编写器需要知道的内容](windows-security-model.md)

**Microsoft Windows 驱动程序开发工具包 (DDK) **

请参阅[内核模式驱动程序体系结构](../index.yml)中的[驱动程序编程方法](https://docs.microsoft.com/windows-hardware/drivers/kernel/driver-programming-techniques)

**测试工具**

[有关性能和兼容性，](/windows-hardware/test/index)请参阅测试[Windows 硬件实验室工具包](../index.yml)

**已知威胁和软件漏洞的公共数据库**

若要扩展软件威胁的知识，请查看已知威胁的可用公共数据库和软件漏洞。

-   常见漏洞和泄密 (CVE) ： <https://cve.mitre.org/>
-   常见漏洞枚举： <https://cwe.mitre.org/>
-   常见攻击模式枚举和分类： <https://capec.mitre.org/index.html>
-   NIST 维护一个站点，说明如何编录漏洞： <https://samate.nist.gov/BF/>


