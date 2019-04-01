---
ms.assetid: 40D39F8E-3CD3-434B-A161-45D5BD4FBA09
title: 驱动程序包项目的 KMDF 验证程序属性
description: 设置远程计算机上的 KMDF 验证程序的属性。  使用这些设置为测试计算机生成和部署 KMDF 驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ae1c204b9819dc9039de47a8af54396894b3159
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349770"
---
# <a name="kmdf-verifier-properties-for-driver-package-projects"></a>驱动程序包项目的 KMDF 验证程序属性

设置远程计算机上的 KMDF 验证程序（或框架验证程序）的属性。 为测试计算机生成和部署 KMDF 驱动程序时，可以使用这些设置。 有关 KMDF 驱动程序的信息，请参阅[内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)。

有关框架验证程序的详细信息，请参阅[使用框架验证程序](https://msdn.microsoft.com/Library/Windows/Hardware/Ff545540)和 [WDF 验证程序控制应用程序](https://msdn.microsoft.com/Library/Windows/Hardware/Ff556129)。

## <a name="span-idsettingkmdfverifierpropertiesfordriverpackageprojectsspanspan-idsettingkmdfverifierpropertiesfordriverpackageprojectsspanspan-idsettingkmdfverifierpropertiesfordriverpackageprojectsspansetting-kmdf-verifier-properties-for-driver-package-projects"></a><span id="Setting_KMDF_Verifier_properties_for_driver_package_projects"></span><span id="setting_kmdf_verifier_properties_for_driver_package_projects"></span><span id="SETTING_KMDF_VERIFIER_PROPERTIES_FOR_DRIVER_PACKAGE_PROJECTS"></span>设置驱动程序包项目的 KMDF 验证程序属性


1.  打开驱动程序包的属性页。 在“解决方案资源管理器”中，右键单击驱动程序包项目，并选择“属性”。
2.  在驱动程序包的属性页中，依次单击“配置属性”、“驱动程序安装”和“KMDF 验证程序”。
3.  单击“启用 KMDF 验证程序”选项并选择“KMDF 验证程序始终启用”。 选择此选项时，可以为 KMDF 驱动程序配置框架验证选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Enable_KMDF_Verifier"></span><span id="enable_kmdf_verifier"></span><span id="ENABLE_KMDF_VERIFIER"></span><strong>启用 KMDF 验证程序</strong></p></td>
<td align="left"><p>启用测试计算机上的 KMDF 验证程序。 可以选择“KMDF 验证始终启用”或“KMDF 验证程序关闭”。 如果未启用 KMDF 验证程序，则当 KMDF 版本为 1.9 或更高版本时，基本框架验证将作为<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448)">驱动程序验证程序</a>的一部分启用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="KMDF_Service_Names"></span><span id="kmdf_service_names"></span><span id="KMDF_SERVICE_NAMES"></span><strong>KMDF 服务名称</strong></p></td>
<td align="left"><p>指定要监视的 KMDF 驱动程序的服务名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="IRQL_checks"></span><span id="irql_checks"></span><span id="IRQL_CHECKS"></span><strong>IRQL 检查</strong></p></td>
<td align="left"><p>启用 IRQL 检查和关键内存泄漏检查。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Forward_Compatible_Checks"></span><span id="forward_compatible_checks"></span><span id="FORWARD_COMPATIBLE_CHECKS"></span><strong>向前兼容检查</strong></p></td>
<td align="left"><p>启用在当前驱动程序版本后创建的检查。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Forward_Progress_Handler_Testing"></span><span id="forward_progress_handler_testing"></span><span id="FORWARD_PROGRESS_HANDLER_TESTING"></span><strong>向前进度处理程序检查</strong></p></td>
<td align="left"><p>指定用于测试驱动程序的向前进度处理的选项。</p>
<p><strong>无分配故障</strong>测试驱动程序的向前进度处理时，不会模拟任何故障。</p>
<p><strong>让所有分配均失败</strong>以向前进度队列为目标的所有 I/O 请求均会显示为失败，具体取决于驱动程序的向前进度处理。</p>
<p><strong>随机让分配失败</strong>随机让以向前进度队列为目标的 I/O 请求失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Track_KMDF_Object_Handles"></span><span id="track_kmdf_object_handles"></span><span id="TRACK_KMDF_OBJECT_HANDLES"></span><strong>跟踪 KMDF 对象句柄</strong></p></td>
<td align="left"><p>指定要跟踪的对象句柄类型列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_KMDF_Loader_Messages"></span><span id="enable_kmdf_loader_messages"></span><span id="ENABLE_KMDF_LOADER_MESSAGES"></span><strong>启用 KMDF 加载器消息</strong></p></td>
<td align="left"><p>通过调试程序启用 KMDF 加载器消息。 启用此功能需要重新启动目标计算机。</p>
<p>从 Windows Vista 起，操作系统默认将取消 DbgPrint 输出，这将使得 WDF 加载器诊断消息在取消被覆盖之前不可用。 KDMF 验证程序可以为你管理此功能，从而使 KMDF 加载器诊断可以在这些系统的内核调试程序中使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Verbose_logging"></span><span id="verbose_logging"></span><span id="VERBOSE_LOGGING"></span><strong>详细日志记录</strong></p></td>
<td align="left"><p>启用详细日志记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Memory_Pages_for_Logs"></span><span id="memory_pages_for_logs"></span><span id="MEMORY_PAGES_FOR_LOGS"></span><strong>日志的内存页</strong></p></td>
<td align="left"><p>指定为内核事件跟踪日志分配的非分页池页数 (1-10)。 选项包括“运行时选择”或 [<strong>1</strong>-<strong>10</strong>]。 如果选择“运行时选择”，则页数取决于 KMDF 运行时。 从 KMDF 1.9 起，如果已通过详细日志记录启用验证，则运行时使用的页数更多。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Fail_Memory_Allocations"></span><span id="fail_memory_allocations"></span><span id="FAIL_MEMORY_ALLOCATIONS"></span><strong>让内存分配失败</strong></p></td>
<td align="left"><p>指定在 KMDF 验证程序开始让所有内存分配失败之前允许的成功内存分配数量。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
* [驱动程序验证程序](https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448)
* [将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)
 

 






