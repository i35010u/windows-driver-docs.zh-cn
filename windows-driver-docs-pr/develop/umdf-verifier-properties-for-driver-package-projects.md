---
ms.assetid: 5BF7AB90-FF2E-4679-8C84-2E8091917F5D
title: 驱动程序包项目的 UMDF 验证程序属性
description: 设置测试计算机上的 UMDF 验证程序的属性。 为测试计算机生成和部署驱动程序时，可以使用这些设置。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a35afe6236b5018df0cf51f4384d9d81cf8fc6c
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "67364203"
---
# <a name="umdf-verifier-properties-for-driver-package-projects"></a>驱动程序包项目的 UMDF 验证程序属性

设置测试计算机上的 UMDF 验证程序的属性。 为测试计算机生成和部署驱动程序时，可以使用这些设置。

有关部署的信息，请参阅[预配计算机以便进行驱动程序部署和测试 (WDK 8.1)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1) 和[将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)

有关调试 UMDF 驱动程序的信息，请参阅[如何启用 UMDF 驱动程序的调试](https://docs.microsoft.com/windows-hardware/drivers/wdf/enabling-a-debugger)和 [WDF 验证程序控制器应用程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdf-verifier-control-application)。

## <a name="span-idsetting_umdf_verifier_properties_for_driver_projectsspanspan-idsetting_umdf_verifier_properties_for_driver_projectsspanspan-idsetting_umdf_verifier_properties_for_driver_projectsspansetting-umdf-verifier-properties-for-driver-projects"></a><span id="Setting_UMDF_Verifier_properties_for_driver_projects"></span><span id="setting_umdf_verifier_properties_for_driver_projects"></span><span id="SETTING_UMDF_VERIFIER_PROPERTIES_FOR_DRIVER_PROJECTS"></span>设置驱动程序项目的 UMDF 验证程序属性


1.  打开驱动程序包的属性页。 在“解决方案资源管理器”中，右键单击驱动程序包项目，并选择“属性”  。
2.  在驱动程序包的属性页中，依次单击“配置属性”  、“驱动程序安装”  和“UMDF 验证程序”  。
3.  选择“部署 UMDF 验证程序”  选项。 启用了此选项时（**是**），可以选择用来在测试计算机上验证 UMDF 驱动程序的 UMDF 验证程序选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_Deploy_UMDF_Verifier"></span><span id="_deploy_umdf_verifier"></span><span id="_DEPLOY_UMDF_VERIFIER"></span><strong>部署 UMDF 验证程序</strong></p></td>
<td align="left"><p>启用测试计算机上的 UMDF 验证程序设置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="UMDF_Service_Names"></span><span id="umdf_service_names"></span><span id="UMDF_SERVICE_NAMES"></span><strong>UMDF 服务名称</strong></p></td>
<td align="left"><p>指定要监视的 UMDF 驱动程序的服务名称。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_Object_Tracking"></span><span id="enable_object_tracking"></span><span id="ENABLE_OBJECT_TRACKING"></span><strong>启用对象跟踪</strong></p></td>
<td align="left"><p>跟踪所有已创建的 UMDF 对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Enable_Reference_Count_Tracking"></span><span id="enable_reference_count_tracking"></span><span id="ENABLE_REFERENCE_COUNT_TRACKING"></span><strong>启用引用计数跟踪</strong></p></td>
<td align="left"><p>跟踪所有 UMDF 对象引用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Maximum_Restart_Attempts"></span><span id="maximum_restart_attempts"></span><span id="MAXIMUM_RESTART_ATTEMPTS"></span><strong>尝试重启的最大次数</strong></p></td>
<td align="left"><p>UMDF 将重启失败的主机进程的最大次数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="UMDF_Logging_level"></span><span id="umdf_logging_level"></span><span id="UMDF_LOGGING_LEVEL"></span><strong>UMDF 日志记录级别</strong></p></td>
<td align="left"><p>指定 UMDF 验证程序为其托管的驱动程序记录的信息量。</p>
<p><strong>仅关键错误和严重错误</strong> - 仅记录关键错误和严重错误。</p>
<p><strong>所有错误</strong> - 记录所有错误。</p>
<p><strong>警告和所有错误</strong> - 记录警告和所有错误。</p>
<p><strong>信息事件、警告和所有错误</strong> - 记录信息事件、警告和所有错误。</p>
<p><strong>详细输出（任何种类的所有事件）</strong> - 记录所有事件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Log_to_Kernel_Debugger"></span><span id="log_to_kernel_debugger"></span><span id="LOG_TO_KERNEL_DEBUGGER"></span><strong>记录到内核调试程序</strong></p></td>
<td align="left"><p>将验证程序输出记录到内核调试程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Break_into_Kernel_Debugger"></span><span id="break_into_kernel_debugger"></span><span id="BREAK_INTO_KERNEL_DEBUGGER"></span><strong>强行进入内核调试程序</strong></p></td>
<td align="left"><p>UMDF 主机进程失败时强行进入内核调试程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Attach_to_Kernel_Debugger"></span><span id="attach_to_kernel_debugger"></span><span id="ATTACH_TO_KERNEL_DEBUGGER"></span><strong>附加到内核调试程序</strong></p></td>
<td align="left"><p>如果未附加用户模式调试程序，则附加到内核调试程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Timeout_on_Driver_Load__sec_"></span><span id="timeout_on_driver_load__sec_"></span><span id="TIMEOUT_ON_DRIVER_LOAD__SEC_"></span><strong>驱动程序加载超时(秒)</strong></p></td>
<td align="left"><p>指定驱动程序加载后附加调试程序之前要等待的时间（以秒为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Timeout_on_Driver_Start__sec_"></span><span id="timeout_on_driver_start__sec_"></span><span id="TIMEOUT_ON_DRIVER_START__SEC_"></span><strong>驱动程序启动超时(秒)</strong></p></td>
<td align="left"><p>指定驱动程序启动后附加调试程序之前要等待的时间（以秒为单位）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Verify_at_Current_Level"></span><span id="verify_at_current_level"></span><span id="VERIFY_AT_CURRENT_LEVEL"></span><strong>在当前级别验证</strong></p></td>
<td align="left"><p>根据当前的框架版本规则验证使用早期框架版本生成的驱动程序。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
* [驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)
* [将驱动程序部署到测试计算机](deploying-a-driver-to-a-test-computer.md)
 

 






