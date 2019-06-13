---
title: 提交设备元数据体验时的错误和解决方案
description: 提交设备元数据体验时的错误和解决方案
ms.assetid: 793b4c92-96e8-4b3e-a7de-d00e953c983a
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83b8d0122497f7c429d922cd0f58b604e7799244
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63337240"
---
# <a name="errors-and-solutions-when-submitting-device-metadata-experiences"></a>提交设备元数据体验时的错误和解决方案


当你提交设备元数据体验以进行验证和发布时，你可能会看到影响体验发布的错误。

## <a name="span-idcommonerrorsspanspan-idcommonerrorsspanspan-idcommonerrorsspancommon-errors"></a><span id="Common_errors"></span><span id="common_errors"></span><span id="COMMON_ERRORS"></span>常见错误


下面列出了一些最常见的错误，它们以字母顺序列出并包括解决方案（如果已提供）。

### <a name="span-idtosolvecommonerrorsspanspan-idtosolvecommonerrorsspanspan-idtosolvecommonerrorsspanto-solve-common-errors"></a><span id="To_solve_common_errors"></span><span id="to_solve_common_errors"></span><span id="TO_SOLVE_COMMON_ERRORS"></span>解决常见错误

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>错误</th>
<th>建议的解决方案</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Behavior.xml 中的 [CategoryName] 类别 ID 不正确。 正确的类别 ID 是 [CategoryId]</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>你的设备需要 Behavior.xml 中的 [CategoryName] Guid [CategoryId]。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>[FolderName] 文件夹已丢失。</p></td>
<td><p>你的一个文件夹已丢失。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>在 PackageInfo.xml 的 &lt;PackageStructure&gt; 元素中需要 [FolderName] 文件夹名称。</p></td>
<td><p>你必须在 PackageInfo.xml 中包括正确的文件夹名称引用。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>[ImageType] 图像 – [SplitType] 拆分的 [FileName] 大小无效。 有效的大小为：[ListOfAllowedSizes]</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>[ImageType] 图像 – [FileName] 大小无效。 有效的大小为：[ListOfAllowedSizes]</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>未针对 Behavior.xml 中的任务 [TaskId] 引用 [TaskGroupName] Guid [TaskGroupGuid]</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>[TaskName] 任务 – 在 Behavior.xml 的“系统设置”类别中，你的设备需要使用 [TaskId]。</p></td>
<td><p>你的设备的“操作中心”任务和“系统设置”任务必须出现在 Device Stage 中的“系统设置”类别下。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>[TaskName] 任务 – [TaskId] 应为你的设备引用 Behavior.xml 中的 taskGroupGuid [TaskGroupGuid]。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>在设备的根处需存在 Behavior.xml 中的 [TaskName] 任务 [TaskId]。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>\DeviceStage\Device\[Locale]\ 和 \DeviceStage\Device\ 文件夹应具有相同的文件。</p></td>
<td><p>如果将此包设置为默认区域设置，则该区域设置目录和中性语言目录必须具有相同的文件。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>.cab 提交需包含硬件信息和/或型号信息。 Please correct the .cab or modify the existing .cabs.</p></td>
<td><p>你的包必须至少包含一个硬件 ID 或型号 ID。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>此 .cab 中的硬件 ID 出现冲突，从而使得该 .cab 无法上载。 Please ensure no other experience you have created uses this Hardware ID.</p></td>
<td><p>你的硬件 ID 已经在你的另一个体验中使用。 在仪表板上的“设备元数据”下，打开“管理体验”页。 在筛选器中，输入硬件 ID 以查找其他体验。 然后，你可以解决任何冲突。</p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules" data-raw-source="[Device Metadata Business Rules](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)">设备元数据业务规则</a>。</p></td>
</tr>
<tr class="even">
<td><p>A Hardware ID in this . cab is in use by another company and the .cab cannot be uploaded. 请验证此硬件 ID。</p></td>
<td><p>你已经包含在包中的硬件 ID 正由另一个公司使用。 你无法提交另一个公司的硬件 ID。 确保你的硬件 ID 拼写正确。 如果你仍然收到错误消息，请发送电子邮件到 sysdev@microsoft.com 以寻求仪表板支持来解决问题。</p></td>
</tr>
<tr class="odd">
<td><p>A live submission already exists for this locale in this experience.</p></td>
<td><p>删除此区域设置的现有实时包，然后再为同一个区域设置上载新包。</p></td>
</tr>
<tr class="even">
<td><p>A live submission already exists with default locale set to true in this experience.</p></td>
<td><p>只能将体验中的一个实时包设置为默认包。</p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules" data-raw-source="[Device Metadata Business Rules](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)">设备元数据业务规则</a>。</p></td>
</tr>
<tr class="odd">
<td><p>A logo submission for a MultiPurpose device does not match the submission category.</p></td>
<td><p>列在徽标提交中的设备类别不匹配你的设备元数据包的主要设备类别。 要解决此问题，请执行下列步骤：</p>
<ul>
<li><p>更正你的徽标提交的设备类别。</p></li>
<li><p>创建一个新体验并且仅绑定正确的徽标提交。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>A Model ID in this cab is in conflict and the cab cannot be uploaded. Please ensure no other experience you have created uses this Model ID.</p></td>
<td><p>你的型号 ID 已经在你的另一个体验中使用。 在仪表板上的“设备元数据”下，打开“管理体验”页。 在筛选器中，输入型号 ID 以查找其他体验。 然后，你可以解决任何冲突。</p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules" data-raw-source="[Device Metadata Business Rules](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)">设备元数据业务规则</a>。</p></td>
</tr>
<tr class="odd">
<td><p>此 cab 中的某个型号 ID 正由另一个公司使用，cab 无法上载。 请验证此型号 ID。</p></td>
<td><p>你已经包含在包中的型号 ID 正由另一个公司使用。 你无法提交另一个公司的型号 ID。 确保你的型号 ID 拼写正确。 如果你仍然收到错误消息，请发送电子邮件到 sysdev@microsoft.com 以寻求仪表板支持来解决问题。</p></td>
</tr>
<tr class="even">
<td><p>A non-preview live package cannot be promoted to live.</p></td>
<td><p>你不能将实时包提升为“实时”状态。</p></td>
</tr>
<tr class="odd">
<td><p>无法将具有错误状态的包提升为实时状态。</p></td>
<td><p>你不能将包含错误的包提升为“实时”状态。</p></td>
</tr>
<tr class="even">
<td><p>A preview submission already exists for this locale in this experience.</p></td>
<td><p>要解决此问题，请尝试执行下列步骤：</p>
<ul>
<li><p>删除此区域设置的现有预览包，然后为同一个区域设置上载新预览包。</p></li>
<li><p>将此区域设置的当前预览包提升为“发布”状态，然后为同一个区域设置上载新预览包。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>A preview submission already exists with default locale set to true in this experience.</p></td>
<td><p>只能将体验中的一个预览包设置为默认包。</p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules" data-raw-source="[Device Metadata Business Rules](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)">设备元数据业务规则</a>。</p></td>
</tr>
<tr class="even">
<td><p>All device metadata .cab files in an experience must support the same Hardware IDs. Please correct the .cab.</p></td>
<td><p>此包不具有该体验中的其他包所具有的相同型号 ID 列表。 更正此包中的型号 ID 列表，然后再次上载此包。</p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules" data-raw-source="[Device Metadata Business Rules](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)">设备元数据业务规则</a>。</p></td>
</tr>
<tr class="odd">
<td><p>对于 Tasks.xml 中的任务 [TaskID]，被允许的域不应为空，</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>找到一个非预期文件：“[ExtraFile]”。 Please ensure you follow the architecture or reference all root files in PackageInfo.xml.</p></td>
<td><p>在包的根目录处存在额外的文件。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>发现一个非预期文件夹：“[ExtraFolder]”。 请确保遵循体系结构或引用 PackageInfo.xml 中的所有根文件夹。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>对于 Tasks.xml 中的任务 [TaskID]，命令行 URL 不应为空。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>在 DeviceInfo.xml 中找不到设备类别。</p></td>
<td><p>你必须设置主要设备类别，它是预定义的选项之一。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>在 \DeviceStage\ folder 中找不到设备文件夹。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>在 DeviceInfo.xml 中找不到设备图标信息</p></td>
<td><p>如果你将某个设备图标包含在 DeviceInfo.xml 文件中，还必须包含设备图标信息。 Device Stage 包需要有设备图标。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>此提交的设备元数据类别需要匹配现有的体验类别。</p></td>
<td><p>此包中的设备类别不匹配此体验其他包中的类别。 修改你的设备类别并重新提交此包。</p></td>
</tr>
<tr class="odd">
<td><p>Device Metadata Submission Type for this submission needs to match the existing experience category.</p></td>
<td><p>设备元数据提交类型被定义为 Device Stage 或“设备和打印机”。 只有 Device Stage 包可以包含在 Device Stage 体验中。 同样，只有“设备和打印机”包可以包含在“设备和打印机”体验中。</p></td>
</tr>
<tr class="even">
<td><p>Device Stage inbox submissions are not allowed for the computer device class.</p></td>
<td><p>如果你的包和体验用于 Device Stage 和计算机设备，你必须已经对它们进行徽标认证，或者你必须在 90 天内对它们进行徽标认证。</p></td>
</tr>
<tr class="odd">
<td><p>Device Stage is not supported for this device.</p></td>
<td><p>在 Device Stage 中不支持你选择的设备类别。</p></td>
</tr>
<tr class="even">
<td><p>Device Stage metadata cannot be submitted for your device [DeviceCategory]</p></td>
<td><p>仅允许为以下设备进行 Device Stage 提交：</p>
<ul>
<li><p>便携式媒体播放机</p></li>
<li><p>数码相机</p></li>
<li><p>移动电话</p></li>
<li><p>打印机或传真机</p></li>
<li><p>扫描仪</p></li>
<li><p>计算机系统</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Device Stage 要求营销项目符号或状态项目显示在 Behavior.xml 中。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>Device Stage 要求在 WindowsInfo.xml 中为你的设备将 LaunchDeviceStageFromExplorer 设置为 True。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>Device Stage 要求在 WindowsInfo.xml 中为你的设备将 LaunchDeviceStageOnDeviceConnect 设置为 True</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>Device Stage 要求在 WindowsInfo.xml 中为你的设备将 ShowDeviceInDisconnectedState 设置为 True。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>Device Stage 要求在 WindowsInfo.xml 中为你的设备将 LaunchDeviceStageFromExplorer 设置为 True。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>“设备和打印机”要求在 WindowsInfo.xml 中为你的设备将 LaunchDeviceStageOnDeviceConnect 设置为 False。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>xml 文件 [FileName] 中出现错误：[Error]</p></td>
<td><p>指定的 .xml 文件失败，因为它包含一个或多个错误。 请验证该文件是否符合其相应的架构及命名空间是否正确。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>文件 [FileName] 在 \DeviceStage\Device\[Locale]\ 和 \DeviceStage\Device\ 文件夹中有所不同。</p></td>
<td><p>如果你已经将此包设置为默认区域设置，则该区域设置目录和中性语言目录必须包含相同的文件。</p>
<p>发生以下错误之一：</p>
<ul>
<li><p>具有相同指定名称的文件存在于这两个目录中，但是文件不同。</p></li>
<li><p>指定的文件仅存在于一个目录中。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>PackageInfo.xml 中的 &lt;PackageStructure&gt; 元素需要文件名 PackageInfo.xml。</p></td>
<td><p>未针对你的程序包正确编写你的 PackageInfo.xml 文件。 必须使用 &lt;PackageStructure&gt; 节点在 PackageInfo.xml 文件中引用程序包中的每个根对象。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>PackageInfo.xml 的 &lt;PackageStructure&gt; 元素中的文件名 [FileReference] 不正确。 正确的文件名：PackageInfo.xml</p></td>
<td><p>在 PackageInfo.xml 文件中使用 &lt;PackageStructure&gt; 节点引用的文件名拼写错误。 请更正错误并重新提交你的程序包。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>对于打印和扫描设备，WindowsInfo.xml 中的 LaunchDeviceStageOnDeviceConnect 需要设置为 False。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>此提交中的硬件 ID：[硬件 ID 列表] 不归你的公司所有。</p></td>
<td><p>根据各自的 SIG，列出的硬件 ID 使用不归你的公司所有的 VID。 如果这不正确，请发送电子邮件到 sysdev@microsoft.com 以寻求仪表板支持。</p></td>
</tr>
<tr class="odd">
<td><p>Hardware IDs in this submission: [list of Hardware ID(s)] do not match the expected list of Hardware IDs from SMBIOS.</p></td>
<td><p>你已经提交的硬件 ID 不是根据你随 SMBIOSFields.xml 文件一起提交的 SMBIOS 信息生成的。</p>
<p>请尝试以下解决方案之一：</p>
<ul>
<li><p>重新生成硬件 ID 并将正确的硬件 ID 包括在你的包中。</p></li>
<li><p>更新 SMBIOSFields.xml 文件以包括用于生成正确硬件 ID 的字段。</p></li>
</ul>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>此提交中的硬件 ID：[硬件 ID 列表] 未通过内置驱动程序分发协议 (IDDA) 列表验证。</p></td>
<td><p>你包含在包中的硬件 ID 未列在与 Microsoft 的内置驱动程序分发协议 (IDDA) 中。 删除这些硬件 ID 并重新提交。</p></td>
</tr>
<tr class="odd">
<td><p>Invalid scheme [Scheme] in Allowed Domain for task [TaskID] in Tasks.xml</p></td>
<td><p>URL 必须以 HTTP 或 HTTPS 开头。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>在 PackageInfo.xml 中未找到区域设置或者其不正确</p></td>
<td><p>PackageInfo.xml 文件中的区域设置标记必须存在，正确设置格式且符合 RFC 4646。</p>
<p>请更正区域设置，然后重新提交你的包。</p></td>
</tr>
<tr class="odd">
<td><p>在 \DeviceStage\Task[TaskID][Locale] 文件夹中的 Resource.xml 文件中缺少 [Id] 的资源引用</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>[设备类] 提交不允许使用型号 ID。</p></td>
<td><p>当提交此类型的设备类的设备元数据时，不能使用型号 ID。 而应仅使用你设备的硬件 ID。 要查找计算机设备的硬件 ID，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>在 DeviceInfo.xml 中未找到型号名称</p></td>
<td><p>你的 DeviceInfo.xml 文件编写不正确。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>无法为该组织找到任何预览密钥。</p></td>
<td><p>你必须在上载预览包之前设置 PreviewKey。</p>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules" data-raw-source="[Device Metadata Business Rules](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)">设备元数据业务规则</a>。</p></td>
</tr>
<tr class="odd">
<td><p>PackageStructure node in PackageInfo.xml is invalid.</p></td>
<td><p>确保你的 PackageInfo.xml 文件正确。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>你的设备需要 Behavior.xml 中的任务 [TaskGUID]。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>任务 [TaskID] 不应使用 taskGroupGuid [TaskGroupGuid]</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>对于任务 [TaskId]，TaskGroupGuid [TaskGroupGuid] 不应由你的设备使用</p></td>
<td><p>你正尝试使用不适用于你的设备的保留 GUID。</p>
<p>请尝试以下解决方案之一：</p>
<ul>
<li><p>不要为你的设备不支持的任务使用 GUID。</p></li>
<li><p>如果你正尝试创建任务，请为该任务生成一个新 GUID。</p></li>
</ul>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>对于 Behavior.xml 中的 taskId [TaskId]，TaskGroupGuid 不正确</p></td>
<td><p>更正任务 GUID，然后重新提交包。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>[FolderName] 文件夹中的 [FileName] 图标文件缺失图像 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">MissingImageSize</a>。</p></td>
<td><p>验证该图像大小是否存在。 如果不存在，请将该图像大小添加到图标，然后重新提交包。</p>
<div class="alert">
<strong>注意</strong><br/><p>256x256 图像层必须采用 PNG 压缩格式。 不允许使用此大小的 BMP 格式。 如果存在此大小但属于 BMP 格式，请创建此大小 PNG 格式的图像，将此图像添加到图标，然后重新提交包。</p>
</div>
<div>

</div>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>The [FileName] icon file in [FolderName] 文件夹中的 [FileName] 图标文件缺失图像 [MissingImageSize]</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>cab 友好名称对于体验而言不唯一。 Please choose another name.</p></td>
<td><p>为体验创建新的友好名称，然后重新提交。</p></td>
</tr>
<tr class="odd">
<td><p>对于 Tasks.xml 中的任务 [TaskID]，CommandLine 参数应指向一个有效的 URL，该 URL 以 HTTP 或 HTTPS 开头。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>设备元数据包和徽标提交中所报告的设备类别不匹配。 如果包中的设备类别不正确，请修复后重新上载。 If the device category in Logo Submission is incorrect, please fix in Submission Manager and try uploading your package again: [list of links per offending logo submission to SubmissionManager]</p></td>
<td><p>在绑定的徽标提交和设备元数据之间的设备类别必须相同，提交才能通过。 验证你的徽标提交全都具有相同的设备类别，并且设备类别与你的包的设备类别相同。</p>
<p>提供的链接指向提交管理器，如果类别不正确，你可以使用它更改徽标提交中的设备类别。</p>
<p>在解决所有问题后，重新提交你的包。</p></td>
</tr>
<tr class="odd">
<td><p>The Device Metadata Category for this submission does not exist.</p></td>
<td><p>你使用的设备元数据类别无效。 你必须从 Windows 硬件认证工具包 (HCK) 中概括的预定义设备元数据类别中进行选择。</p></td>
</tr>
<tr class="even">
<td><p>体验名称已存在于该组织中。</p></td>
<td><p>创建具有不同名称的新体验。</p></td>
</tr>
<tr class="odd">
<td><p>The provided Logo submissions do not share Hardware IDs or Model IDs with the Device Metadata submission.</p></td>
<td><p>绑定的徽标提交必须包含体验的设备元数据包中的硬件 ID。</p></td>
</tr>
<tr class="even">
<td><p>The reference in PackageInfo.xml, DeviceInformation, was not found in the package.</p></td>
<td><p>PackageInfo.xml 文件中缺少 DeviceInformation 文件夹引用。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>在程序包中未找到 PackageInfo.xml 中对 DeviceStage 的引用。</p></td>
<td><p>PackageInfo.xml 文件的 &lt;PackageStructure&gt; 元素中的引用拼写错误或不位于程序包的根目录中。 删除引用，或添加正确的文件或目录。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>在程序包中未找到 PackageInfo.xml 中对 WindowsInformation 的引用。</p></td>
<td><p>PackageInfo.xml 文件中缺少 WindowsInformation 文件夹引用。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>提交包含徽标提交未覆盖的 [硬件 ID 和/或型号 ID 的列表]。</p></td>
<td><p>你的包包含你的徽标提交未覆盖的硬件 ID 或型号 ID。</p>
<p>请尝试以下解决方案之一：</p>
<ul>
<li><p>更正你的设备元数据包中的硬件 ID 或型号 ID。</p></li>
<li><p>创建一个新体验并且仅绑定关联的徽标提交。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>The system manufacturer for this computer submission does not match the organization of the submitting user.</p></td>
<td><p>你提交的 SMBIOSFields.xml 文件中的系统制造商不匹配我们记录中的制造商。</p>
<p>请尝试以下解决方案之一：</p>
<ul>
<li><p>更正系统制造商的名称，然后重新提交包。</p></li>
<li><p>如果系统制造商字段正确，但你的文件未通过，请向仪表板支持部门发送电子邮件：sysdev@microsoft.com。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>The TaskID [TaskID] cannot be used with multiple TaskGroups.</p></td>
<td><p>你的 Device Stage 包包含用于不同 TaskGroup 的 TaskID。 每个 TaskGroup 和每个任务的 TaskID 必须唯一。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>此预览密钥已被拒绝。 请选择另一个值。</p></td>
<td><p>你使用仪表板设置的 PreviewKey 未被接受。 请提交新的 PreviewKey。</p></td>
</tr>
<tr class="odd">
<td><p>Unexpected file found in [FolderName] folder- [ExtraFile]</p></td>
<td><p>你的包结构存在问题。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>在 [Path] 文件夹中找到非预期文件 - [ExtraFile]</p></td>
<td><p>你的包结构存在问题。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>在任务 [TaskGroupGuid] 文件夹的 [locale] 子文件夹中找到非预期文件 – [FileName]</p></td>
<td><p>删除指定文件，然后重新提交包。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>在 [FolderName] 文件夹中找到非预期文件夹 - [ExtraFolder]</p></td>
<td><p>你的包结构存在问题。</p>
<div class="alert">
<strong>注意</strong><br/><p>如果 DeviceInfo.xml 文件中的设备类别未正确设置，则可能出现此错误。</p>
</div>
<div>

</div>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>在 [Path] 文件夹中找到非预期文件夹 - [ExtraFolder]</p></td>
<td><p>你的包结构存在问题。</p>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>对于 Tasks.xml 中的任务 [TaskID]，URL 不应为 localhost。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="odd">
<td><p>对于 Tasks.xml 中的任务 [TaskID]，命令行中指定的 URL 无效。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>[DeviceClass] 的 [SubmissionType] 元数据需要有效的提交 orare</p></td>
<td><p>数码相机和便携式媒体播放机必须具有一个或多个 Windows 7 或 Windows Vista® 徽标提交。</p>
<p>移动电话必须具有一个或多个 Windows 7 徽标提交。</p></td>
</tr>
<tr class="odd">
<td><p>You already have a preview submission for this Operating System Version. Remove the current Live submission.</p></td>
<td><p>你正在尝试为某个区域设置提升预览包，但是该区域设置已经有一个发布的包。</p>
<p>如果你希望提升此预览包，请首先删除发布的包，然后重试。</p></td>
</tr>
<tr class="even">
<td><p>You do not have access to this experience.</p></td>
<td><p>你正在尝试获取对不属于你的公司的体验的访问权限。</p></td>
</tr>
<tr class="odd">
<td><p>对于 Tasks.xml 中的任务 [TaskID]，你的设备无法将命令值设置为 HostedSiteWithDevice。</p></td>
<td><p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?LinkId=241658" data-raw-source="[Microsoft Device Experience Development Kit](https://go.microsoft.com/fwlink/p/?LinkId=241658)">Microsoft 设备使用体验开发工具包</a>。</p></td>
</tr>
<tr class="even">
<td><p>你的提交因仪表板错误而被阻止。 请发送电子邮件到 sysdev@microsoft.com 以寻求仪表板支持来解决问题。</p></td>
<td><p>请发送电子邮件到 sysdev@microsoft.com 以寻求仪表板支持。</p></td>
</tr>
</tbody>
</table>



## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[创建设备元数据体验](https://docs.microsoft.com/windows-hardware/drivers/dashboard/create-a-device-metadata-experience)

[提交设备元数据包（仪表板帮助）](https://docs.microsoft.com/windows-hardware/drivers/dashboard/submit-a-device-metadata-package--dashboard-help-)

[设备元数据业务规则](https://docs.microsoft.com/windows-hardware/drivers/dashboard/device-metadata-business-rules)










