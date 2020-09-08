---
ms.assetid: 79AB7242-72D6-4198-9AF0-482CBFB756C7
title: 如何使用“驱动程序测试”模板编写驱动程序测试
description: 使用适用于 Windows 8 的 Windows 驱动程序工具包 (WDK) 来创建自己的驱动程序测试或自定义所提供的部分测试。
ms.date: 03/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: b750c17de0789089e5eae9b3fd6ed4504d232342
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210827"
---
# <a name="how-to-write-a-driver-test-using-a-driver-test-template"></a>如何使用“驱动程序测试”模板编写驱动程序测试

> [!NOTE]
> 本主题介绍仅在 Visual Studio 2013 中提供的功能。 有关以前的 WDK 和 Visual Studio 版本的信息，请参阅[其他 WDK 下载](../other-wdk-downloads.md)。
> 


你可以使用适用于 Windows 8 的 Windows 驱动程序工具包 (WDK) 来创建自己的驱动程序测试或自定义所提供的部分测试。 你可以使用 WDK 为 Microsoft Visual Studio Ultimate 2012 提供的驱动程序测试框架将你创建的测试部署到远程测试计算机。

通过 WDK 提供的模板可创建采用 C++、C\# 和脚本 (JScript) 编写的、适用于 Windows 驱动程序测试项目的起始代码。 你可以选择想要包含的测试用例，也可以从空白项目开始。 你可以自定义代码，为驱动程序添加新的测试用例。 你可以使用驱动程序测试框架从 Visual Studio 部署测试。

## <a name="span-idto_customize_a_driver_test_using_the_driver_test_template_for_c__spanspan-idto_customize_a_driver_test_using_the_driver_test_template_for_c__spanspan-idto_customize_a_driver_test_using_the_driver_test_template_for_c__spanto-customize-a-driver-test-using-the-driver-test-template-for-c"></a><span id="To_customize_a_driver_test_using_the_Driver_Test_template_for_C__"></span><span id="to_customize_a_driver_test_using_the_driver_test_template_for_c__"></span><span id="TO_CUSTOMIZE_A_DRIVER_TEST_USING_THE_DRIVER_TEST_TEMPLATE_FOR_C__"></span>使用 C++ 驱动程序测试模板自定义驱动程序测试


1.  从“文件”菜单中选择“新建”&gt;“项目” 。
2.  从“新建项目”  对话框中的已安装模板列表中，选择“Visual C++”&gt;“Windows 驱动程序”&gt;“测试”  。
3.  选择“C++ Windows 驱动程序测试”  。
4.  为驱动程序测试项目提供名称和位置（或使用默认值）。
5.  从“Windows 驱动程序测试”  对话框中，选择你想要包含的测试用例或选择空（空白）驱动程序测试。 有关测试用例的详细信息，请参阅 [Windows 驱动程序测试用例](#windows_driver_test_cases)。
6.  添加所需的测试元数据。 有关详细信息，请参阅[如何添加测试元数据](to-add-test-metadata.md)。
7.  生成驱动程序测试。

## <a name="span-idto_customize_a_driver_test_using_the_driver_test_template_for_c_spanspan-idto_customize_a_driver_test_using_the_driver_test_template_for_c_spanspan-idto_customize_a_driver_test_using_the_driver_test_template_for_c_spanto-customize-a-driver-test-using-the-driver-test-template-for-c"></a><span id="To_customize_a_driver_test_using_the_Driver_Test_template_for_C_"></span><span id="to_customize_a_driver_test_using_the_driver_test_template_for_c_"></span><span id="TO_CUSTOMIZE_A_DRIVER_TEST_USING_THE_DRIVER_TEST_TEMPLATE_FOR_C_"></span>使用 C\# 驱动程序测试模板自定义驱动程序测试


1.  从“文件”菜单中选择“新建”&gt;“项目” 。
2.  从“新建项目”  对话框中的已安装模板列表中，选择“Visual C\#”&gt;“Windows 驱动程序”  。
3.  选择“C\# Windows 驱动程序测试”  。
4.  为驱动程序测试项目提供名称和位置（或使用默认值）。
5.  从“Windows 驱动程序测试”  对话框中，选择你想要包含的测试用例或选择空（空白）驱动程序测试。 有关测试用例的信息，请参阅 [Windows 驱动程序测试用例](#windows_driver_test_cases)。
6.  添加所需的测试元数据。 有关详细信息，请参阅[如何添加测试元数据](to-add-test-metadata.md)。
7.  生成驱动程序测试。

## <a name="span-idto_customize_a_driver_test_using_the_driver_test_template_for_scriptspanspan-idto_customize_a_driver_test_using_the_driver_test_template_for_scriptspanspan-idto_customize_a_driver_test_using_the_driver_test_template_for_scriptspanto-customize-a-driver-test-using-the-driver-test-template-for-script"></a><span id="To_customize_a_driver_test_using_the_Driver_Test_template_for_Script"></span><span id="to_customize_a_driver_test_using_the_driver_test_template_for_script"></span><span id="TO_CUSTOMIZE_A_DRIVER_TEST_USING_THE_DRIVER_TEST_TEMPLATE_FOR_SCRIPT"></span>使用脚本驱动程序测试模板自定义驱动程序测试


1.  从“文件”菜单中选择“新建”&gt;“项目” 。
2.  从“新建项目”  对话框中的已安装模板列表中，选择“脚本”&gt;“Windows 驱动程序”  。
3.  选择“Windows 驱动程序测试脚本”  。
4.  为驱动程序测试项目提供名称和位置（或使用默认值）。
5.  从“Windows 驱动程序测试”  对话框中，选择你想要包含的测试用例或选择空（空白）驱动程序测试。 有关测试用例的信息，请参阅 [Windows 驱动程序测试用例](#windows_driver_test_cases)。
6.  添加所需的测试元数据。 有关详细信息，请参阅[如何添加测试元数据](to-add-test-metadata.md)。
7.  生成驱动程序测试。

## <a name="span-idmaking_the_driver_tests_you_create_available_for_deployment_on_test_computersspanspan-idmaking_the_driver_tests_you_create_available_for_deployment_on_test_computersspanspan-idmaking_the_driver_tests_you_create_available_for_deployment_on_test_computersspanmaking-the-driver-tests-you-create-available-for-deployment-on-test-computers"></a><span id="Making_the_driver_tests_you_create_available_for_deployment_on_test_computers"></span><span id="making_the_driver_tests_you_create_available_for_deployment_on_test_computers"></span><span id="MAKING_THE_DRIVER_TESTS_YOU_CREATE_AVAILABLE_FOR_DEPLOYMENT_ON_TEST_COMPUTERS"></span>使你创建的驱动程序测试可部署到测试计算机上


生成驱动程序测试时，新测试将可部署到测试计算机上。 默认情况下，你创建的测试将显示在测试类别“我的测试类别”  中。 测试名称基于你选择的测试用例，其名称将类似于“我的即插即用意外删除测试”  。 每次生成测试时，测试将被覆盖。 最后生成的测试可供在测试计算机上部署和运行。

## <a name="span-idwindows_driver_test_casesspanspan-idwindows_driver_test_casesspanwindows-driver-test-cases"></a><span id="windows_driver_test_cases"></span><span id="WINDOWS_DRIVER_TEST_CASES"></span>Windows 驱动程序测试用例


WDK 提供有采用 C++、C\# 和脚本编写的、适用于 Windows 驱动程序测试项目的起始代码。 你可以选择想要包含的测试用例，也可以从空白项目开始。 并非所有测试用例都在所有语言中可用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">即插即用测试用例</th>
<th align="left">这些测试用例将强制驱动程序处理大部分与即插即用 (PnP) 相关的 IRP</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">禁用/启用</td>
<td align="left">提供用于禁用和启用 PnP 设备的测试用例代码。</td>
</tr>
<tr class="even">
<td align="left">删除</td>
<td align="left">提供用于删除 PnP 设备的测试用例代码。</td>
</tr>
<tr class="odd">
<td align="left">意外删除</td>
<td align="left">提供用于执行 PnP 设备意外删除的测试用例代码。</td>
</tr>
<tr class="even">
<td align="left">电源管理测试用例</td>
<td align="left">提供用于强制驱动程序处理系统睡眠状态的测试用例。</td>
</tr>
<tr class="odd">
<td align="left">系统睡眠状态</td>
<td align="left">提供用于在系统从睡眠状态至电源状态循环时执行设备 I/O 的测试用例代码。</td>
</tr>
<tr class="even">
<td align="left">压力和功能测试用例</td>
<td align="left">提供用于对 IOCTL 和 WMI 接口执行 I/O 压力和功能测试的测试用例。</td>
</tr>
<tr class="odd">
<td align="left">I/O 压力</td>
<td align="left">提供用于执行设备 I/O 压力的测试用例。</td>
</tr>
<tr class="even">
<td align="left">功能 IOCTL 接口</td>
<td align="left">提供为 IOCTL 接口创建功能测试用例的模板。 （仅可用于 C++）。</td>
</tr>
<tr class="odd">
<td align="left">功能 WMI 接口</td>
<td align="left">提供为 Windows 管理接口 (WMI) 创建功能测试用例的模板。 （仅可用于脚本）</td>
</tr>
<tr class="even">
<td align="left">空测试用例</td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">提供用于创建 Windows 驱动程序测试项目的空白模板。</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [测试创作和执行框架](../taef/index.md)
* [Windows 驱动程序测试框架](../wdtf/index.md)
* [如何添加测试元数据](to-add-test-metadata.md)
 

