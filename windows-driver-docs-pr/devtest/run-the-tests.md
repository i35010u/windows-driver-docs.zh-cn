---
title: 运行测试
description: Windows 驱动程序的数据驱动的 SysFund 测试的测试和配置文件说明
keywords:
- Sysfund 测试
- 数据驱动的测试
- SDEL 查询
ms.date: 11/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ab393dd0e4794015c8a96535b2d3b9d4461e6eb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840046"
---
# <a name="run-the-tests"></a>运行测试
## <a name="description-of-the-tests-and-configuration-file"></a>测试和配置文件的说明
可以在 \<解压 EWDK 根 > \Program Files\Windows Kits\10\Testing\Tests\Additional Tests\x64\DevFund\DataDriven. 中找到数据驱动的 SysFund 测试  数据驱动的测试套件由以下文件组成：

- 使用 XML 配置文件 WDTFTest 的五个测试 DLL：

  *   Sysfund_Device_IO_DataDriven
  *   Sysfund_PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven
  *   Sysfund_PNP_RemoveAndRestartDevice_DataDriven
  *   Sysfund_RebootRestart_With_IO_During_DataDriven
  *   Sysfund_Sleep_With_IO_BeforeAndAfter_DataDriven
- 使用 XML 配置文件 WDTFTest 的两个实用工具 DLL：
  *   Utility_DeviceStatusCheck_DataDriven
  *   Utility_EnableDisableDriverVerifier_DataDriven
- XML 配置文件：
      *   WDTFTest

**系统设备 i/o 测试**
-   Binary： Sysfund_Device_IO_DataDriven
-   此测试将 i/o 发送到系统上的所有设备

**使用 IO （可靠性）前后的系统-PNP （禁用和启用）**
-   Binary： Sysfund_PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven
-   [文档](https://docs.microsoft.com/windows-hardware/test/hlk/testref/b2849bf1-3478-4fd7-a577-31001084e908)

**系统-PNP 删除设备测试（可靠性）**
-   Binary： Sysfund_PNP_RemoveAndRestartDevice_DataDriven
-   [文档](https://docs.microsoft.com/windows-hardware/test/hlk/testref/ead2222e-4485-4bfc-84cd-43ac0d2e8181)

**系统 - 使用期间 IO 重新引导/重启（可靠性）**
-   Binary： Sysfund_RebootRestart_With_IO_During_DataDriven
-   [文档](https://docs.microsoft.com/windows-hardware/test/hlk/testref/6d6ed5ec-1765-4569-a7ac-20ed7869d89a)

**系统-IO 前后的 IO （可靠性 SysFund）** 
-   Binary： Sysfund_Sleep_With_IO_BeforeAndAfter_DataDriven
-   [文档](https://docs.microsoft.com/windows-hardware/test/hlk/testref/16ac817e-b042-4679-8027-c6c44d1ce29f)

**设备状态检查**
-   Binary： Utility_DeviceStatusCheck_DataDriven
-   此实用程序 DLL 验证目标设备的问题代码是否为0（正常工作）。  它通常用于运行 SysFund 测试，以验证目标设备是否正常工作。

**启用/禁用驱动程序验证程序**
-   Binary： Utility_EnableDisableDriverVerifier_DataDriven
-   此实用程序启用或禁用与目标设备相关的驱动程序的驱动程序验证程序。

**数据驱动的测试配置文件**
-   文件： WDTFTest
-   此文件包含数据驱动的 SysFund 测试和关联的实用程序的所有配置信息。

## <a name="configure-the-tests"></a>配置测试

数据驱动的测试配置文件（WDTFTest）包含多个元素，这些元素定义传递给测试和实用工具的参数。  所有数据驱动的测试和实用工具共享相同的配置文件（WDTFTest）。  默认情况下，配置文件会将测试和实用程序配置为面向系统上的所有设备，但可以轻松地对其进行自定义以满足测试通过的要求。

如下所示，可对配置文件进行自定义，以便测试和实用工具将系统上的任何设备集（从一个设备或驱动程序定向到所有设备和驱动程序）。

测试和实用工具将仅使用所需的元素，并且将忽略所有其他元素。
### <a name="wdtftestxml-parameter-descriptions-and-use"></a>WDTFTest 参数说明和用法
#### <a name="configuring-the-sdel-query"></a>配置 SDEL 查询
[SDEL 语言](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)用于创建查询，该查询可返回测试和实用程序的目标设备。 使用和语句将以下 SDEL 相关参数一起用于创建完整的查询：

**SDEL**：值*IsDevice*指定系统上的完整设备集。  通常，除非您只想测试特定驱动程序或设备，否则不会编辑此参数。  接下来，与 SDEL 相关的参数将通过指定应从测试中排除的驱动程序或设备，从此超集创建设备子集，因此此参数可以保持不变。
```
    <Parameter Name="SDEL">IsDevice</Parameter>
```

**SdelExcludeVMDevnode**：排除对 VM 操作至关重要的设备节点，并且无法禁用。  此参数应保持不变，因为如果系统不是虚拟机，则它不起作用。
```
    <Parameter Name="SdelExcludeVMDevnode">(DisplayName!='Microsoft Hyper-V Virtual Machine Bus')</Parameter>
```

**SdelExcludeDrivers**：建议使用 SDEL 排除驱动程序和/或设备。  例如，你可以使用它来排除具有已知 bug 的驱动程序或缩小测试范围。  默认情况下，以默认的 ```(DriverBinaryNames!='')``` 目标为系统上所有设备（如上文所述的 "Microsoft Hyper-V 虚拟机总线" 设备节点除外）的所有驱动程序。
```
    <Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!='')</Parameter>
```

#### <a name="general-test-configuration-parameters"></a>常规测试配置参数
**TestCycles**：指定测试应运行的迭代数。
```
    <Parameter Name="TestCycles">1</Parameter>
```

**IOPeriod**指定 i/o 应运行的分钟数。
```
    <Parameter Name="IOPeriod">1</Parameter>
```

**ResumeDelay**：指定在从睡眠状态恢复后发送 i/o 前等待的秒数。
```
    <Parameter Name="ResumeDelay">10</Parameter>
```

**Wpa2PskAesSsid**：指定测试 WiFi 访问点的名称。
```
    <Parameter Name="Wpa2PskAesSsid">WiFiRouterName</Parameter>
```

**Wpa2PskPassword**：指定测试 WiFi 访问点的密码。
```
    <Parameter Name="Wpa2PskPassword">WiFiRouterPassword</Parameter>
```

#### <a name="parameters-that-apply-to-utility_enabledisabledriververifier_datadrivendll-only"></a>仅适用于 ```utility_enabledisabledriververifier_datadriven.dll``` 的参数：

**DriverVerifierLevel**：0x209BB 的默认值等于[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)的 "标准标志"。
```
    <Parameter Name="DriverVerifierLevel">0x209BB</Parameter>
```

**AddOnly**：指定生成的 SDEL 查询结果应将驱动程序添加到驱动程序验证程序，而无需删除任何。  如果已在应追加而不是替换的一组驱动程序上启用了驱动程序验证程序，则此方法非常有用。
```
    <Parameter Name="AddOnly">false</Parameter>
```

**NoReboot**：指定计算机不应自动重新启动以启用驱动程序验证程序设置。  如果将*NoReboot*参数设置为 true，则在手动重新启动计算机之前，扩充的驱动程序验证程序设置将不会生效。
```
    <Parameter Name="NoReboot">false</Parameter>
```

### <a name="enable-driver-verifier"></a>启用驱动程序验证程序
若要打开驱动程序验证程序，请运行以下命令：
```
    te.exe utility_enabledisabledriververifier_datadriven.dll /name:Utility_DriverVerifier#0::EnableDriverVerifier /rebootstatefile=state.xml 
```
在某些情况下，计算机可能无法重新启动。  这是测试框架的已知技术限制。  如果在使用此实用程序更改驱动程序验证程序设置后30秒内未开始重启计算机，则必须手动重新启动计算机，更新的驱动程序验证程序设置才能生效。

重新启动后，打开命令提示符并运行**verifier/querysettings** ，以确保已启用驱动程序验证程序。

### <a name="verify-devices-are-working"></a>验证设备是否正常工作
数据驱动的 SysFund 测试预期测试目标的所有设备都有问题代码0（正常工作）。  若要确保所有目标设备都正常工作，请使用 DeviceStatusCheck 实用工具：
```
    te.exe Utility_DeviceStatusCheck_DataDriven.dll
```
此实用程序使用 WDTFTest 中定义的 SDEL 查询来查找所测试设备集，并验证它们都有**问题代码 0**。  "通过" 结果表示查询的设备集全部工作正常。 查看**TestTextLog**以调查失败。  有关设备管理器问题代码的说明，请参阅[设备管理器错误消息](https://docs.microsoft.com/windows-hardware/drivers/install/device-manager-error-messages)。

### <a name="launch-a-test"></a>启动测试
若要启动一个数据驱动的 SysFund 测试，请使用以下命令：
```
    te.exe Sysfund_PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven.dll
```
```
    te.exe Sysfund_Sleep_With_IO_BeforeAndAfter_DataDriven.dll
```
### <a name="refine-the-configuration-file"></a>优化配置文件
在进行任何更改之前，应备份 WDTFTest 的原始副本。

可以根据数据驱动的 SysFund 测试的结果来优化测试配置文件（WDTFTest）。  例如，如果最初针对系统上的所有设备运行数据驱动的 SysFund 测试，而某个特定设备或驱动程序未通过该测试，则测试配置文件可更新为在调查 bug 时筛选出该设备的测试。  这允许在调查 bug 时并行继续进行测试。

若要筛选出特定设备，请编辑 WDTFTest 中的**SdelExcludeDrivers**元素。  下面的代码筛选出*mydriver*，例如： 
```
<Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!=’mydriver.sys’)</Parameter>
```

同样，以下代码将基于设备实例路径筛选出设备：
```
<Parameter Name="SdelExcludeDrivers">(DeviceId!=’my\device\id’)</Parameter>
```
可以创建复杂的 SDEL 查询来筛选出多个设备：
```
<Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!=’mydriver1.sys’ AND DriverBinaryNames!=’mydriver2.sys’)</Parameter>
```

修复 mydriver1.inf 和 mydriver2.inf 会被中的 bug 后，可以将 WDTFTest 中的**SdelExcludeDrivers**元素重置为默认值，以将这些驱动程序和关联的设备作为目标添加：
```
    <Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!='')</Parameter>
```

## <a name="troubleshooting-problems"></a>疑难解答问题
### <a name="malformed-sdel-query-in-the-configuration-file"></a>配置文件中的 SDEL 查询格式不正确
以下错误消息表示 WDTFTest 配置文件中包含格式不正确的 SDEL 查询：
```
    Error: Verify: SUCCEEDED(m_pDeviceDepot->Query(CComBSTR(DQ), &m_pTestTargets)) - Value (0x80070057) [File: onecore\base\tools\wdtf\tests\devfund\datadriven\sysfund_pnp_disableenable_with_io_beforeandafter_datadriven\test.cpp, Function: PNP_DisableEnable_With_IO_BeforeAndAfter::PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven_Test, Line: 231]
    EndGroup: PNP_DisableEnable_With_IO_BeforeAndAfter::PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven_Test#0 [Failed]
```
HRESULT "0x80070057" 表示 "E_INVALIDARG：一个或多个参数无效"。 请仔细检查 WDTFTest 配置文件中的[SDEL 文档](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)，并查找可能导致此错误的格式不正确的查询。

### <a name="test-is-blocked-because-it-might-reboot-the-machine"></a>测试被阻止，因为它可能会重新启动计算机
某些 SysFund 测试可以在测试期间重新启动计算机。 若要运行可重新启动计算机的测试，必须使用 "/rebootstatefile" 参数：
```
    te.exe <testname> /rebootstatefile=state.xml
```
如果未将/rebootstatefile 参数传递给测试，则会显示以下消息并阻止测试：
```
    TestBlocked: TAEF: This test cannot be run as it might reboot the machine.
    EndGroup: Sysfund_RebootRestart_With_IO_During::Sysfund_RebootRestart_With_IO_During_DataDriven_Test#0 [Blocked]
```

### <a name="test-is-blocked-because-the-sdel-query-contains--characters"></a>测试被阻止，因为 SDEL 查询包含 "&" 字符
当指定基于设备实例路径值的设备的 SDEL 查询时，路径中的 "&" 字符必须替换为 "& amp\;"。 以下消息表示 WDTFTest 配置文件，该文件包含设备实例路径中的 "&" 字符：
```
    TestBlocked: TAEF: [HRESULT: 0xC00CEE22] Error while getting value for 'SDEL' in table 'DataDrivenSysfundTable' in DataSource 'WDTFTest.xml' on line 24.
    EndGroup: PNP_DisableEnable_With_IO_BeforeAndAfter::PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven_Test#error [Blocked]
```
这是生成上述错误消息的 WDTFTest 配置文件中的 XML：
```
    <Parameter Name="SDEL">IsDevice AND deviceid='PCI\VEN_11AB&DEV_2B38&SUBSYS_045E0003&REV_00\4&91A2562&0&00E8'</Parameter>
```
这是用于修复错误的 deviceid 的格式正确的值：
```
    <Parameter Name="SDEL">IsDevice AND deviceid='PCI\VEN_11AB&DEV_2B38&SUBSYS_045E0003&REV_00\4&91A2562&0&00E8'</Parameter>
```

### <a name="other-issues"></a>其他问题
若要帮助解决此处未列出的其他问题，请参阅[DevFund 其他文档](https://docs.microsoft.com/windows-hardware/test/hlk/testref/device-devfund-additional-documentation)。
