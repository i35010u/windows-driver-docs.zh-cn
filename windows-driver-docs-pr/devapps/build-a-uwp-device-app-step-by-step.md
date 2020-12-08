---
title: 分步构建 UWP 设备应用
description: 此分步指南详细介绍了如何使用 Microsoft Visual Studio 和设备元数据创作向导构建 UWP 设备应用。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1da0f2d8d1df7861d1a1536fc4a1029f7744250
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802693"
---
# <a name="span-iddevappsbuild_a_windows_store_device_app_step-by-stepspanbuild-a-uwp-device-app-step-by-step"></a><span id="devapps.build_a_windows_store_device_app_step-by-step"></span>逐步生成 UWP 设备应用


此分步指南详细介绍了如何使用 Microsoft Visual Studio 和设备元数据创作向导构建 UWP 设备应用。 有关此过程的详细介绍，请参阅 [构建 UWP 设备应用](the-workflow.md)。

UWP 设备应用是一种特殊类型的 UWP 应用，设备制造商可以创建它来充当其内部或外围设备。 通过使用设备元数据，设备应用可以运行特权操作并在设备接通电源时自动安装。 有关 UWP 设备应用的详细信息，请参阅 " [满足 uwp 设备应用](meet-uwp-device-apps.md)"。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="step-1--create-a-uwp-device-app.md" data-raw-source="[Step 1: Create a UWP device app](step-1--create-a-uwp-device-app.md)">步骤1：创建 UWP 设备应用</a></p></td>
<td align="left"><p>本主题介绍使用 Visual Studio 创建 UWP 设备应用的基本过程。 了解所有 UWP 设备应用共用的任务。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="step-2--create-device-metadata.md" data-raw-source="[Step 2: Create device metadata](step-2--create-device-metadata.md)">步骤2：创建设备元数据</a></p></td>
<td align="left"><p>本主题介绍如何使用 <strong>设备元数据创作向导</strong> 来创建将 UWP 设备应用与设备关联的新设备元数据。 向导还可以创建一个 <strong>StoreManfest.xml</strong> 文件，该文件可能需要在下一步中添加到应用中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="step-3--add-an-experience-id-to-the-app.md" data-raw-source="[Step 3: Add an experience ID to the app](step-3--add-an-experience-id-to-the-app.md)">步骤3：将体验 ID 添加到应用</a></p></td>
<td align="left"><p>本主题介绍如何将体验 ID 添加到 UWP 设备应用。 <em>体验 ID</em>是一个 GUID，用于唯一标识设备元数据包;如果你的应用程序已配置为自动安装，则这是必需的，因为适用于打印机和<a href="uwp-device-apps-for-webcams.md" data-raw-source="[cameras](uwp-device-apps-for-webcams.md)">照相机</a>的<a href="uwp-device-apps-for-printers.md" data-raw-source="[UWP device apps for printers](uwp-device-apps-for-printers.md)">UWP 设备应用</a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="step-4--test-device-metadata.md" data-raw-source="[Step 4: Test device metadata](step-4--test-device-metadata.md)">步骤4：测试设备元数据</a></p></td>
<td align="left"><p>本主题介绍如何在将 UWP 设备应用提交到 Windows 开发人员中心仪表板之前，对其进行本地测试。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="step-5--submit-the-app.md" data-raw-source="[Step 5: Submit the app](step-5--submit-the-app.md)">步骤5：提交应用</a></p></td>
<td align="left"><p>本主题介绍如何将 UWP 设备应用提交到 Microsoft Store 仪表板。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="step-6--submit-device-metadata.md" data-raw-source="[Step 6: Submit device metadata](step-6--submit-device-metadata.md)">步骤6：提交设备元数据</a></p></td>
<td align="left"><p>本主题介绍如何向 Windows 开发人员中心硬件仪表板提交 UWP 设备应用的设备元数据。</p></td>
</tr>
</tbody>
</table>

 

 

 





