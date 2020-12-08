---
title: 渗透压力测试（设备基础功能）
description: 设备基础的渗透测试执行各种形式的输入攻击，这是安全测试的关键组成部分。 攻击和渗透测试可帮助识别软件接口中的漏洞。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bd64f5cb2d59374c4383fe5c8ea4e9c54fcfdc7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820373"
---
# <a name="penetration-tests-device-fundamentals"></a>渗透压力测试（设备基础功能）


设备基础的渗透测试执行各种形式的输入攻击，这是安全测试的关键组成部分。 攻击和渗透测试可帮助识别软件接口中的漏洞。

## <a name="penetration"></a>性


渗透测试包括两个测试类别：模糊测试和 [I/o 监视](iospy.md) 和 i/o [攻击](ioattack.md) 测试。 模糊测试也是 **设备路径 Exceriser** 测试工具的一项功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">测试</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Disable_I_O_Spy"></span><span id="disable_i_o_spy"></span><span id="DISABLE_I_O_SPY"></span>禁用 i/o Spy</p></td>
<td align="left"><p>禁用1个或多个设备上的 <a href="iospy.md" data-raw-source="[I/O Spy](iospy.md)">I/o 监视</a> 。</p>
<p><strong>测试二进制文件：</strong> Devfund_IOSpy_DisableSupport. wsc</p>
<p><strong>测试方法：</strong> DisableIoSpy</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="display_i_o_spy-enabled_device"></span>显示启用了监视的 i/o 设备</p></td>
<td align="left"><p>显示在其上启用了 <a href="iospy.md" data-raw-source="[I/O Spy](iospy.md)">I/o 监视</a> 程序的设备。</p>
<p><strong>测试二进制文件：</strong> Devfund_IOSpy_DisplayEnabledDevices. wsc</p>
<p><strong>测试方法：</strong> DisplayIoSpyDevices</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_I_O_Spy_"></span><span id="enable_i_o_spy_"></span><span id="ENABLE_I_O_SPY_"></span>启用 i/o Spy</p></td>
<td align="left"><p>启用一个或多个设备上的 <a href="iospy.md" data-raw-source="[I/O Spy](iospy.md)">I/o 监视</a> 。</p>
<p><strong>测试二进制文件：</strong> Devfund_IOSpy_EnableSupport. wsc</p>
<p><strong>测试方法：</strong> EnableIoSpy</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p>
<p><em>DFD</em> - 指定 IoSpy 数据文件的路径。 默认位置为%SystemDrive%\DriverTest\IoSpy</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="fuzz_misc_api_test"></span>模糊杂项 API 测试</p></td>
<td align="left"><p>模糊杂项 API 测试是确定驱动程序是否可以处理来自内核模式驱动程序的各种常见调用的测试。</p>
<p>这些测试包括以下测试：</p>
<ul>
<li><p>调用 <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile" data-raw-source="[&lt;strong&gt;ZwReadFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)"><strong>ZwReadFile</strong></a> 和 <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile" data-raw-source="[&lt;strong&gt;ZwWriteFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile)"><strong>ZwWriteFile</strong></a>，指定有效的数据缓冲区指针、不同的长度 (包括零) 和不同的字节偏移量，包括零、-1 和64位字节偏移量。</p></li>
<li><p>调用以取消 I/0 并刷新缓冲区。</p></li>
<li><p>一系列目录查询调用，其中使用带有有效用户数据缓冲区指针和不同缓冲区长度的常见文件信息类 (包括零) 。</p></li>
<li><p>目录查询调用与在虚拟 DOS 计算机 (控制的程序发出的调用) 。</p></li>
<li><p>调用检索具有不同缓冲区大小和长度的文件的扩展属性。</p></li>
<li><p>调用以创建和关闭节对象，并具有不同的章节页面保护和章节分配属性 (提交的分区、图像文件部分) 。</p></li>
<li><p>用于锁定和解锁文件的调用。</p></li>
<li><p>调用检索卷的配额条目。</p></li>
<li><p>文件属性测试，一系列具有指向 <strong>ObjectAttributes</strong> 结构的有效指针的文件属性查询。</p>
<p>文件属性测试有可选的零长度测试。 检索文件的扩展属性时，模糊测试向驱动程序传递一个空白 (零长度) 查询和一个无效的缓冲区地址。</p></li>
</ul>
<p><strong>测试二进制文件：</strong> Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong> DoMiscAPITest</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Misc_API_with_zero-length_query_test"></span><span id="fuzz_misc_api_with_zero-length_query_test"></span><span id="FUZZ_MISC_API_WITH_ZERO-LENGTH_QUERY_TEST"></span>模糊含零长度查询测试的杂项 API</p></td>
<td align="left"><p>此测试执行与模糊杂项 API 测试相同的测试，并在尝试检索文件的扩展属性时，将空白 (零长度) 查询和无效缓冲区地址传递给驱动程序。</p>
<p><strong>测试二进制文件：</strong> Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong> DoMiscAPIWithZeroLengthTest</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="fuzz_open_and_close_test"></span>模糊打开并关闭测试</p></td>
<td align="left"><p>此测试执行数千个开即用的序列。</p>
<p>有关此测试的详细信息，请参阅 <a href="#about-the-fuzz-open-and-close-test" data-raw-source="[About the Fuzz open and close test](#about-the-fuzz-open-and-close-test)">关于模糊打开并关闭测试</a>。</p>
<p><strong>测试二进制文件：</strong> Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong> DoOpenCloseTest</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Query_and_Set_File_Information_test_"></span><span id="fuzz_query_and_set_file_information_test_"></span><span id="FUZZ_QUERY_AND_SET_FILE_INFORMATION_TEST_"></span>模糊查询和设置文件信息测试</p></td>
<td align="left"><p>此测试会发出调用来检索和更改设备的对象、文件和卷信息。</p>
<p>在 <em>查询和设置文件信息测试</em>过程中，模糊测试问题会调用以检索和更改由 <a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">基本打开操作</a> 和其他打开的操作打开的设备的对象、文件和卷信息，包括由模糊子测试执行的操作。</p>
<p>模糊测试将使用有效的缓冲区和各种缓冲区长度和文件信息类发出每个查询或设置至少1024次调用。 每种类型的一个请求也会随无效的缓冲区指针和零缓冲区长度一起发送。</p>
<p>如果使用 <em>ChangeBufferProtectionFlags</em> 参数（用于设置保护选项），则模糊测试会改变每个查询中的缓冲区的安全设置，并设置调用。</p>
<p>此测试还会执行模糊的子打开测试。</p>
<p>此测试使用 <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile" data-raw-source="[&lt;strong&gt;ZwQueryInformationFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)"><strong>ZwQueryInformationFile</strong></a>、 <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile" data-raw-source="[&lt;strong&gt;ZwSetInformationFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)"><strong>ZwSetInformationFile</strong></a>、 <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwqueryvolumeinformationfile" data-raw-source="[&lt;strong&gt;ZwQueryVolumeInformationFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwqueryvolumeinformationfile)"><strong>ZwQueryVolumeInformationFile</strong></a>和 <a href="/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwsetvolumeinformationfile" data-raw-source="[&lt;strong&gt;ZwSetVolumeInformationFile&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwsetvolumeinformationfile)"><strong>ZwSetVolumeInformationFile</strong></a> 函数。</p>
<p><strong>测试二进制文件：</strong> Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong> DoQueryAndSetFileInformationTest</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Fuzz_Query_and_Set_Security_test"></span><span id="fuzz_query_and_set_security_test"></span><span id="FUZZ_QUERY_AND_SET_SECURITY_TEST"></span>模糊查询和设置安全测试</p></td>
<td align="left"><p>此测试将调用以检索安全描述符，并更改设备的安全状态。</p>
<p>在 <em>查询和设置安全测试</em>过程中，模糊测试问题会调用以检索安全描述符，并更改由 <a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">基本打开操作</a> 和其他打开的操作打开的设备的安全状态，包括模糊子测试执行的操作。</p>
<p>模糊测试将发出每个查询或设置调用至少1024次，并使用有效缓冲区和各种缓冲长度和安全信息类型 (OWNER_SECURITY_INFORMATION、GROUP_SECURITY_INFORMATION、DACL_SECURITY_INFORMATION、SACL_SECURITY_INFORMATION 和无) 的信息类型。 每种类型的一个请求也会随无效的缓冲区指针和零缓冲区长度一起发送。</p>
<p>如果使用 <em>ChangeBufferProtectionFlags</em> 参数（用于设置保护选项），则模糊测试会改变每个查询中的缓冲区的安全设置，并设置调用。</p>
<p><strong>测试二进制文件：</strong> Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong> DoQueryAndSetSecurityTest</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Random_FSCTL_test___Fuzz_Random_IOCTL_test_"></span><span id="fuzz_random_fsctl_test___fuzz_random_ioctl_test_"></span><span id="FUZZ_RANDOM_FSCTL_TEST___FUZZ_RANDOM_IOCTL_TEST_"></span>模糊随机 FSCTL 测试/模糊随机 IOCTL 测试</p></td>
<td align="left"><p>此测试向 DeviceIoControl 函数发出一系列调用，其中包含从指定值范围随机选择的函数代码、设备类型、数据传输方法和访问要求。 调用包括具有有效和无效的缓冲区指针和长度的输入和输出缓冲区，以及随机生成的内容。</p>
<p>在随机测试期间，模糊测试会向 <strong>DeviceIoControl</strong> 函数发出一系列调用，其中包含从指定值范围随机选择的函数代码、设备类型、数据传输方法和访问要求。 调用包括具有有效和无效的缓冲区指针和长度的输入和输出缓冲区，以及随机生成的内容。</p>
<p>模糊测试对在 <a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">基本打开操作</a> 和其他打开的测试过程中打开的所有设备执行随机测试。 您可以使用以下参数自定义此测试：</p>
<ul>
<li><p>使用 <em>MinFunctionCode</em> 和 <em>MaxFunctionCode</em> 指定调用中使用的 IOCTL 或 FSCTL 函数代码的范围</p></li>
<li><p>使用 <em>MinDeviceType</em> 和 <em>MaxDeviceType</em> 指定在调用中使用的设备类型的范围</p></li>
<li><p>使用 <em>SeedNumber</em> 为生成例程的随机数指定种子数字。</p></li>
</ul>
<p>模糊测试用于为测试生成随机数的函数使用 <em>种子数字</em>，即随机数生成算法的起始编号。 若要重现测试条件，请使用 <em>seed number</em> 参数指定在原始测试试验中使用的种子数字。</p>
<p><em>定制的随机测试</em>包含为随机测试的一部分。 定制的随机测试使用随机测试的结果来更详细地检查对 IOCTL 或 FSCTL 请求的驱动程序响应。 定制的随机测试会探测随机测试丢失的区域，并根据随机测试调用返回的状态，驱动程序未按预期方式响应。</p>
<p><strong>测试二进制文件：</strong> Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong> DoRandomIOCTLTest, DoRandomFSCTLTest</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
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
<td align="left"><p><span id="fuzz_sub-opens_test"></span>模糊子测试</p></td>
<td align="left"><p>该测试执行一系列快速调用，以打开设备命名空间中的对象。 在这些调用中，它将传递一个以设备开头的路径，并包含不同长度和内容的任意名称和有意义的字符串。</p>
<p>在 <em>相对打开的测试</em>过程中， (也称为 " <em>子打开测试</em> ") 模糊测试尝试打开设备 <a href="/windows-hardware/drivers/kernel/controlling-device-namespace-access" data-raw-source="[namespace](../kernel/controlling-device-namespace-access.md)">命名空间</a>中的对象。</p>
<p>在此测试期间，模糊测试将执行一系列快速调用，以打开通过使用 <a href="#basic-open-operations" data-raw-source="[Basic Open Operations](#basic-open-operations)">基本打开操作</a> 和其他打开的操作打开的设备的命名空间中的对象。 在这些调用中，模糊测试传递一个路径，该路径以设备开头，并包含不同长度和内容的任意名称和有意义的字符串。</p>
<p>此测试确定驱动程序或文件系统如何在其命名空间中管理打开的请求。 具体而言，如果驱动程序不支持在其命名空间中打开请求，则该驱动程序必须通过失败请求来阻止未经授权的访问，或者在使用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice" data-raw-source="[&lt;strong&gt;IoCreateDevice&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)"><strong>IoCreateDevice</strong></a> 或 <a href="/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure" data-raw-source="[&lt;strong&gt;IoCreateDeviceSecure&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)"><strong>IoCreateDeviceSecure</strong></a> 创建设备对象时设置 FILE_DEVICE_SECURE_OPEN 设备特性。</p>
<p>有关设备命名空间的详细信息，请参阅 <a href="/windows-hardware/drivers/kernel/controlling-device-namespace-access" data-raw-source="[Controlling Device Namespace Access](../kernel/controlling-device-namespace-access.md)">控制设备命名空间访问</a>。</p>
<p><strong>测试二进制文件：</strong> Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong> DoSubOpensTest</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Fuzz_Sub-opens_with_Streams_test"></span><span id="fuzz_sub-opens_with_streams_test"></span><span id="FUZZ_SUB-OPENS_WITH_STREAMS_TEST"></span>模糊通过流测试打开</p></td>
<td align="left"><p>此测试尝试在设备上打开各种命名数据流。 测试使用一系列任意流名称，这些名称包含的内容和字符对某些设备上的其他用法可能有效。</p>
<p>在 <em>流测试</em>过程中，模糊测试尝试在设备上打开各种命名数据流。 测试使用一系列任意流名称，这些名称包含的内容和字符对某些设备上的其他用法可能有效。 此测试确定驱动程序是否能正确处理数据流请求，尤其是当驱动程序导出不支持或预计数据流的设备时。</p>
<p><em>命名</em>数据流是文件对象的属性。 通过编写文件的名称、冒号和数据流的名称（例如，"File01.txt： AccessDate"，其中 <em>AccessDate</em> 是一个命名的数据流，即 File01.txt 文件的属性），可以指定已命名的数据流。</p>
<p>模糊测试记录测试中使用的流名称。</p>
<p><strong>测试二进制文件：</strong> Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong> DoSubOpensWithStreamsTest</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DoPoolCheck</em></p>
<p><em>DQ</em></p>
<p><em>TestCycles</em></p>
<p><em>ChangeBufferProtectionFlags</em></p>
<p><em>Impersonate</em></p>
<p><em>FillZeroPageWithNull</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Fuzz_Zero-Length_Buffer_FSCTL_test___Fuzz_Zero-Length_Buffer_IOCTL_test"></span><span id="fuzz_zero-length_buffer_fsctl_test___fuzz_zero-length_buffer_ioctl_test"></span><span id="FUZZ_ZERO-LENGTH_BUFFER_FSCTL_TEST___FUZZ_ZERO-LENGTH_BUFFER_IOCTL_TEST"></span>模糊 Zero-Length Buffer FSCTL test/模糊 Zero-Length 缓冲器 IOCTL 测试</p></td>
<td align="left"><p>此测试发出一系列对 <a href="/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl function&lt;/strong&gt;](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl 函数</strong></a> 的调用，其中的输入和/或输出缓冲区长度为0。 该测试通过使用不同的函数代码、设备类型、数据传输方法和访问要求，生成不同的文件系统控制代码。</p>
<p>在 Zero-Length 缓冲区测试期间，模糊测试会发出一系列对 <a href="/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl function&lt;/strong&gt;](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)"><strong>DeviceIoControl 函数</strong></a> 的调用，其中的输入和/或输出缓冲区长度为0。 该测试通过使用不同的函数代码、设备类型、数据传输方法和访问要求，生成不同的 i/o 控制代码。 有关 i/o 控制代码的内容的信息，请参阅 <a href="/windows-hardware/drivers/kernel/defining-i-o-control-codes" data-raw-source="[Defining I/O Control Codes](../kernel/defining-i-o-control-codes.md)">定义 I/o 控制代码</a>。</p>
<p>若要测试驱动程序对无效缓冲区指针的处理，这些用户模式调用中的缓冲区指针指定内核虚拟地址空间中的最大地址，例如 0xFFFFFC00) 。</p>
<p>模糊测试对基本和其他打开的测试中打开的所有设备执行 Zero-Length 的缓冲区测试。 可以通过使用<em>MinFunctionCode</em>和<em>MaxFunctionCode</em>命令参数来自定义此测试，以指定调用中使用的 IOCTL 或 FSCTL 函数代码的<em>范围，并</em>指定<em>MaxDeviceType</em>调用中使用的设备类型的范围。</p>
<p><strong>测试二进制文件：</strong> Devfund_DevicePathExerciser.dll</p>
<p><strong>测试方法：</strong> DoZeroLengthBufferIOCTLTest, DoZeroLengthBufferFSCTLTest</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
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
<td align="left"><p><span id="Run_I_O_Attack"></span><span id="run_i_o_attack"></span><span id="RUN_I_O_ATTACK"></span>运行 i/o 攻击</p></td>
<td align="left"><p>在指定的一个或一些设备上运行 <a href="ioattack.md" data-raw-source="[I/O Attack](ioattack.md)">I/o 攻击</a> 。</p>
<p><strong>测试二进制文件：</strong> Devfund_IOAttack_DeleteDataFile. wsc</p>
<p><strong>测试方法：</strong> RunIoAttack</p>
<p><strong>参数：</strong> - 请参阅 <a href="/windows-hardware/drivers" data-raw-source="[Device Fundamentals Test Parameters](/windows-hardware/drivers)">设备基础测试参数</a></p>
<p><em>DQ</em></p></td>
</tr>
</tbody>
</table>

 

## <a name="about-the-fuzz-open-and-close-test"></a>关于模糊打开和关闭测试


模糊打开和关闭测试使用几种不同的方法来打开和关闭指定设备或设备的实例： [基本打开操作](#basic-open-operations)、 [直接设备打开操作](#direct-device-open-operations)和 [打开和关闭测试](#open-and-close-test)。

### <a name="basic-open-operations"></a>基本打开操作

在 *基本的打开操作* 过程中，模糊测试反复打开 (使用不同方法和选项创建指定设备的) 实例或指定驱动程序导出的设备。

模糊测试始终执行基本的打开操作。 不需要选择它们，也不能从测试会话中排除它们。

模糊测试通过调用适用于设备的系统服务 ([ZwXxx 例程](/previous-versions/windows/hardware/drivers/ff567122(v=vs.85))) ，在用户模式下执行所有打开的操作。 如果打开的调用返回设备的句柄，则模糊测试使用该句柄来执行为测试会话选择的其他设备测试。

基本打开操作有五种类型：

-   **标准打开。** 模糊测试将异步打开设备，并仅指定本机设备名称。

-   **打开并添加反斜杠。** 模糊测试发出设备名称的打开调用，后跟反斜杠 (（如 \) \\ 设备 \\ cdrom \\ ），就像调用打开设备中的根目录一样。

    此操作确定驱动程序或文件系统在其命名空间中管理打开的请求的方式。 具体而言，如果设备不支持在其命名空间中打开请求，驱动程序必须通过失败请求来阻止未经授权的访问，或者 \_ \_ \_ 在调用 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 或 [**IoCreateDeviceSecure**](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure) 以创建设备对象时设置文件设备安全打开的设备特性。

-   **以命名管道形式打开。** 模糊测试打开设备并为设备建立命名管道。 Access 参数 (ShareAccess) 最初设置为 "读取" 和 "写入"，但如果请求失败，则会调整此参数。 如果设备不支持命名管道，则该请求将失败。

-   **作为 mailslot 打开。** 模糊测试将设备作为 mailslot 打开。 如果设备不支持此类型的连接，则该请求将失败。

-   **作为树连接打开。** 模糊测试将设备作为树连接打开，以便在远程网络访问中使用。 Access 参数 (ShareAccess) 最初设置为 "读取" 和 "写入"，但如果请求失败，则会调整此参数。 如果设备不支持此类型的连接，则该请求将失败。

打开调用中使用的参数会因设备特征而异，并使调用成功。 例如，如果基本打开操作因为调用未满足设备的安全要求而失败，则模糊测试将使用对较少访问的请求来重复打开操作。 例如，如果请求写入访问权限的打开操作返回安全冲突错误，则使用读取访问请求重复打开。

### <a name="direct-device-open-operations"></a>直接设备打开操作

在 *直接设备打开操作* 期间，模糊测试会直接以设备形式打开设备，而不是以文件系统中的文件形式打开设备。 直接设备打开操作始终是同步的。 如果调用成功，模糊测试会使用提供的句柄来执行其他选定的测试。

### <a name="open-and-close-test"></a>打开并关闭测试

在 *打开和关闭测试* 的过程中，模糊测试会创建多个线程，每个线程都执行数千个开结-闭合序列。 这会测试驱动程序处理大量其他简单和预期调用的能力。

打开和关闭测试使用在 [基本打开操作](#basic-open-operations) 中使用的相同选项，并使用添加的反斜杠测试打开并在这些测试之前执行。

## <a name="related-topics"></a>相关主题


[如何在运行时使用 Visual Studio 测试驱动程序](/windows-hardware/drivers)

[如何选择和配置设备基础功能测试](/windows-hardware/drivers)

[设备基础功能测试](device-fundamentals-tests.md)

[设备基础功能测试参数](/windows-hardware/drivers)

[Provided WDTF Simple I/O plug-ins](../wdtf/provided-wdtf-simpleio-plug-ins.md)（提供的 WDTF 简单 I/O 插件）

[如何在运行时通过命令提示符测试驱动程序](/windows-hardware/drivers)

