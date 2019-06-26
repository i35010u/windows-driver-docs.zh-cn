---
title: 运行测试
description: Windows 驱动程序的测试数据驱动 SysFund 测试和配置文件的说明
keywords:
- Sysfund 测试
- 数据驱动的测试
- SDEL 查询
ms.date: 11/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60f92999cba81a5b7c6b0a9c6cda1e535559a9f1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353869"
---
# <a name="run-the-tests"></a>运行测试
## <a name="description-of-the-tests-and-configuration-file"></a>测试和配置文件的说明
您可以找到在数据驱动的 SysFund 测试\<解压缩的 EWDK 根 > files\windows Kits\10\Testing\Tests\Additional Tests\x64\DevFund\DataDriven。  数据驱动的测试套件包括以下文件：

- 五条测试 DLL 的使用 XML 配置文件 WDTFTest.xml:

  *   Sysfund_Device_IO_DataDriven.dll
  *   Sysfund_PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven.dll
  *   Sysfund_PNP_RemoveAndRestartDevice_DataDriven.dll
  *   Sysfund_RebootRestart_With_IO_During_DataDriven.dll
  *   Sysfund_Sleep_With_IO_BeforeAndAfter_DataDriven.dll
- 两个实用程序 DLL 的使用哪一个 XML 配置文件 WDTFTest.xml:
  *   Utility_DeviceStatusCheck_DataDriven.dll
  *   Utility_EnableDisableDriverVerifier_DataDriven.dll
- XML 配置文件：
      *   WDTFTest.xml

**系统-设备 I/O 测试**
-   二进制：Sysfund_Device_IO_DataDriven.dll
-   此测试将 I/O 发送到系统上的所有设备

**系统-PNP （禁用和启用） 与 IO 之前和之后 （可靠性）**
-   二进制：Sysfund_PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven.dll
-   [文档](https://docs.microsoft.com/windows-hardware/test/hlk/testref/b2849bf1-3478-4fd7-a577-31001084e908)

**系统-即插即用中删除设备测试 （可靠性）**
-   二进制：Sysfund_PNP_RemoveAndRestartDevice_DataDriven.dll
-   [文档](https://docs.microsoft.com/windows-hardware/test/hlk/testref/ead2222e-4485-4bfc-84cd-43ac0d2e8181)

**系统 - 使用期间 IO 重新引导/重启（可靠性）**
-   二进制：Sysfund_RebootRestart_With_IO_During_DataDriven.dll
-   [文档](https://docs.microsoft.com/windows-hardware/test/hlk/testref/6d6ed5ec-1765-4569-a7ac-20ed7869d89a)

**系统-IO (可靠性 SysFund) 前后的睡眠** 
-   二进制：Sysfund_Sleep_With_IO_BeforeAndAfter_DataDriven.dll
-   [文档](https://docs.microsoft.com/windows-hardware/test/hlk/testref/16ac817e-b042-4679-8027-c6c44d1ce29f)

**设备状态检查**
-   二进制：Utility_DeviceStatusCheck_DataDriven.dll
-   此实用程序 DLL 验证目标设备问题代码为 0 （正常）。  它通常用于运行 SysFund 测试之前验证目标设备正常工作。

**启用/禁用驱动程序验证程序**
-   二进制：Utility_EnableDisableDriverVerifier_DataDriven.dll
-   此实用程序启用或禁用驱动程序验证程序关联的目标设备的驱动程序。

**数据驱动的测试配置文件**
-   文件：WDTFTest.xml
-   此文件包含所有的数据驱动的 SysFund 测试和相关的实用程序的配置信息。

## <a name="configure-the-tests"></a>配置测试

数据驱动的测试配置文件 (WDTFTest.xml) 包含几个元素，定义的测试和实用程序传递的参数。  数据驱动的测试和实用程序的所有共享相同的配置文件 (WDTFTest.xml)。  默认情况下，配置文件配置的测试和实用程序以面向所有设备的系统上，但这可以轻松地自定义以满足测试轮次的要求。

如下所示，以便测试和实用程序将面向任何组在系统上，从一个设备或驱动程序添加到所有设备和驱动程序的设备，配置文件可以进行自定义。

测试和实用程序将使用所需的元素，将忽略所有其他元素。
### <a name="wdtftestxml-parameter-descriptions-and-use"></a>WDTFTest.xml 参数说明和使用
#### <a name="configuring-the-sdel-query"></a>配置 SDEL 查询
[SDEL 语言](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)用于创建返回测试和实用程序的目标设备的查询。 将以下 SDEL 相关参数一起使用 AND 语句创建完整的查询：

**SDEL**:该值*IsDevice*指定完整的一组设备在系统上。  通常情况下，不编辑此参数，除非你只想要测试的特定驱动程序或设备。  下一步 SDEL 相关参数将通过指定驱动程序从此超集创建设备的子集或不进行测试，以便可以在此参数的设备保持不变。
```
    <Parameter Name="SDEL">IsDevice</Parameter>
```

**SdelExcludeVMDevnode**:排除设备节点的 VM 操作的关键，并且不能禁用。  此参数应留保持不变，因为它具有不起作用，如果系统不是虚拟机。
```
    <Parameter Name="SdelExcludeVMDevnode">(DisplayName!='Microsoft Hyper-V Virtual Machine Bus')</Parameter>
```

**SdelExcludeDrivers**： 这是使用 SDEL 驱动程序和/或设备中排除的建议的位置。  例如，您可以以此排除具有已知 bug 的驱动程序，或若要缩小测试范围。  使用默认值为运行```(DriverBinaryNames!='')```面向的所有设备 （除如上文所述的"Microsoft HYPER-V 虚拟机总线"设备节点） 的系统上的所有驱动程序。
```
    <Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!='')</Parameter>
```

#### <a name="general-test-configuration-parameters"></a>一般测试的配置参数
**TestCycles**:指定应运行测试的迭代数。
```
    <Parameter Name="TestCycles">1</Parameter>
```

**IOPeriod**指定多少分钟 I/O 应运行。
```
    <Parameter Name="IOPeriod">1</Parameter>
```

**ResumeDelay**:指定要从恢复后发送 I/O 之前所等待的秒数进入睡眠状态。
```
    <Parameter Name="ResumeDelay">10</Parameter>
```

**Wpa2PskAesSsid**:指定测试 WiFi 接入点的名称。
```
    <Parameter Name="Wpa2PskAesSsid">WiFiRouterName</Parameter>
```

**Wpa2PskPassword**:指定测试 WiFi 接入点的密码。
```
    <Parameter Name="Wpa2PskPassword">WiFiRouterPassword</Parameter>
```

#### <a name="parameters-that-apply-to-utilityenabledisabledriververifierdatadrivendll-only"></a>将应用于参数```utility_enabledisabledriververifier_datadriven.dll```仅：

**DriverVerifierLevel**:0x209BB 的默认值等于"标准标志" [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。
```
    <Parameter Name="DriverVerifierLevel">0x209BB</Parameter>
```

**只添加**:指定生成 SDEL 查询结果，应该不删除任何与 Driver Verifier 添加驱动程序。  这是上一系列驱动程序应该追加而不是替换为已启用驱动程序验证程序的情况下很有用。
```
    <Parameter Name="AddOnly">false</Parameter>
```

**NoReboot**:指定的计算机应不自动重新启动来启用驱动程序验证程序设置。  如果*NoReboot*参数设置为 true，增强的驱动程序验证程序设置将不会生效之前手动重新启动计算机。
```
    <Parameter Name="NoReboot">false</Parameter>
```

### <a name="enable-driver-verifier"></a>启用驱动程序验证程序
若要启用驱动程序验证程序，请运行以下命令：
```
    te.exe utility_enabledisabledriververifier_datadriven.dll /name:Utility_DriverVerifier#0::EnableDriverVerifier /rebootstatefile=state.xml 
```
在某些情况下，计算机可能不会重新启动。  这是测试框架是已知技术限制。  如果计算机不会开始在更改此实用程序的驱动程序验证程序设置后的 30 秒内重新启动，您必须手动重新启动计算机已更新的驱动程序验证程序设置，才会生效。

重新启动后，打开命令提示符并运行**verifier /querysettings**以确保已启用驱动程序验证程序。

### <a name="verify-devices-are-working"></a>验证设备正常工作
数据驱动的 SysFund 测试预期要有问题的代码为 0 （正常） 的测试所针对的任何设备。  若要确保所有设备作为目标在正常工作，请使用 DeviceStatusCheck 实用程序：
```
    te.exe Utility_DeviceStatusCheck_DataDriven.dll
```
此实用工具使用 WDTFTest.xml 中定义的 SDEL 查询找到的一组待测试的设备，并验证它们都具有**问题代码 0**。  "通过"结果意味着查询设备的组是所有正常运行。 审阅**TestTextLog.log**为调查故障。  设备管理器问题代码的说明，请参阅[设备管理器错误消息](https://docs.microsoft.com/windows-hardware/drivers/install/device-manager-error-messages)。

### <a name="launch-a-test"></a>启动测试
若要启动数据驱动的 SysFund 测试之一，请使用以下命令：
```
    te.exe Sysfund_PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven.dll
```
```
    te.exe Sysfund_Sleep_With_IO_BeforeAndAfter_DataDriven.dll
```
### <a name="refine-the-configuration-file"></a>优化配置文件
应进行任何更改之前备份 WDTFTest.xml 的原始副本。

测试配置文件 (WDTFTest.xml) 可以是经过优化的基于数据驱动 SysFund 测试的结果。  例如，如果数据驱动的 SysFund 测试最初运行目标系统上的所有设备和一个特定设备或驱动程序，则测试失败，可以调查 bug 时，筛选出测试该设备的更新测试配置文件。  这样，测试时能够继续执行并行调查 bug。

若要筛选出特定设备，请编辑**SdelExcludeDrivers** WDTFTest.xml 中的元素。  下面的代码筛选器扩展*mydriver.sys*，例如： 
```
<Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!=’mydriver.sys’)</Parameter>
```

同样，下面的代码筛选器扩展基于设备实例路径的设备：
```
<Parameter Name="SdelExcludeDrivers">(DeviceId!=’my\device\id’)</Parameter>
```
您可以创建复杂 SDEL 查询来筛选出多个设备：
```
<Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!=’mydriver1.sys’ AND DriverBinaryNames!=’mydriver2.sys’)</Parameter>
```

修复在 mydriver1.sys 和 mydriver2.sys bug 后，可以重置**SdelExcludeDrivers** WDTFTest.xml 中要包括这些驱动程序和关联的设备作为目标的默认值的元素：
```
    <Parameter Name="SdelExcludeDrivers">(DriverBinaryNames!='')</Parameter>
```

## <a name="troubleshooting-problems"></a>故障排除问题
### <a name="malformed-sdel-query-in-the-configuration-file"></a>配置文件中的格式不正确 SDEL 查询
以下的错误消息为指示的格式不对 SDEL 查询 WDTFTest.xml 配置文件中包含：
```
    Error: Verify: SUCCEEDED(m_pDeviceDepot->Query(CComBSTR(DQ), &m_pTestTargets)) - Value (0x80070057) [File: onecore\base\tools\wdtf\tests\devfund\datadriven\sysfund_pnp_disableenable_with_io_beforeandafter_datadriven\test.cpp, Function: PNP_DisableEnable_With_IO_BeforeAndAfter::PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven_Test, Line: 231]
    EndGroup: PNP_DisableEnable_With_IO_BeforeAndAfter::PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven_Test#0 [Failed]
```
HRESULT"0x80070057"意味着"E_INVALIDARG:一个或多个参数是无效的"。 请仔细检查 WDTFTest.xml 配置文件对照[SDEL 文档](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)并查找可能导致此错误的查询格式不正确。

### <a name="test-is-blocked-because-it-might-reboot-the-machine"></a>测试是被阻止，因为它可能会重新启动计算机
某些 SysFund 测试可以在测试过程中重新启动计算机。 若要运行的测试可以重新启动计算机，"/ rebootstatefile"必须使用参数：
```
    te.exe <testname> /rebootstatefile=state.xml
```
如果不传递给测试的 /rebootstatefile 参数，将显示以下消息，并测试将被阻止：
```
    TestBlocked: TAEF: This test cannot be run as it might reboot the machine.
    EndGroup: Sysfund_RebootRestart_With_IO_During::Sysfund_RebootRestart_With_IO_During_DataDriven_Test#0 [Blocked]
```

### <a name="test-is-blocked-because-the-sdel-query-contains--characters"></a>测试是阻止因为 SDEL 查询包含 & 字符
当后缀 SDEL 查询该设备为目标值基础其设备实例路径，& 路径中的字符必须是将替换为"& a m p\;"。 是指示 WDTFTest.xml 配置文件，其中包含 & 字符设备实例路径中的以下消息：
```
    TestBlocked: TAEF: [HRESULT: 0xC00CEE22] Error while getting value for 'SDEL' in table 'DataDrivenSysfundTable' in DataSource 'WDTFTest.xml' on line 24.
    EndGroup: PNP_DisableEnable_With_IO_BeforeAndAfter::PNP_DisableEnable_With_IO_BeforeAndAfter_DataDriven_Test#error [Blocked]
```
这是生成上面的错误消息的 WDTFTest.xml 配置文件中的 XML:
```
    <Parameter Name="SDEL">IsDevice AND deviceid='PCI\VEN_11AB&DEV_2B38&SUBSYS_045E0003&REV_00\4&91A2562&0&00E8'</Parameter>
```
这是 deviceid 修复该错误的格式正确的值：
```
    <Parameter Name="SDEL">IsDevice AND deviceid='PCI\VEN_11AB&DEV_2B38&SUBSYS_045E0003&REV_00\4&91A2562&0&00E8'</Parameter>
```

### <a name="other-issues"></a>其他问题
有关此处未列出其他问题疑难解答的帮助，请参阅[Device.DevFund 其他文档](https://docs.microsoft.com/windows-hardware/test/hlk/testref/device-devfund-additional-documentation)。
