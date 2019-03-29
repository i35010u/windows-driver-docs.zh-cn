---
title: 适用于打印机的 UWP 设备应用
description: 此部分介绍打印机的 UWP 设备应用。
ms.assetid: 3325B492-2A70-4EB7-99B0-3FE3E24CE398
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 881528423e31121f8e6705ab7bd2f86ca9a83e9f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564359"
---
# <a name="uwp-device-apps-for-printers"></a>适用于打印机的 UWP 设备应用


此部分介绍打印机的 UWP 设备应用。 UWP 的设备应用程序可以突出显示的自定义打印设置浮出控件通过打印机的特殊功能并通知支持。 UWP 的设备应用程序还可以显示打印机状态、 管理的打印作业，并执行打印机维护任务。 若要在一般情况下了解有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

**重要**  若要使用 UWP 的设备应用程序功能，您的打印机必须支持 v4 打印驱动程序模型。 有关详细信息，请参阅[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)。

 

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


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
<td align="left"><p>本主题使用C#的版本<a href="https://go.microsoft.com/fwlink/p/?LinkID=242862" data-raw-source="[Print settings and print notifications](https://go.microsoft.com/fwlink/p/?LinkID=242862)">打印设置和打印通知</a>示例，用于演示如何查询打印机状态并将其显示。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="how-to-customize-print-settings.md" data-raw-source="[How to customize print settings](how-to-customize-print-settings.md)">如何自定义打印设置</a></p></td>
<td align="left"><p>本主题介绍在高级打印设置浮出控件，并演示如何将C#的版本<a href="https://go.microsoft.com/fwlink/p/?LinkID=242862" data-raw-source="[Print settings and print notifications](https://go.microsoft.com/fwlink/p/?LinkID=242862)">打印设置和打印通知</a>示例使用自定义的浮出控件替换默认浮出控件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="working-with-print-notifications.md" data-raw-source="[Working with print notifications](working-with-print-notifications.md)">使用打印通知</a></p></td>
<td align="left"><p>本主题介绍打印通知，并演示如何将C#的版本<a href="https://go.microsoft.com/fwlink/p/?LinkID=242862" data-raw-source="[Print settings and print notifications](https://go.microsoft.com/fwlink/p/?LinkID=242862)">打印设置和打印通知</a>示例使用后台任务响应打印通知。 后台任务演示如何保存通知中的本地应用程序数据的详细信息存储、 发送 toast，和更新磁贴和徽章。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="how-to-manage-print-jobs.md" data-raw-source="[How to manage print jobs](how-to-manage-print-jobs.md)">如何管理打印作业</a></p></td>
<td align="left"><p>在 Windows 8.1，UWP 应用的打印机的设备应用程序可以管理打印作业。 本主题使用C#的版本<a href="https://go.microsoft.com/fwlink/p/?LinkID=299829" data-raw-source="[Print job management and printer maintenance](https://go.microsoft.com/fwlink/p/?LinkID=299829)">打印作业管理和打印机维护</a>示例，用于演示如何创建一个视图的打印作业、 监视这些作业，并如有必要，取消的作业。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="how-to-do-printer-maintenance.md" data-raw-source="[How to do printer maintenance](how-to-do-printer-maintenance.md)">如何执行操作的打印机的维护</a></p></td>
<td align="left"><p>在 Windows 8.1 UWP 设备应用程序可以执行打印机维护，如对齐打印头和清洗喷嘴。 本主题使用C#的版本<a href="https://go.microsoft.com/fwlink/p/?LinkID=299829" data-raw-source="[Print job management and printer maintenance](https://go.microsoft.com/fwlink/p/?LinkID=299829)">打印作业管理和打印机维护</a>示例，用于演示如何使用双向通信 (Bidi) 来执行此类设备的维护。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="printer-extension-library-overview.md" data-raw-source="[Printer extension library overview](printer-extension-library-overview.md)">打印机扩展库概述</a></p></td>
<td align="left"><p>本主题介绍了打印机扩展库，则可帮助设备制造商的库编写他们的打印机的 UWP 设备应用程序。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idshouldicreateawindowsstoredeviceappformyprinterspanspan-idshouldicreateawindowsstoredeviceappformyprinterspanspan-idshouldicreateawindowsstoredeviceappformyprinterspanshould-i-create-a-uwp-device-app-for-my-printer"></a><span id="Should_I_create_a_Windows_Store_device_app_for_my_printer_"></span><span id="should_i_create_a_windows_store_device_app_for_my_printer_"></span><span id="SHOULD_I_CREATE_A_WINDOWS_STORE_DEVICE_APP_FOR_MY_PRINTER_"></span>应为我的打印机创建 UWP 设备应用程序？


如果你想要为打印机使用 UWP 设备应用：

-   重点介绍高级的设备功能，如打印每页的多张照片。
-   提供了特定于设备的建议。 例如，可以使用你的设备应用来显示图像的管理选项，或提供用于设置和保存特定于打印机的默认值的方法。

## <a name="span-idgeneralrecommendationsspanspan-idgeneralrecommendationsspanspan-idgeneralrecommendationsspangeneral-recommendations"></a><span id="General_recommendations"></span><span id="general_recommendations"></span><span id="GENERAL_RECOMMENDATIONS"></span>一般建议


-   调用 window.print() 后，检查并处理来自应用的打印按钮的 onClick 事件处理程序中的错误消息。 这样，如果没有打印机不可用，终止打印请求您的应用程序。
-   如果打印失败通知用户，并且如果可能，解释失败的原因。
-   如果您计划自定义打印体验，请将此代码分离为打印辅助应用程序。 这允许您崇高目标，你的代码，可简化测试和调试进程。
-   请勿尝试自定义打印体验使用 V3 打印驱动程序。
-   不播发自定义打印 UI 中的打印设备的附件的。
-   不显示销售情况下调用 Microsoft Store 应用设备应用程序的原因不相关的项。 例如，它是相关以显示打印墨盒，购买后用户单击警报墨迹较低的通知。 但是，不适合以尝试销售打印线或照片打印工具包在此方案中相同。
-   不将用户重定向到多个产品销售额的公司的网站。
-   不显示不与设置打印首选项的任务相关的信息。 例如，不提供有关如何清洗打印头或如何对齐和测试打印喷嘴的信息。

## <a name="span-idsamplesspanspan-idsamplesspanspan-idsamplesspansamples"></a><span id="Samples"></span><span id="samples"></span><span id="SAMPLES"></span>示例


打印机的 UWP 设备应用示例演示您可以在 UWP 设备应用中实现的与打印机相关的功能。 每个示例还包括`PrinterExtensionLibrary`项目中，可以在您自己的应用程序，以便打印机扩展中重复使用。 打印机扩展插件库包装的 COM 实现[打印机扩展插件接口](https://go.microsoft.com/fwlink/p/?LinkID=299887)从 v4 打印驱动程序。

-   [打印作业管理和打印机维护](https://go.microsoft.com/fwlink/p/?LinkID=299829)示例演示如何管理打印作业，并执行打印机使用的双向通信 (Bidi) 的维护任务。

-   [打印设置和打印通知](https://go.microsoft.com/fwlink/p/?LinkID=242862)示例演示如何创建 UWP 设备应用提供的自定义浮出控件高级打印设置，可以显示打印机状态，并可以在磁贴中显示打印机通知或toast。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[开发 v4 打印驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=314231)

[打印机扩展插件接口 （v4 打印驱动程序）](https://go.microsoft.com/fwlink/p/?LinkID=299887)

[双向通信](https://go.microsoft.com/fwlink/p/?LinkId=317192)

[UWP 应用入门](getting-started.md)

[创建 UWP 设备应用程序 （分步指南）](step-1--create-a-uwp-device-app.md)

[创建设备元数据对 UWP 设备应用 （分步指南）](step-2--create-device-metadata.md)

 

 






