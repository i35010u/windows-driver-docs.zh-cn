---
title: 适用于打印机的 UWP 设备应用
description: 此部分介绍打印机的 UWP 设备应用。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf16a6120e2014e9ac2206aa53f7266c9455dc6b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802659"
---
# <a name="uwp-device-apps-for-printers"></a>适用于打印机的 UWP 设备应用


此部分介绍打印机的 UWP 设备应用。 UWP 设备应用可以通过自定义的打印设置浮出控件和通知支持突出显示打印机的特殊功能。 UWP 设备应用还可以显示打印机状态、管理打印作业和执行打印机维护任务。 若要详细了解 UWP 设备应用的详细信息，请参阅了解 [uwp 设备应用](meet-uwp-device-apps.md)。

**重要提示**  若要使用 UWP 设备应用功能，打印机必须支持 v4 打印驱动程序模型。 有关详细信息，请参阅 [开发 v4 打印驱动程序](../print/v4-printer-driver.md)。

 

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
<td align="left"><p><a href="how-to-display-printer-status.md" data-raw-source="[How to display printer status](how-to-display-printer-status.md)">如何显示打印机状态</a></p></td>
<td align="left"><p>本主题使用 " <a href="https://go.microsoft.com/fwlink/p/?LinkID=242862" data-raw-source="[Print settings and print notifications](https://go.microsoft.com/fwlink/p/?LinkID=242862)">打印设置" 和 "打印通知</a> " 示例的 c # 版本来演示如何查询打印机状态并显示该状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="how-to-customize-print-settings.md" data-raw-source="[How to customize print settings](how-to-customize-print-settings.md)">如何自定义打印设置</a></p></td>
<td align="left"><p>本主题介绍 "高级打印设置" 浮出控件，并演示 c # 版本的 " <a href="https://go.microsoft.com/fwlink/p/?LinkID=242862" data-raw-source="[Print settings and print notifications](https://go.microsoft.com/fwlink/p/?LinkID=242862)">打印设置" 和 "打印通知</a> " 示例如何使用自定义浮出控件替换默认浮出控件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="working-with-print-notifications.md" data-raw-source="[Working with print notifications](working-with-print-notifications.md)">处理打印通知</a></p></td>
<td align="left"><p>本主题介绍打印通知，并演示 c # 版本的 <a href="https://go.microsoft.com/fwlink/p/?LinkID=242862" data-raw-source="[Print settings and print notifications](https://go.microsoft.com/fwlink/p/?LinkID=242862)">打印设置和打印通知</a> 示例如何使用后台任务来响应打印通知。 后台任务演示了如何将通知详细信息保存在本地应用程序数据存储区中，发送 toast 并更新磁贴和徽章。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="how-to-manage-print-jobs.md" data-raw-source="[How to manage print jobs](how-to-manage-print-jobs.md)">如何管理打印作业</a></p></td>
<td align="left"><p>在 Windows 8.1 中，用于打印机的 UWP 设备应用可以管理打印作业。 本主题使用 <a href="https://go.microsoft.com/fwlink/p/?LinkID=299829" data-raw-source="[Print job management and printer maintenance](https://go.microsoft.com/fwlink/p/?LinkID=299829)">打印作业管理和打印机维护</a> 示例的 c # 版本来演示如何创建打印作业的视图、监视这些作业，并在必要时取消作业。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="how-to-do-printer-maintenance.md" data-raw-source="[How to do printer maintenance](how-to-do-printer-maintenance.md)">如何执行打印机维护</a></p></td>
<td align="left"><p>在 Windows 8.1 中，UWP 设备应用可以执行打印机维护，如对齐打印头和清洁喷嘴。 本主题使用 <a href="https://go.microsoft.com/fwlink/p/?LinkID=299829" data-raw-source="[Print job management and printer maintenance](https://go.microsoft.com/fwlink/p/?LinkID=299829)">打印作业管理和打印机维护</a> 示例的 c # 版本来演示如何使用双向通信 () 双向通信来执行此类设备维护。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="printer-extension-library-overview.md" data-raw-source="[Printer extension library overview](printer-extension-library-overview.md)">打印机扩展库概述</a></p></td>
<td align="left"><p>本主题介绍了打印机扩展库，这是一个可帮助设备制造商为其打印机写入 UWP 设备应用程序的库。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idshould_i_create_a_windows_store_device_app_for_my_printer_spanspan-idshould_i_create_a_windows_store_device_app_for_my_printer_spanspan-idshould_i_create_a_windows_store_device_app_for_my_printer_spanshould-i-create-a-uwp-device-app-for-my-printer"></a><span id="Should_I_create_a_Windows_Store_device_app_for_my_printer_"></span><span id="should_i_create_a_windows_store_device_app_for_my_printer_"></span><span id="SHOULD_I_CREATE_A_WINDOWS_STORE_DEVICE_APP_FOR_MY_PRINTER_"></span>我是否应该为打印机创建 UWP 设备应用？


如果要执行以下操作，请使用适用于打印机的 UWP 设备应用：

-   突出显示高级设备功能，如每页打印多张照片。
-   做出特定于设备的建议。 例如，你可以使用设备应用来显示映像管理选项，或提供设置和保存特定于打印机的默认值的方法。

## <a name="span-idgeneral_recommendationsspanspan-idgeneral_recommendationsspanspan-idgeneral_recommendationsspangeneral-recommendations"></a><span id="General_recommendations"></span><span id="general_recommendations"></span><span id="GENERAL_RECOMMENDATIONS"></span>一般建议


-   在调用窗口后，打印 ( # A1，在您的应用程序的 "打印" 按钮的 onClick 事件处理程序内检查并处理错误消息。 这允许你的应用程序在不使用打印机的情况下中止打印请求。
-   如果打印失败，通知用户，如果可能，还会说明失败的原因。
-   如果打算自定义打印体验，请将此代码分隔到打印助理应用。 这使您可以化为您的代码，并简化测试和调试过程。
-   请勿尝试自定义打印体验来使用 V3 打印驱动程序。
-   不要在您的自定义打印 UI 中公布打印设备的附件。
-   不显示与调用 Microsoft Store 设备应用的原因无关的销售项目。 例如，在用户单击通知后显示购买的打印墨盒，提醒他们墨迹太低。 但是，在这种情况下，也不适合尝试销售打印电缆或照片打印工具包。
-   不要将用户重定向到公司的网站以获得更多产品销售额。
-   不要提供与设置打印首选项的任务无关的信息。 例如，不要提供有关如何清洁打印头或如何对齐和测试打印喷嘴的信息。

## <a name="span-idsamplesspanspan-idsamplesspanspan-idsamplesspansamples"></a><span id="Samples"></span><span id="samples"></span><span id="SAMPLES"></span>范例


打印机的 UWP 设备应用示例演示了可以在自己的 UWP 设备应用中实现的与打印机相关的功能。 每个示例还包含 `PrinterExtensionLibrary` 项目，可以在自己的应用程序中重复使用，以帮助打印扩展。 打印机扩展库将 [打印机扩展接口](/windows-hardware/drivers/ddi/_print/) 的 COM 实现从 v4 打印驱动程序中换行。


**Windows 8 示例：**

-   [打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例演示如何使用双向通信 () 双向通信来管理打印作业和执行打印机维护任务。

-   " [打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862) " 示例演示如何创建一个 UWP 设备应用，该应用提供高级打印设置的自定义浮出控件，可以显示打印机状态，并且可以在磁贴或 toast 中显示打印机通知。


**Windows 10 示例：**

-   " [编写打印工作流应用程序并将 WSDAs 迁移到 UWP](https://github.com/microsoft/print-oem-samples) " 示例显示 OEM 打印伙伴如何使用 "打印工作流" 功能，以及如何将现有 Windows 应用商店设备应用 (WSDAs) 代码迁移到通用 Windows 平台。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发 v4 打印驱动程序](../print/v4-printer-driver.md)

[ (v4 打印驱动程序的打印机扩展接口) ](/windows-hardware/drivers/ddi/_print/)

[双向通信](../print/bidirectional-communication.md)

[UWP 应用入门](getting-started.md)

[ (分步指南创建 UWP 设备应用) ](step-1--create-a-uwp-device-app.md)

[ (分步指南创建 UWP 设备应用的设备元数据) ](step-2--create-device-metadata.md)

 

