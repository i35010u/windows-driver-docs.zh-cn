---
title: 安全性
description: 使用此部分中的主题来了解有关 Windows 10 移动版中的安全性的详细信息。
ms.assetid: 15783e59-f37b-4373-8604-d35c57eedfcc
ms.date: 08/31/2018
ms.localizationpriority: medium
ms.openlocfilehash: 78bda857fe00c3e1ced1050c787d63f0563321f0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189403"
---
# <a name="security"></a>安全性

详细了解 Windows 10 中的安全性。

## <a name="os-security-tasks"></a>OS 安全任务

若要创建安全设备，OEM 应完成以下任务。



<table>
  <thead>
    <th>任务</th>
    <th>说明</th>
  </thead>
  <tbody>
    <tr>
      <td>了解如何对不同类型的可执行代码和其他代码资产进行签名</td>
      <td>所有 Windows 10 移动版二进制文件都需要数字签名才能在零售电话上加载和执行。 有关详细信息，请参阅： <a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-a-code-signing-certificate">获取代码签名证书</a>。</td>
</tr>
<tr class="even">
<td>了解映像验证和加密</td>
<td>Windows 10 移动版包含 <a href="https://docs.microsoft.com/windows-hardware/drivers/bringup/secure-boot">安全引导</a>，这是在允许执行固件映像之前对其进行验证的进程。 Windows 10 移动版还提供了 <a href="https://docs.microsoft.com/windows-hardware/drivers/bringup/secure-boot-and-device-encryption-overview">设备加密</a>功能，该功能可对存储在内部数据分区上的所有用户数据进行加密。 在制造过程中，Oem 必须执行一系列任务才能实现这些功能。</td>
</tr>
<tr>
<td>了解 SDL)  (安全开发生命周期</td>
<td>Oem 可以使用<a href="https://www.microsoft.com/sdl">安全开发生命周期 (SDL) </a>最佳实践和相关工具，以提高其产品的安全性。</td>
</tr>
</tbody>
</table>

## <a name="sdl-recommendations-for-oems"></a>针对 Oem 的 SDL 建议

Microsoft 安全开发生命周期 (SDL) 是一组最佳实践和相关的工具，Oem 可以使用这些方法来提高产品的安全性。 SDL 实践按传统软件开发生命周期的阶段进行组织，在这种情况中，它们最为有效。 例如，在软件设计期间威胁建模最为有效。

如果是独立实现的，其中的许多安全活动会提供一定程度的安全优势。 但是，Microsoft 的实际经验表明，在软件开发生命周期的正确阶段中按时间顺序执行的安全活动以及作为可重复过程的一部分，这可能会导致比即席实现产生的安全性更高的安全性。 有关 SDL 的详细信息，请参阅 [Microsoft 安全开发生命周期](https://www.microsoft.com/sdl)。

下表描述了在 OEM 采用时最有用的 SDL 实践的子集。 其中一些做法对驱动程序代码更有帮助，而另一些则更有助于应用程序代码。 某些 SDL 实践对这二者都很有用。 驱动程序往往以更高的特权运行，因此，在开发驱动程序代码时，必须考虑这些最佳做法。

|工具|信息|建议的区域|
|----|----|----|
|[Microsoft SDL Threat Modeling Tool](https://www.microsoft.com/download/details.aspx?id=49168)|SDL Threat Modeling Tool 使架构师和开发人员能够为其系统创建威胁模型，然后分析威胁模型，以了解系统设计中的潜在安全问题。 设计完成之前，威胁建模在设计期间最有效。 有关详细信息，请参阅 [SDL 实践 #7：使用威胁建模](https://www.microsoft.com/sdl)。|驱动程序|
|[FxCop](https://www.microsoft.com/sdl)|FxCop 为静态分析器。 它分析托管代码程序集，并报告有关程序集的信息，例如可能的设计、本地化、性能和安全性改进。|合作伙伴应用|
|[从 FxCop 代码分析迁移到 .NET 编译器平台分析器](/visualstudio/code-quality/fxcop-analyzers)|Visual Studio 2017 包括一系列内置的 .NET Compiler Platform 分析器，这些分析器在用户键入时分析 C# 或 Visual Basic 代码。 可以将其他分析器作为 Visual Studio 扩展安装，或在每个项目上作为 NuGet 包安装。 分析器关注代码样式、代码质量和可维护性、代码设计和其他问题。|托管代码中的合作伙伴应用|
|[BinSkim](https://www.microsoft.com/sdl)|BinSkim 是一种二进制静态分析工具，用于扫描 Windows 可移植可执行文件 (PE) 文件以确保安全和正确性。  在 BinSkim 执行的验证中，会验证 PE 文件是否已选择加入 Windows 平台提供的所有二进制缓解措施。  ([用户指南 (.docx 下载) ](https://github.com/microsoft/binskim/blob/master/docs/BinSkimUserGuide.docx?raw=true)) |驱动程序和合作伙伴应用|
|[C/c + + 代码分析](/visualstudio/code-quality/code-analysis-for-c-cpp-overview)|适用于 C/c + + 的代码分析是一个静态分析器，在安装 Visual Studio Team System 开发版或 Visual Studio 团队套件时提供，有助于检测和更正代码缺陷。 它一次 plows 一个函数的源代码，并查找 C/c + + 编码模式和可能指示编程错误的代码使用不正确。|驱动程序和合作伙伴应用|