---
title: Windows Hello 指纹驱动程序签名过程
description: Windows Hello 指纹驱动程序签名过程
ms.assetid: 803f4326-32ce-44b4-a2fb-6c6f245c3728
keywords:
- 生物识别驱动程序 WDK，windows hello
- 签名生物识别驱动程序
ms.date: 07/19/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1067c95e922d6880f1ee6f0984ff9a659ce25df
ms.sourcegitcommit: cfd4d8ee889c6a3feed79ae112662f6c095b6a36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94417426"
---
# <a name="windows-hello-steps-to-submit-a-fingerprint-driver"></a>Windows Hello：提交指纹驱动程序的步骤


## <a name="submitting-a-fingerprint-driver-for-windows-hello-compatibility"></a>提交用于 Windows Hello 兼容性的指纹驱动程序 
Microsoft 在生物识别传感器上引入了新的要求，以遵守 Windows Hello 质量准则。 需要新的手动审阅过程才能获得与 Windows Hello 互操作的批准。 系统会强制执行该过程，其中包含通过 Windows DevCenter (获取的特定签名的操作系统检查： https://developer.microsoft.com/) 只能通过执行本文档中的过程来获取。 6/1/17 之前由 WHQL 创建和签名的驱动程序 grandfathered。 在此日期之后未获取此签名的新的和更新的驱动程序将不能在 Windows Hello 的 Windows Hello 版本1703或更高版本中使用。

驱动程序将始终手动批准以获取 Windows Hello 签名。 批准的驱动程序的更新可以引用以前的提交以获得更快的批准。 如果驱动程序适用于新的传感器，或对匹配引擎所做的更改影响到了远、FRR 或表示攻击检测，则必须对其进行新的审核。 

生物识别签名强制日期为6/1/2017，之后将不会加载不包含 bio 签名的驱动程序，并且这些驱动程序将不再适用于 Windows Hello。

### <a name="step-one-create-a-biometric-driver"></a>步骤1：创建生物识别驱动程序
按照此处的说明创建生物识别驱动程序： 

[Windows 生物识别框架](/windows/desktop/SecBioMet/biometric-service-api-portal)

### <a name="step-two-test-your-sensor-and-self-validate"></a>步骤2：测试传感器和自我验证
自行验证传感器和驱动程序，确保它们满足 Microsoft 的生物识别要求，并在指纹安全检查模板中报告调查结果。 在连接时，可在指纹合作伙伴包中找到要求和模板的文档。 如果你没有连接访问权限，请与你的 Microsoft 代表联系。

### <a name="step-three-modify-the-driver-configuration-xml-file"></a>步骤3：修改驱动程序配置 xml 文件
提交驱动程序时，Windows 10 版本1703指纹检测测试将进行检查，以确保 <vendorCompliance> 和 <securityReview> 标记包含在以下字段中：

**bugId** ：包含之前批准的安全审核信息的以前的 HLK 提交 ID 号; 如果提交正在进行全新的安全检查，则为0。

**updateExistingSubmission** ：如果提交作为之前已完成安全检查的提交的更新，则为 true; 否则为 false。

#### <a name="example"></a>示例
 ```cpp
<?xml version="1.0" encoding="utf-8"?>
<bioTestConfiguration version="0" runOptional="false" runInteractive="true" abortOnFailure="false" manualStep="false" priority="3" logType="WTT">
  <vendorCompliance>
    <securityReview bugId="12345678" updateExistingSubmission="true"/>
  </vendorCompliance>
  <testSuites>
    <testSuite deviceRequired="false" id="StorageAdapter">
      <library>storagetest.dll</library>
      <description>storage Adapter Test Suite</description>
    </testSuite>
  </testSuites>
  <deviceInfo>
         <sensorAdapterLib>WinbioSensorAdapter.dll</sensorAdapterLib>
         <engineAdapterLib>vcsWBFEngineAdapter.dll</engineAdapterLib>
         <storageAdapterLib>winbiostorageadapter.dll</storageAdapterLib>
         <indicatorSupported>0</indicatorSupported>
         <supportedModes>
             <supportedMode>0x01</supportedMode>
         </supportedModes>
         <supportedPurposes>
             <supportedPurpose>0x01</supportedPurpose>
             <supportedPurpose>0x02</supportedPurpose>
             <supportedPurpose>0x04</supportedPurpose>
         </supportedPurposes>
  </deviceInfo>
</bioTestConfiguration>
 ```
### <a name="step-four-modify-the-driver-configuration-inf"></a>步骤4：修改驱动程序配置 inf
生物识别驱动程序包需要提交到新的 DevCenter 门户，才能获取所需的 Windows Hello 签名并将其上传到 WU。 包需要包含驱动程序 INF 文件中的特定属性，以正确指定适配器 dll 获取数字签名。 下面的示例演示了用于获取适配器二进制文件的 bio 签名及其相关库的格式设置。

例如，如果驱动程序包中包含一个名为 sensor.dll、engine.dll 和 storage.dll 的传感器、引擎和存储适配器，并且其中一个已加载 stringparser.dll，则若要在每个文件上获取 bio 签名，则 INF 文件必须包含以下组件：

```cpp
[SignatureAttributes]
sensor.dll = SignatureAttributes.WindowsHello
engine.dll = SignatureAttributes.WindowsHello
storage.dll = SignatureAttributes.WindowsHello
stringparser.dll = SignatureAttributes.WindowsHello

[SignatureAttributes.WindowsHello]
WindowsHello = true
```

此步骤最重要的是确保你的驱动程序收到合适的认证。 如果要在提交到 DevCenter 时获得生物识别签名，则所有第三方生物识别适配器文件和这些适配器加载的任何第三方 dll 都需要标记并包含在此方法中。

### <a name="step-five-run-the-hlk-test-suite"></a>步骤5：运行 HLK 测试套件
在步骤3和4中，进行的 HLK 测试可确保进行上述修改，如果不存在配置信息，将会失败。
在 HLK studio 中打包最终的 HLK 时，包括在 bug 中提交的安全审阅模板作为补充文件。

### <a name="step-six-submit-the-driver-package-and-hlk-logs"></a>步骤6：提交驱动程序包和 HLK 日志
将打包的 HLK 文件提交到 DevCenter 进行检查。 Microsoft 内的功能团队将在收到手动审查过程时收到提交通知。 团队将在 HLK 包中查看提交的模板，以确保自我验证的信息满足 Microsoft 的生物识别要求。

### <a name="step-seven-wait-for-microsoft-approval-and-signing"></a>步骤7：等待 Microsoft 审批和签名
Microsoft 将批准提交，前提是它满足所有的生物识别要求，保证生物识别签名不会对驱动程序使用 Windows Hello 进行认证。 例如，可以在检查签名的 inf 配置文件中排除文件。 如果在 OS 强制签名时加载此文件，则加载将失败，并且驱动程序将不能与 Windows Hello 一起运行。 已签名的驱动程序应由 IHV 和 OEM 测试，以确保它在总体系统中有效。

### <a name="step-eight-update-an-existing-driver"></a>步骤8：更新现有的驱动程序
如果需要对之前签名的驱动程序进行更新，请按照步骤3中的说明填写更新的驱动程序的驱动程序配置 xml 中的 bugId 和 updateExistingSubmission 字段。
如果正在对 grandfathered 驱动程序进行更新，则应使用相同的步骤。 BugId 字段应设置为 grandfathered 驱动程序的提交 ID，updateExistingSubmission 字段应设置为 true。
驱动程序配置 xml 应包含在提交的驱动程序包中。

## <a name="related-topics"></a>相关主题


[Windows Hello 面部身份验证](/windows-hardware/design/device-experiences/windows-hello-face-authentication)

[Windows Hello](/windows-hardware/design/device-experiences/windows-hello)

[生物识别设备设计指南](./index.md)