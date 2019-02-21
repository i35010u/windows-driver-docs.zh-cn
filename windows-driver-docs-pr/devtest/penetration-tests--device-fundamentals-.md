---
title: 渗透压力测试（设备基础功能）
description: 设备的基础知识渗透测试执行各种形式的输入攻击，安全测试的重要组成部分。 攻击和渗透测试可帮助确定在软件界面中的漏洞。
ms.assetid: 53EBAF4B-2CEF-492B-98B8-DA199FDFBC46
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 032f9387f8281a8b1a94fa856bfddcd209794763
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533689"
---
# <a name="penetration-tests-device-fundamentals"></a>渗透压力测试（设备基础功能）


设备的基础知识渗透测试执行各种形式的输入攻击，安全测试的重要组成部分。 攻击和渗透测试可帮助确定在软件界面中的漏洞。

## <a name="penetration"></a>渗透


渗透测试包括两种类别的测试：模糊测试和[I/O Spy](iospy.md)并[I/O 攻击](ioattack.md)测试。 模糊测试也是一项功能**设备路径 Exceriser**测试工具。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">测试</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Disable_I_O_Spy"></span><span id="disable_i_o_spy"></span><span id="DISABLE_I_O_SPY"></span>禁用 I/O Spy</p></td>
<td align="left"><p>禁用<a href="iospy.md" data-raw-source="[I/O Spy](iospy.md)">I/O Spy</a> 1 个或多个设备上。</p>
<p><strong>测试二进制文件：</strong>Devfund_IOSpy_DisableSupport.wsc</p>
<p><strong>测试方法：</strong>DisableIoSpy</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="display_i_o_spy-enabled_device"></span>显示 I/O Spy 启用设备</p></td>
<td align="left"><p>显示拥有的设备<a href="iospy.md" data-raw-source="[I/O Spy](iospy.md)">I/O Spy</a>在其上启用。</p>
<p><strong>测试二进制文件：</strong>Devfund_IOSpy_DisplayEnabledDevices.wsc</p>
<p><strong>测试方法：</strong>DisplayIoSpyDevices</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_I_O_Spy_"></span><span id="enable_i_o_spy_"></span><span id="ENABLE_I_O_SPY_"></span>启用 I/O Spy</p></td>
<td align="left"><p>启用<a href="iospy.md" data-raw-source="[I/O Spy](iospy.md)">I/O Spy</a>一个或多个设备上。</p>
<p><strong>测试二进制文件：</strong>Devfund_IOSpy_EnableSupport.wsc</p>
<p><strong>测试方法：</strong>EnableIoSpy</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>DFD</em> -指定 IoSpy 数据文件的路径。 默认位置是 %SystemDrive%\DriverTest\IoSpy</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="fuzz_misc_api_test"></span>模糊杂项 API 测试</p></td>
<td align="left"><p>模糊杂项 API 测试是确定驱动程序是否可以处理各种从内核模式驱动程序的常用调用的测试。</p>
<p>测试包括以下测试：</p>
<ul>
<li><p>调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567072" data-raw-source="[&lt;strong&gt;ZwReadFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567072)"> <strong>ZwReadFile</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff567121" data-raw-source="[&lt;strong&gt;ZwWriteFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567121)"> <strong>ZwWriteFile</strong></a>、 指定有效的数据缓冲区的指针、 不同的长度 （包括零） 和不同的字节偏移量，包括零，-1 和 64 位字节偏移量。</p></li>
<li><p>用来取消我调用 / 0 并刷新缓冲区。</p></li>
<li><p>目录查询的一系列调用使用有效的用户数据缓冲区的指针使用常见的文件信息类和不同的缓冲区长度 （包括零）。</p></li>
<li><p>目录查询调用类似于颁发的管理的虚拟 DOS 机 (VDM) 下运行的程序。</p></li>
<li><p>调用以检索具有不同的缓冲区大小和长度的文件的扩展的属性。</p></li>
<li><p>调用以创建并关闭部分对象，使用不同的部分页保护和组合的分配属性 （已提交的部分，图像文件部分）。</p></li>
<li><p>调用以锁定和解锁文件。</p></li>
<li><p>调用以检索了卷的配额项。</p></li>
<li><p>文件属性测试，带有有效指针指向的文件属性查询的一系列<strong>ObjectAttributes</strong>结构。</p>
<p>文件特性测试具有可选的长度为零的测试。 检索的扩展的属性的文件，时模糊测试到驱动程序传递空 （长度为零） 查询和无效的缓冲区地址。</p></li>
</ul>
<p><strong>测试二进制文件：</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong>DoMiscAPITest</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Misc_API_with_zero-length_query_test"></span><span id="fuzz_misc_api_with_zero-length_query_test"></span><span id="FUZZ_MISC_API_WITH_ZERO-LENGTH_QUERY_TEST"></span>使用长度为零的查询测试模糊杂项 API</p></td>
<td align="left"><p>此测试执行为模糊杂项 API 测试相同的测试并这一次会尝试检索的扩展的属性的文件时到驱动程序中将保留为空 （长度为零） 查询和无效的缓冲区地址。</p>
<p><strong>测试二进制文件：</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong>DoMiscAPIWithZeroLengthTest</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="fuzz_open_and_close_test"></span>模糊打开和关闭测试</p></td>
<td align="left"><p>此测试可执行数千个创建的打开-关闭序列。</p>
<p>有关此测试的详细信息，请参阅<a href="#about-the-fuzz-open-and-close-test" data-raw-source="[About the Fuzz open and close test](#about-the-fuzz-open-and-close-test)">模糊有关打开和关闭测试</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong>DoOpenCloseTest</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Query_and_Set_File_Information_test_"></span><span id="fuzz_query_and_set_file_information_test_"></span><span id="FUZZ_QUERY_AND_SET_FILE_INFORMATION_TEST_"></span>模糊查询和设置文件信息的测试</p></td>
<td align="left"><p>此测试会发出调用以检索和更改设备的对象、 文件和卷信息。</p>
<p>期间<em>查询和设置文件的信息测试</em>，打开模糊测试问题调用以检索和更改设备的对象、 文件和卷信息<a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">基本打开操作</a>和其他开放操作，包括模糊子打开测试执行的操作。</p>
<p>模糊测试问题每个查询或使用有效的缓冲区和缓冲区长度和文件信息类的各种设置调用至少 1024年的时间。 每种类型的一个请求也会发送的缓冲区无效指针和缓冲区长度为零。</p>
<p>如果您使用<em>ChangeBufferProtectionFlags</em>参数，它指向的缓冲区上设置保护选项，模糊测试各不相同的安全设置每个查询和设置调用。</p>
<p>该测试还执行模糊子打开测试。</p>
<p>此测试使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff567052" data-raw-source="[&lt;strong&gt;ZwQueryInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567052)"> <strong>ZwQueryInformationFile</strong></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff567096" data-raw-source="[&lt;strong&gt;ZwSetInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567096)"> <strong>ZwSetInformationFile</strong></a>， <a href="https://msdn.microsoft.com/library/windows/hardware/ff567070" data-raw-source="[&lt;strong&gt;ZwQueryVolumeInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567070)"> <strong>ZwQueryVolumeInformationFile</strong></a>，并<a href="https://msdn.microsoft.com/library/windows/hardware/ff567112" data-raw-source="[&lt;strong&gt;ZwSetVolumeInformationFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567112)"> <strong>ZwSetVolumeInformationFile</strong> </a>函数。</p>
<p><strong>测试二进制文件：</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong>DoQueryAndSetFileInformationTest</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Fuzz_Query_and_Set_Security_test"></span><span id="fuzz_query_and_set_security_test"></span><span id="FUZZ_QUERY_AND_SET_SECURITY_TEST"></span>模糊查询和设置安全测试</p></td>
<td align="left"><p>此测试会发出调用以检索的安全描述符和更改设备的安全状态。</p>
<p>期间<em>查询和设置安全测试</em>，模糊测试发出调用以检索的安全描述符和更改的安全状态的设备打开<a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">基本打开操作</a>和其他开放操作，包括模糊子打开测试执行的操作。</p>
<p>模糊测试问题每个查询或使用有效的缓冲区和各种缓冲区长度和安全信息类型 （OWNER_SECURITY_INFORMATION、 GROUP_SECURITY_INFORMATION、 DACL_SECURITY_INFORMATION、 SACL_SECURITY_ 设置调用至少 1024年时间信息和没有信息类型）。 每种类型的一个请求也会发送的缓冲区无效指针和缓冲区长度为零。</p>
<p>如果您使用<em>ChangeBufferProtectionFlags</em>参数，它指向的缓冲区上设置保护选项，模糊测试各不相同的安全设置每个查询和设置调用。</p>
<p><strong>测试二进制文件：</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong>DoQueryAndSetSecurityTest</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Random_FSCTL_test___Fuzz_Random_IOCTL_test_"></span><span id="fuzz_random_fsctl_test___fuzz_random_ioctl_test_"></span><span id="FUZZ_RANDOM_FSCTL_TEST___FUZZ_RANDOM_IOCTL_TEST_"></span>模糊随机 FSCTL 测试 / 模糊随机 IOCTL 测试</p></td>
<td align="left"><p>此测试函数代码、 设备类型、 数据传输方法，与指定的值范围从随机选择的访问要求发出一系列对 DeviceIoControl 函数的调用。 调用包含输入和输出缓冲区，使用有效和无效缓冲指针和长度，并随机生成的内容。</p>
<p>在随机测试时，模糊测试发出调用一系列<strong>DeviceIoControl</strong>函数和函数代码、 设备类型、 数据传输方法，并从指定范围的随机选择的访问要求值。 调用包含输入和输出缓冲区，使用有效和无效缓冲指针和长度，并随机生成的内容。</p>
<p>模糊测试执行期间打开的所有设备上的随机测试<a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">打开的基本操作</a>和其他打开的测试。 可以使用以下参数来自定义此测试：</p>
<ul>
<li><p>使用<em>MinFunctionCode</em>并<em>MaxFunctionCode</em>指定范围的 IOCTL 或 FSCTL 函数调用中使用的代码</p></li>
<li><p>使用<em>MinDeviceType</em>并<em>MaxDeviceType</em>来指定在调用中使用的设备类型的范围</p></li>
<li><p>使用<em>SeedNumber</em>指定种子数字随机数生成例程。</p></li>
</ul>
<p>模糊测试用于测试使用生成随机数的函数<em>设定种子数</em>、 起始编号的随机数字生成算法。 若要重现的测试条件，请使用<em>设定种子数</em>原始测试试用版中使用参数来指定种子数字。</p>
<p>一个<em>定制随机测试</em>包含随机测试。 定制的随机测试使用随机测试的结果来检查对 IOCTL 或 FSCTL 请求更多详细信息中的驱动程序响应。 定制的随机测试探测随机测试错过的区域和那些在其上驱动程序未响应按预期方式根据随机测试调用返回的状态。</p>
<p><strong>测试二进制文件：</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong>DoRandomIOCTLTest DoRandomFSCTLTest</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>MinInBuffer</em></p>
<p><em>MaxInBuffer</em></p>
<p><em>MinOutBuffer</em></p>
<p><em>MaxOutBuffer</em></p>
<p><em>MaxRandomCalls</em></p>
<p><em>MaxTailoredCalls</em></p>
<p><em>SeedNumber</em></p>
<p><em>MinDeviceType</em></p>
<p><em>MaxDeviceType</em></p>
<p><em>MinFunctionCode</em></p>
<p><em>MaxFunctionCode</em></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="fuzz_sub-opens_test"></span>模糊子打开测试</p></td>
<td align="left"><p>该测试可执行一系列快速调用，以在设备中打开对象的&#39;s 命名空间。 在这些调用，它将传递与设备开始且包含任意名称和不同长度和内容的无意义字符串的路径。</p>
<p>期间<em>打开测试相对</em>，(也称为<em>子打开测试</em>) 模糊测试尝试在设备中打开对象&#39;s<a href="https://msdn.microsoft.com/library/windows/hardware/ff542068" data-raw-source="[namespace](https://msdn.microsoft.com/library/windows/hardware/ff542068)">命名空间</a>。</p>
<p>在此测试期间模糊测试执行一系列快速的调用，以便在使用打开的设备的命名空间中打开对象<a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">打开的基本操作</a>和其他打开的操作。 在这些调用，模糊测试传递与设备开始且包含任意名称和不同长度和内容的无意义字符串的路径。</p>
<p>此测试确定驱动程序或文件系统中管理其命名空间中的打开请求的方式。 具体而言，如果该驱动程序不支持在其命名空间中的开放请求，它必须防止未经授权的访问，失败的请求，或使用时设置 FILE_DEVICE_SECURE_OPEN 设备特征<a href="https://msdn.microsoft.com/library/windows/hardware/ff548397" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548397)"> <strong>IoCreateDevice</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff548407" data-raw-source="[&lt;strong&gt;IoCreateDeviceSecure&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548407)"> <strong>IoCreateDeviceSecure</strong> </a>创建设备对象。</p>
<p>有关命名空间的设备的详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff542068" data-raw-source="[Controlling Device Namespace Access](https://msdn.microsoft.com/library/windows/hardware/ff542068)">控制设备 Namespace 访问</a>。</p>
<p><strong>测试二进制文件：</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong>DoSubOpensTest</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Sub-opens_with_Streams_test"></span><span id="fuzz_sub-opens_with_streams_test"></span><span id="FUZZ_SUB-OPENS_WITH_STREAMS_TEST"></span>模糊子随即打开，并且流测试</p></td>
<td align="left"><p>此测试尝试打开各种设备上的命名的数据流。 测试使用与内容和可能会对某些设备上的其他使用有效的字符系列的任意流名称。</p>
<p>期间<em>流测试</em>，模糊测试尝试打开各种设备上的命名的数据流。 测试使用与内容和可能会对某些设备上的其他使用有效的字符系列的任意流名称。 此测试确定是否尤其是是否该驱动程序将导出的设备不支持或预测的数据流量，该驱动程序能够正确处理数据流请求。</p>
<p>一个<em>名为数据流</em>是文件对象的属性。 通过编写文件、 一个冒号和数据流，例如，名称的名称指定的命名的数据流&quot;File01.txt:AccessDate&quot;其中<em>AccessDate</em>是命名的数据流，也就是说，属性File01.txt 文件中。</p>
<p>模糊测试记录在测试中使用流名称。</p>
<p><strong>测试二进制文件：</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong>DoSubOpensWithStreamsTest</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Fuzz_Zero-Length_Buffer_FSCTL_test___Fuzz_Zero-Length_Buffer_IOCTL_test"></span><span id="fuzz_zero-length_buffer_fsctl_test___fuzz_zero-length_buffer_ioctl_test"></span><span id="FUZZ_ZERO-LENGTH_BUFFER_FSCTL_TEST___FUZZ_ZERO-LENGTH_BUFFER_IOCTL_TEST"></span>模糊长度为零的缓冲区 FSCTL 测试 / 模糊长度为零的缓冲区 IOCTL 测试</p></td>
<td align="left"><p>此测试发出调用一系列<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl function&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl 函数</strong></a>输入和/或输出缓冲区长度为 0。 测试通过使用不同的函数代码、 设备类型、 数据传输方法和访问要求生成不同的文件系统控制代码。</p>
<p>测试长度为零的缓冲区，请在模糊测试发出调用一系列<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl function&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl 函数</strong></a>输入和/或输出缓冲区长度为 0。 测试通过使用不同的函数代码、 设备类型、 数据传输方法和访问要求生成不同的 I/O 控制代码。 有关内容的 I/O 控制代码的信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff543023" data-raw-source="[Defining I/O Control Codes](https://msdn.microsoft.com/library/windows/hardware/ff543023)">定义的 I/O 控制代码</a>。</p>
<p>若要测试该驱动程序&#39;的缓冲区无效指针，这些用户模式下调用中的缓冲区指针的 s 处理内核虚拟地址空间，如 0xFFFFFC00 指定地址高)。</p>
<p>模糊测试打开在基本和其他打开测试过程中的所有设备上执行的缓冲区长度为零的测试。 你可以使用自定义此测试<em>MinFunctionCode</em>并<em>MaxFunctionCode</em>参数指定的范围的 IOCTL 或 FSCTL 函数调用中使用的代码的命令和<em>MinDeviceType</em>并<em>MaxDeviceType</em>来指定在调用中使用的设备类型的范围。</p>
<p><strong>测试二进制文件：</strong>Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong>DoZeroLengthBufferIOCTLTest DoZeroLengthBufferFSCTLTest</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>MinDeviceType</em></p>
<p><em>MaxDeviceType</em></p>
<p><em>MinFunctionCode</em></p>
<p><em>MaxFunctionCode</em></p>
<p><em>DoPoolCheck</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Run_I_O_Attack"></span><span id="run_i_o_attack"></span><span id="RUN_I_O_ATTACK"></span>运行 I/O 攻击</p></td>
<td align="left"><p>运行<a href="ioattack.md" data-raw-source="[I/O Attack](ioattack.md)">I/O 攻击</a>指定的设备或设备上。</p>
<p><strong>测试二进制文件：</strong>Devfund_IOAttack_DeleteDataFile.wsc</p>
<p><strong>测试方法：</strong>RunIoAttack</p>
<p><strong>参数：</strong> -请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests" data-raw-source="[Device Fundamentals Test Parameters](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)">设备基础测试参数</a></p>
<p><em>DQ</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="about-the-fuzz-open-and-close-test"></a>有关模糊打开和关闭测试


模糊打开和关闭测试采用多种不同的方式打开和关闭指定的设备或设备的实例：[基本操作，打开](#basic-open-operations)，[直接设备打开操作](#direct-device-open-operations)，和一个[打开和关闭测试](#open-and-close-test)。

### <a name="basic-open-operations"></a>打开的基本操作

期间*打开的基本操作*，模糊重复测试打开 （创建） 指定的设备或设备的实例由指定的驱动程序导出使用不同的方法和选项。

模糊测试始终执行基本的打开操作。 不需要选择它们并不能在测试会话中排除。

模糊测试通过调用系统服务在用户模式下执行所有打开的操作 ([ZwXxx 例程](https://msdn.microsoft.com/library/windows/hardware/ff567122)) 是适用于设备。 如果打开调用返回到设备的句柄，模糊测试使用句柄来执行其他设备测试选择测试会话。

有五种类型的打开的基本操作：

-   **打开标准。** 模糊测试以异步方式打开设备，并指定只有本机设备名称。

-   **打开方式添加反斜杠。** 模糊测试发出打开调用的设备名称后, 跟反斜杠 (\)，如\\设备\\cdrom\\，就像调用是一样，若要打开设备的根目录。

    此操作将确定驱动程序或文件系统中管理其命名空间中的打开请求的方式。 具体而言，如果设备不支持在其命名空间中的开放请求，该驱动程序必须防止未经授权的访问，通过失败的请求，或设置文件\_设备\_SECURE\_打开设备调用时的特征[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)或[ **IoCreateDeviceSecure** ](https://msdn.microsoft.com/library/windows/hardware/ff548407)创建设备对象。

-   **打开为命名管道。** 模糊测试打开设备并建立到设备的命名的管道。 访问参数 (ShareAccess) 最初设置为读取和写入，但如果请求失败调整。 如果设备不支持命名的管道，它应会使请求失败。

-   **打开为邮件槽。** 模糊测试作为邮件槽打开该设备。 如果设备不支持此类型的连接，它应会使请求失败。

-   **打开为树的连接。** 模糊测试作为树连接用于远程网络访问权限打开设备。 访问参数 (ShareAccess) 最初设置为读取和写入，但如果请求失败调整。 如果设备不支持此类型的连接，它应会使请求失败。

打开调用中使用的参数更改以适应设备特征，并使其可能的调用会成功。 例如，如果基本打开操作失败，因为该调用不符合设备的安全要求，模糊测试针对较小的访问权限重复打开操作的请求。 例如，如果请求写访问权限打开操作返回安全冲突错误，请打开重复带有请求的读取访问权限。

### <a name="direct-device-open-operations"></a>直接设备打开操作

期间*直接设备打开操作*，模糊测试文件系统中直接为设备，而不是一个文件打开设备。 直接设备打开操作始终是同步的。 如果调用成功，模糊测试将使用提供执行其他所选的测试的句柄。

### <a name="open-and-close-test"></a>打开和关闭测试

期间*打开和关闭测试*，模糊测试创建多个线程，其中每个执行数千个创建的打开-关闭序列。 这会测试处理否则为简单和预期调用特别卷驱动程序的能力。

打开和关闭测试使用相同的选项中使用[打开的基本操作](#basic-open-operations)和打开方式添加反斜杠测试，并且只需在这些测试之前执行。

## <a name="related-topics"></a>相关主题


[如何测试在运行时使用 Visual Studio 的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)

[如何选择和配置设备基础测试](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[设备基础测试](device-fundamentals-tests.md)

[设备基础测试参数](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)

[提供 WDTF 简单 I/O 插件](https://msdn.microsoft.com/library/windows/hardware/hh781398)

[如何测试在运行时从命令提示符下的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/how_to_test_a_driver_at_runtime_from_a_command_prompt)

 

 






