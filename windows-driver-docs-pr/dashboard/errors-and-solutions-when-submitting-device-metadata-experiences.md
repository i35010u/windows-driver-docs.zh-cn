---
title: 提交设备元数据体验时的错误和解决方案
description: 提交设备元数据体验时的错误和解决方案
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37a139239754f5767a357bebd68b7237b70ca7f1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800375"
---
# <a name="errors-and-solutions-when-submitting-device-metadata-experiences"></a>提交设备元数据体验时的错误和解决方案

当你提交设备元数据体验以进行验证和发布时，你可能会看到影响体验发布的错误。

## <a name="common-errors"></a>常见错误

下面列出了一些最常见的错误，它们以字母顺序列出并包括解决方案（如果已提供）。

### <a name="to-solve-common-errors"></a>解决常见错误的步骤

|错误|建议的解决方案|
|----|----|
|:::no-loc text="\[CategoryName] Category id is incorrect in Behavior.xml. Correct Category id is \[CategoryId]"::: | 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。 |
|:::no-loc text="\[CategoryName] Guid \[CategoryId] is required for your device in Behavior.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="\[FolderName] folder is missing.":::|你的一个文件夹已丢失。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="\[FolderName] folder name is required in <PackageStructure> element in PackageInfo.xml.":::|你必须在 PackageInfo.xml 中包括正确的文件夹名称引用。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="\[ImageType] Image – \[FileName] size for \[SplitType] split is invalid. Valid size(s) are: \[ListOfAllowedSizes]":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="\[ImageType] Image – \[FileName] size is invalid. Valid size(s) are: \[ListOfAllowedSizes]":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="\[TaskGroupName] Guid \[TaskGroupGuid] is not referenced for the task \[TaskId] in Behavior.xml":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="\[TaskName] Task – \[TaskId] is required for your device within the System Settings category in Behavior.xml.":::|你的设备的“操作中心”任务和“系统设置”任务必须出现在 Device Stage 中的“系统设置”类别下。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="\[TaskName] Task – \[TaskId] should reference taskGroupGuid \[TaskGroupGuid] for your device in Behavior.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="\[TaskName] task \[TaskId] is required to exist at root for your device in Behavior.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="\DeviceStage\Device\[Locale]\ and \DeviceStage\Device\ folders should have same files.":::|如果将此包设置为默认区域设置，则该区域设置目录和中性语言目录必须具有相同的文件。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))">。|
|:::no-loc text="A .cab submission needs to contain either Hardware and/or Model information. Please correct the .cab or modify the existing .cabs.":::|你的包必须至少包含一个硬件 ID 或型号 ID。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="A Hardware ID in this .cab is in conflict and the .cab cannot be uploaded. Please ensure no other experience you have created uses this Hardware ID.":::|你的硬件 ID 已经在你的另一个体验中使用。 在仪表板上的“设备元数据”  下，打开“管理体验”  页。 在筛选器中，输入硬件 ID 以查找其他体验。 然后，你可以解决任何冲突。 有关详细信息，请参阅[设备元数据业务规则](./device-metadata-business-rules.md)。|
|:::no-loc text="A Hardware ID in this. cab is in use by another company and the .cab cannot be uploaded. Please verify this Hardware ID.":::|你已经包含在包中的硬件 ID 正由另一个公司使用。 你无法提交另一个公司的硬件 ID。 确保你的硬件 ID 拼写正确。 如果仍然收到错误消息，请联系仪表板支持部门。|
|:::no-loc text="A live submission already exists for this locale in this experience.":::|删除此区域设置的现有实时包，然后再为同一个区域设置上载新包。|
|:::no-loc text="A live submission already exists with default locale set to true in this experience.":::|只能将体验中的一个实时包设置为默认包。 有关详细信息，请参阅[设备元数据业务规则](./device-metadata-business-rules.md)。|
|:::no-loc text="A logo submission for a MultiPurpose device does not match the submission category.":::|列在徽标提交中的设备类别不匹配你的设备元数据包的主要设备类别。 要解决此问题，请执行下列步骤：<br/> \- 更正你的徽标提交的设备类别。<br/>\- 创建一个新体验并且仅绑定正确的徽标提交。|
|:::no-loc text="A Model ID in this cab is in conflict and the cab cannot be uploaded. Please ensure no other experience you have created uses this Model ID.":::|你的型号 ID 已经在你的另一个体验中使用。 在仪表板上的“设备元数据”  下，打开“管理体验”  页。 在筛选器中，输入型号 ID 以查找其他体验。 然后，你可以解决任何冲突。 有关详细信息，请参阅[设备元数据业务规则](./device-metadata-business-rules.md)。|
|:::no-loc text="A Model ID in this cab is in use by another company and the cab cannot be uploaded. Please verify this Model ID.":::|你已经包含在包中的型号 ID 正由另一个公司使用。 你无法提交另一个公司的型号 ID。 确保你的型号 ID 拼写正确。 如果你仍然收到错误消息，请发送电子邮件到 sysdev@microsoft.com 以寻求仪表板支持来解决问题。|
|:::no-loc text="A non-preview live package cannot be promoted to live.":::|你不能将实时包提升为“实时”状态。|
|:::no-loc text="A package with a status of error cannot be promoted to live.":::|你不能将包含错误的包提升为“实时”状态。|
|:::no-loc text="A preview submission already exists for this locale in this experience.":::|要解决此问题，请尝试执行下列步骤：<br/> \- 删除此区域设置的现有预览包，然后为同一个区域设置上载新预览包。<br/>\- 将此区域设置的当前预览包提升为“发布”状态，然后为同一个区域设置上载新预览包。|
|:::no-loc text="A preview submission already exists with default locale set to true in this experience.":::|只能将体验中的一个预览包设置为默认包。 有关详细信息，请参阅[设备元数据业务规则](./device-metadata-business-rules.md)。|
|:::no-loc text="All device metadata .cab files in an experience must support the same Hardware IDs. Please correct the .cab.":::|此包不具有该体验中的其他包所具有的相同型号 ID 列表。 更正此包中的型号 ID 列表，然后再次上载此包。 有关详细信息，请参阅[设备元数据业务规则](./device-metadata-business-rules.md)。|
|:::no-loc text="Allowed Domain should not be empty for task [TaskID] in Tasks.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="An unexpected file was found:'\[ExtraFile]'. Please ensure you follow the architecture or reference all root files in PackageInfo.xml.":::|在包的根目录处存在额外的文件。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="An unexpected folder was found: ‘\[ExtraFolder]'. Please ensure you follow the architecture or reference all root folders in PackageInfo.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="CommandLine URL should not be null for task \[TaskID] in Tasks.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Device Category not found in DeviceInfo.xml .":::|你必须设置主要设备类别，它是预定义的选项之一。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Device folder not found in \DeviceStage\ folder":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Device icon information not found in DeviceInfo.xml":::|如果你将某个设备图标包含在 DeviceInfo.xml 文件中，还必须包含设备图标信息。 Device Stage 包需要有设备图标。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Device Metadata Category for this submission needs to match the existing experience category.":::|此包中的设备类别不匹配此体验其他包中的类别。 修改你的设备类别并重新提交此包。|
|:::no-loc text="Device Metadata Submission Type for this submission needs to match the existing experience category.":::| 设备元数据提交类型被定义为 Device Stage 或“设备和打印机”。 只有 Device Stage 包可以包含在 Device Stage 体验中。 同样，只有“设备和打印机”包可以包含在“设备和打印机”体验中。|
|:::no-loc text="Device Stage inbox submissions are not allowed for the computer device class.":::|如果你的包和体验用于 Device Stage 和计算机设备，你必须已经对它们进行徽标认证，或者你必须在 90 天内对它们进行徽标认证。|
|:::no-loc text="Device Stage is not supported for this device.":::|在 Device Stage 中不支持你选择的设备类别。|
|:::no-loc text="Device Stage metadata cannot be submitted for your device \[DeviceCategory]":::|仅允许为以下设备进行 Device Stage 提交：<br/>\- 便携式媒体播放机<br/>\- 数码相机<br/>\- 移动电话<br/>\- 打印机或传真机<br/>\- 扫描仪<br/>\-计算机系统|
|:::no-loc text="Device Stage requires either Marketing Bullets or Status Items to be present in Behavior.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Device Stage requires LaunchDeviceStageFromExplorer to be set to true for your device in WindowsInfo.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Device Stage requires LaunchDeviceStageOnDeviceConnect to be set to True for your device in WindowsInfo.xml":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Device Stage requires ShowDeviceInDisconnectedState to be set to True for your device in WindowsInfo.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Devices and Printers requires LaunchDeviceStageFromExplorer to be set to False for your device in WindowsInfo.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Devices and Printers requires LaunchDeviceStageOnDeviceConnect to be set to False for your device in WindowsInfo.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Error in xml file \[FileName] : \[Error]":::|指定的 .xml 文件失败，因为它包含一个或多个错误。 请验证该文件是否符合其相应的架构及命名空间是否正确。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="File \[FileName] is different in \DeviceStage\Device\[Locale]\ and \DeviceStage\Device\ folders.":::|如果你已经将此包设置为默认区域设置，则该区域设置目录和中性语言目录必须包含相同的文件。 发生以下错误之一： <br/>\- 具有相同指定名称的文件存在于这两个目录中，但是文件不同。<br/>\- 指定的文件仅存在于一个目录中。|
|:::no-loc text="File Name PackageInfo.xml is expected in &lt;PackageStructure&gt; element in PackageInfo.xml.":::|未针对你的程序包正确编写你的 PackageInfo.xml 文件。 必须使用 <PackageStructure> 节点在 PackageInfo.xml 文件中引用程序包中的每个根对象。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Filename \[FileReference] is incorrect in <PackageStructure> element in PackageInfo.xml. Correct filename: PackageInfo.xml":::|在 PackageInfo.xml 文件中使用 <PackageStructure> 节点引用的文件名拼写错误。 请更正错误并重新提交你的程序包。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="For Printing and Scanning Devices, LaunchDeviceStageOnDeviceConnect needs to be set to False in WindowsInfo.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="HardwareIDs in this submission: [list of Hardware ID(s)] are not owned by your company.":::|根据各自的 SIG，列出的硬件 ID 使用不归你的公司所有的 VID。 如果这不正确，请联系仪表板支持部门。|
|:::no-loc text="Hardware IDs in this submission: \[list of Hardware ID(s)] do not match the expected list of Hardware IDs from SMBIOS.":::|你已经提交的硬件 ID 不是根据你随 SMBIOSFields.xml 文件一起提交的 SMBIOS 信息生成的。 请尝试以下解决方案之一：<br>\- 重新生成硬件 ID 并将正确的硬件 ID 包括在你的包中。<br/>\- 更新 SMBIOSFields.xml 文件以包括用于生成正确硬件 ID 的字段。<br/>有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Hardware IDs in this submission: [list of Hardware ID(s)] fail the Inbox Driver Distribution Agreement (IDDA) list validation.":::|你包含在包中的硬件 ID 未列在与 Microsoft 的内置驱动程序分发协议 (IDDA) 中。 删除这些硬件 ID 并重新提交。|
|:::no-loc text="Invalid scheme \[Scheme] in Allowed Domain for task \[TaskID] in Tasks.xml":::|URL 必须以 HTTP 或 HTTPS 开头。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Locale not found or is incorrect in PackageInfo.xml":::|PackageInfo.xml 文件中的区域设置标记必须存在，正确设置格式且符合 RFC 4646。 请更正区域设置，然后重新提交你的包。|
|:::no-loc text="Missing resource reference for \[Id] in Resource.xml file in \DeviceStage\Task\[TaskID]\[Locale] folder":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Model IDs are not allowed for [Device Class] submissions.":::|当提交此类型的设备类的设备元数据时，不能使用型号 ID。 而应仅使用你设备的硬件 ID。 要查找计算机设备的硬件 ID，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Model Name not found in DeviceInfo.xml":::|你的 DeviceInfo.xml 文件编写不正确。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="No preview key can be found for this organization.":::|你必须在上载预览包之前设置 PreviewKey。 有关详细信息，请参阅[设备元数据业务规则](./device-metadata-business-rules.md)。|
|:::no-loc text="PackageStructure node in PackageInfo.xml is invalid.":::|确保你的 PackageInfo.xml 文件正确。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Task \[TaskGUID] is required for your device in Behavior.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Task \[TaskID] should not use taskGroupGuid \[TaskGroupGuid]":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="TaskGroupGuid \[TaskGroupGuid] should not be used by your device for task \[TaskId]":::|你正尝试使用不适用于你的设备的保留 GUID。 请尝试以下解决方案之一：<br/>\- 不要为你的设备不支持的任务使用 GUID。<br/>\- 如果你正尝试创建任务，请为该任务生成一个新 GUID。<br/>有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="TaskGroupGuid incorrect for taskId \[TaskId] in Behavior.xml":::|更正任务 GUID，然后重新提交包。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="The \[FileName] icon file in \[FolderName] folder is missing image MissingImageSize.":::|验证该图像大小是否存在。 如果不存在，请将该图像大小添加到图标，然后重新提交包。<br/><br/>**注意**   256x256 图像层必须采用 PNG 压缩格式。 不允许使用此大小的 BMP 格式。 如果存在此大小但属于 BMP 格式，请创建此大小 PNG 格式的图像，将此图像添加到图标，然后重新提交包。 <br/><br/>有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="The cab Friendly Name is not unique to the Experience. Please choose another name.":::|为体验创建新的友好名称，然后重新提交。|
|:::no-loc text="The CommandLine argument should point to a valid URL beginning with HTTP or HTTPS for task \[TaskID] in Tasks.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="The device category reported in your Device Metadata package and Logo Submission don't match. If the device category in the package is incorrect, please fix and upload again. If the device category in Logo Submission is incorrect, please fix in Submission Manager and try uploading your package again: [list of links per offending logo submission to SubmissionManager]":::|在绑定的徽标提交和设备元数据之间的设备类别必须相同，提交才能通过。 验证你的徽标提交全都具有相同的设备类别，并且设备类别与你的包的设备类别相同。 提供的链接指向提交管理器，如果类别不正确，你可以使用它更改徽标提交中的设备类别。 在解决所有问题后，重新提交你的包。|
|:::no-loc text="The Device Metadata Category for this submission does not exist.":::|你使用的设备元数据类别无效。 你必须从 Windows 硬件认证工具包 (HCK) 中概括的预定义设备元数据类别中进行选择。|
|:::no-loc text="The Experience name already exists for this organization.":::|创建具有不同名称的新体验。|
|:::no-loc text="The provided Logo submissions do not share Hardware IDs or Model IDs with the Device Metadata submission.":::|绑定的徽标提交必须包含体验的设备元数据包中的硬件 ID。|
|:::no-loc text="The reference in PackageInfo.xml, DeviceInformation, was not found in the package.":::|PackageInfo.xml 文件中缺少 DeviceInformation 文件夹引用。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="The reference in PackageInfo.xml, DeviceStage, was not found in the package.":::|PackageInfo.xml 文件的 &lt;PackageStructure&gt; 元素中的引用拼写错误或不位于程序包的根目录中。 删除引用，或添加正确的文件或目录。 <p>有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="The reference in PackageInfo.xml, WindowsInformation, was not found in the package.":::|PackageInfo.xml 文件中缺少 WindowsInformation 文件夹引用。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="The submission contains [list of Hardware ID(s) and/or Model ID(s)] that are not covered via a logo submission.":::|你的包包含你的徽标提交未覆盖的硬件 ID 或型号 ID。 请尝试以下解决方案之一：<br/>\- 更正你的设备元数据包中的硬件 ID 或型号 ID。<br/>\- 创建一个新体验并且仅绑定关联的徽标提交。|
|:::no-loc text="The system manufacturer for this computer submission does not match the organization of the submitting user.":::|你提交的 SMBIOSFields.xml 文件中的系统制造商不匹配我们记录中的制造商。 请尝试以下解决方案之一：<br/>\- 更正系统制造商的名称，然后重新提交包。<br/>\- 如果系统制造商字段正确，但你的文件未通过，请向仪表板支持部门发送电子邮件：sysdev@microsoft.com。|
|:::no-loc text="The TaskID \[TaskID] cannot be used with multiple TaskGroups.":::|你的 Device Stage 包包含用于不同 TaskGroup 的 TaskID。 每个 TaskGroup 和每个任务的 TaskID 必须唯一。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="This preview key has been rejected. Please choose another value.":::|你使用仪表板设置的 PreviewKey 未被接受。 请提交新的 PreviewKey。|
|:::no-loc text="Unexpected file found in \[FolderName] folder- \[ExtraFile]":::|你的包结构存在问题。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Unexpected file found in \[Path] folder – \[ExtraFile]":::|你的包结构存在问题。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Unexpected file found in the \[locale] subfolder of task \[TaskGroupGuid] folder – \[FileName]":::|删除指定文件，然后重新提交包。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Unexpected folder found in \[FolderName] folder- \[ExtraFolder]":::|你的包结构存在问题。 <br/><br/>**注意**   如果 DeviceInfo.xml 文件中的设备类别未正确设置，则可能出现此错误。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Unexpected folder found in \[Path] folder – \[ExtraFolder]":::|你的包结构存在问题。 有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="URL should not be a localhost for task \[TaskID] in Tasks.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="URL specified in the commandLine is not valid for task \[TaskID] in Tasks.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Valid logo submission(s) are needed for \[SubmissionType] metadata for \[DeviceClass]":::|数码相机和便携式媒体播放机必须具有一个或多个 Windows 7 或 Windows Vista® 徽标提交。 移动电话必须具有一个或多个 Windows 7 徽标提交。|
|:::no-loc text="You already have a preview submission for this Operating System Version. Remove the current Live submission.":::|你正在尝试为某个区域设置提升预览包，但是该区域设置已经有一个发布的包。 如果你希望提升此预览包，请首先删除发布的包，然后重试。|
|:::no-loc text="You do not have access to this experience.":::|你正在尝试获取对不属于你的公司的体验的访问权限。|
|:::no-loc text="Your device cannot have the command value set to HostedSiteWithDevice for task \[TaskID] in Tasks.xml.":::|有关详细信息，请参阅 [Microsoft 设备使用体验开发工具包](/previous-versions/windows/hardware/device-stage/dn629504(v=vs.85))。|
|:::no-loc text="Your submission is blocked due to a Dashboard error. Please email Dashboard Support at sysdev@microsoft.com for a resolution.":::|请联系仪表板支持部门。|

## <a name="related-topics"></a>相关主题

[创建设备元数据体验](./create-a-device-metadata-experience.md)

[提交设备元数据包（仪表板帮助）](./submit-a-device-metadata-package--dashboard-help-.md)

[设备元数据业务规则](./device-metadata-business-rules.md)
