---
title: 安全性
description: 使用在本部分中主题来了解有关 Windows 10 移动版中的安全性的详细信息。
ms.assetid: 15783e59-f37b-4373-8604-d35c57eedfcc
ms.date: 08/31/2018
ms.localizationpriority: medium
ms.openlocfilehash: 13a35de780c5165bdd4b336dc1e3e4d879394529
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564511"
---
# <a name="security"></a>安全性

了解有关 Windows 10 中安全的详细信息。

## <a name="os-security-tasks"></a>OS 安全任务

若要创建安全的设备，OEM 应完成以下任务。

<table>
  <thead>
    <th>任务</th>
    <th>描述</th>
  </thead>
  <tbody>
    <tr>
      <td>了解如何进行签名不同类型的可执行代码和其他代码资产</td>
      <td>Windows 10 移动版的所有二进制文件需要加载和执行零售手机上的数字签名。 有关详细信息，请参阅：<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/get-a-code-signing-certificate">获取代码签名证书</a>。</td>
</tr>
<tr class="even">
<td>了解映像验证和加密</td>
<td>Windows 10 移动版包括<a href="https://docs.microsoft.com/windows-hardware/drivers/bringup/secure-boot">安全启动</a>，允许他们执行之前会验证固件映像的过程。 Windows 10 移动版还提供了<a href="https://docs.microsoft.com/windows-hardware/drivers/bringup/secure-boot-and-device-encryption-overview">设备加密</a>，一项功能，对存储在内部数据分区上的所有用户数据进行都加密。 Oem 必须在要启用这些功能的制造期间执行一的系列任务。</td>
</tr>
<tr>
<td>了解安全开发生命周期 (SDL)</td>
<td><a href="https://www.microsoft.com/sdl">安全开发生命周期 (SDL)</a>最佳实践和相关的工具可用于由 Oem 改进其产品的安全性。</td>
</tr>
</tbody>
</table>

## <a name="sdl-recommendations-for-oems"></a>SDL 建议 oem

Microsoft 安全开发生命周期 (SDL) 是一套最佳做法和 Oem 可以使用以提高其产品的安全性的相关的工具。 SDL 做法其按它们是最有效的传统软件开发生命周期的阶段。 例如，在软件设计过程威胁建模是最有效。

如果在独立的基础上实现，许多这些安全活动将提供某种程度的安全性权益。 但是，在 Microsoft 的实际经验已经证明比获得按时间顺序阶段正确的软件开发生命周期和可重复的过程的一部分执行的活动可能会导致更高的安全性的安全生成于临时实现。 有关 SDL 的详细信息，请参阅[Microsoft 安全开发生命周期](https://www.microsoft.com/sdl)。

下表描述了对 OEM 采用最有用的 SDL 实践的子集。 这些做法一些更多有用的驱动程序代码，而有些则是更多有用的应用程序代码。 一些 SDL 方法可用于两者。 驱动程序往往具有更高权限运行，因此务必要开发驱动程序代码时考虑这些最佳实践。

|工具|信息|建议的区域|
|----|----|----|
|[Microsoft SDL 威胁建模工具](https://www.microsoft.com/download/details.aspx?id=49168)|SDL 威胁建模工具使架构师和开发人员来创建其系统的威胁模型，然后对其系统的设计中的潜在安全问题的威胁模型分析。 威胁建模是设计期间，最有效的在最终设计。 有关详细信息，请参阅[SDL 做法 #7： 使用威胁建模](https://www.microsoft.com/sdl/process/design.aspx)。|驱动程序|
|[FxCop](https://www.microsoft.com/SDL/adopt/tools.aspx)|FxCop 是一种静态分析器。 它将分析托管代码程序集并报告有关程序集，例如可能的设计、 本地化、 性能和安全性改进的信息。|合作伙伴应用|
|[从 FxCop 代码分析迁移到.NET 编译器平台分析器](https://docs.microsoft.com/visualstudio/code-quality/fxcop-analyzers)|Visual Studio 2017 包括一组内置分析 C# 或 Visual Basic 代码，当您键入的.NET Compiler Platform 分析器。 你可以安装其他分析器以 Visual Studio 扩展，或在每个项目上作为 NuGet 包。 分析器查看代码样式、 代码质量和可维护性、 代码设计和其他问题。|在托管代码中的合作伙伴应用|
|[BinSkim](https://www.microsoft.com/SDL/adopt/tools.aspx)|BinSkim 是一个二进制的静态分析工具，便可扫描 Windows 可移植可执行文件 (PE) 文件的安全性和正确性。  由 BinSkim 执行验证的 PE 文件已选择加入到所有 Windows 平台所提供的二进制缓解的验证。 ([用户指南](https://github.com/Microsoft/binskim/blob/develop/docs/BinSkimUserGuide.docx))|驱动程序和合作伙伴应用|
|[C/c + + 代码分析](https://docs.microsoft.com/visualstudio/code-quality/code-analysis-for-c-cpp-overview)|C/c + + 代码分析是一种静态分析器，提供与安装的 Visual Studio Team System Development Edition 或 Visual Studio Team Suite 和可帮助检测和更正代码缺陷。 它一次 plows 通过源代码一个函数，并查找 C/c + + 编码模式和不正确的代码可能指示编程错误的使用情况。|驱动程序和合作伙伴应用|
