---
title: Windows Hello 指纹驱动程序签名过程
description: Windows Hello 指纹驱动程序签名过程
ms.assetid: 803f4326-32ce-44b4-a2fb-6c6f245c3728
keywords:
- 生物识别驱动程序 WDK，windows 你好
- 签名生物识别驱动程序
ms.author: dawnwood
ms.date: 07/19/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c2ad4afc2031afb34057ad75f053c9065ff830c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576853"
---
# <a name="windows-hello-steps-to-submit-a-fingerprint-driver"></a>Windows Hello：提交指纹驱动程序的步骤


## <a name="submitting-a-fingerprint-driver-for-windows-hello-compatibility"></a>正在提交用于 Windows Hello 兼容性的指纹驱动程序 
Microsoft 引入了新的要求，在生物识别传感器以符合 Windows Hello 质量准则。 新的手动审核过程将需要获得批准才能与 Windows Hello 进行互操作。 该过程将使用 OS 强制实施通过 Windows 开发人员中心获取的特定签名的检查 (此处： https://developer.microsoft.com/)仅可以通过反映经受该流程本文档中的获取的。 已创建并前 6/1/17 通过 WHQL 签名的驱动程序被 grandfathered。 在此日期之后未获得此签名的新的和更新驱动程序不会使用 Windows Hello 在 Window 10，版本 1703年或更高版本之后强制日期。

驱动程序将始终进行手动批准，若要获取 Windows Hello 签名。 已批准的驱动程序的更新可以引用以前提交的速度更快的批准。 如果它适用于新的传感器，或者该远的影响、 FRR 或演示文稿攻击检测发生了更改到匹配的引擎，驱动程序必须经历新评审。 

生物特征签名强制日期为 6/1/2017，其后不包含个人简历签名的驱动程序将不会加载和将无法再使用 Windows Hello。

### <a name="step-one-create-a-biometric-driver"></a>步骤一：创建生物识别驱动程序
按照此处的说明创建生物识别驱动程序： https://docs.microsoft.com/windows/desktop/SecBioMet/biometric-service-api-portal

### <a name="step-two-test-your-sensor-and-self-validate"></a>第二步：测试您的传感器和自验证
自助验证传感器和驱动程序以确保其符合 Microsoft 的生物识别要求以及报告指纹安全审阅模板中发现的情况。 可以在连接指纹合作伙伴包中找到有关要求和模板的文档。 如果未对连接访问，请联系 Microsoft 代表联系。

### <a name="step-three-modify-the-driver-configuration-xml-file"></a>第三步：修改驱动程序配置 xml 文件
当提交您的驱动程序，Windows 10，版本 1703年指纹 HLK 测试将检查以确保<vendorCompliance>和<securityReview>标记都包含以下字段：

**bugId**:包含以前批准的安全审核信息或 0，如果提交正在进行全新的安全检查上一 HLK 提交的 ID 号。

**updateExistingSubmission**: true 如果提交可作为更新上一提交已经过安全检查和 false; 否则为。

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
### <a name="step-four-modify-the-driver-configuration-inf"></a>第四步：修改驱动程序配置 inf
生物识别驱动程序包将需要提交到新的开发人员中心门户，以获取所需的 Windows Hello 签名并上传到 WU。 包将需要在要指定正确的适配器 dll 获取数字签名的驱动程序 INF 文件中包含特定属性。 下面的示例演示获取适配器二进制文件和其相关的库中的个人简历签名的格式设置。

例如，如果驱动程序包包含传感器、 引擎和存储适配器，分别名为 sensor.dll、 engine.dll 和 storage.dll 和一个加载 stringparser.dll，然后以获取每个文件，该个人简历签名 INF 文件必须包括以下组件：

```cpp
[SignatureAttributes]
sensor.dll = SignatureAttributes.WindowsHello
engine.dll = SignatureAttributes.WindowsHello
storage.dll = SignatureAttributes.WindowsHello
stringparser.dll = SignatureAttributes.WindowsHello

[SignatureAttributes.WindowsHello]
WindowsHello = true
```

此步骤是确保您的驱动程序收到正确的证书对最重要的。 第三方生物识别适配器的所有文件和加载这些适配器的任何第三方 dll 将需要标有，若要获取生物特征签名时提交给开发人员中心包含在这种方式。

### <a name="step-five-run-the-hlk-test-suite"></a>第五步：运行 HLK 测试套件
HLK 测试将确保上述修改已在步骤 3 和 4 并且如果配置信息不存在将失败。
打包在 HLK studio 最终 HLK 时包括安全审阅模板提交 bug 时补充文件中。

### <a name="step-six-submit-the-driver-package-and-hlk-logs"></a>第六步：提交的驱动程序包和 HLK 日志
打包 HLK 将文件提交给开发人员中心进行审阅。 在 Microsoft 内部，功能团队将在提交内容的通知，到达手动检查进程时。 团队将查看提交的模板，请确保自经过验证的信息满足 Microsoft 的生物识别要求对 HLK 包中。

### <a name="step-seven-wait-for-microsoft-approval-and-signing"></a>第七步：等待 Microsoft 批准和签名
Microsoft 提供符合所有的生物识别要求将审批提交获取生物特征签名不是驱动程序会使用 Windows Hello 的证书。 例如，无法用于签名检查 inf 配置文件中排除文件。 如果此文件加载时 OS 强制签名、 加载将失败，该驱动程序将运行于 Windows Hello。 签名的驱动程序应进行测试，确保其正常集体系统中的 IHV 和 OEM。

### <a name="step-eight-update-an-existing-driver"></a>第 8 步：更新现有的驱动程序
如果需要进行的更新之前已签名的驱动程序，按照在用于更新的驱动程序的驱动程序配置 xml 中的 bugId 和 updateExistingSubmission 字段中填充的步骤 3 下的说明。
如果对 grandfathered 驱动程序进行更新时，应使用相同的步骤。 BugId 字段应设置为 grandfathered 驱动程序的提交 ID 和 updateExistingSubmission 字段应设置为 true。
驱动程序配置 xml 应包含在提交的驱动程序包。

## <a name="related-topics"></a>相关主题


[Windows Hello 面部身份验证](https://docs.microsoft.com/windows-hardware/design/device-experiences/windows-hello-face-authentication)

[Windows Hello](https://docs.microsoft.com/windows-hardware/design/device-experiences/windows-hello)

[生物识别设备设计指南](https://docs.microsoft.com/windows-hardware/drivers/biometric/)


