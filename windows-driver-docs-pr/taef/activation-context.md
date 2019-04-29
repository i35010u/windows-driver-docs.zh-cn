---
title: 激活上下文
description: 激活上下文
ms.assetid: 76584379-2AEF-47e0-B14E-C7698903658F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3388671e65c10e205114934ddb1c2fbb26ce0505
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380501"
---
# <a name="activation-context"></a>激活上下文


TAEF 提供一种机制来指定激活上下文下运行测试。

提供激活上下文，用户可以从各种通过并行程序集在系统中选择某个特定的二进制版本。 所需的激活上下文的清单文件中指定，并且可以通过 ActivationContext 属性传递给 TAEF。 可以指定 ActivationContext 属性，为运行时参数或测试元数据。

## <a name="span-idsampleactivationcontextmanifestfilespanspan-idsampleactivationcontextmanifestfilespanspan-idsampleactivationcontextmanifestfilespansample-activation-context-manifest-file"></a><span id="Sample_Activation_Context_manifest_file"></span><span id="sample_activation_context_manifest_file"></span><span id="SAMPLE_ACTIVATION_CONTEXT_MANIFEST_FILE"></span>示例激活上下文清单文件


```cpp
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">
  <dependency>
    <dependentAssembly>
      <assemblyIdentity type="win32" name="Microsoft.Windows.Common-Controls" version="6.0.0.0" 
        processorArchitecture="*" publicKeyToken="6595b64144ccf1df"/>
    </dependentAssembly>
  </dependency>
</assembly>
```

清单文件**Comctlv6.manifest**的上面所示指定该版本 6 的 comctl32.dll 是要在测试执行期间使用。 若要了解有关清单文件的详细信息，请参阅[清单文件引用](https://msdn.microsoft.com/library/aa375632(VS.85).aspx)

## <a name="span-idspecifyingactivationcontextmanifestatthecommandpromptspanspan-idspecifyingactivationcontextmanifestatthecommandpromptspanspan-idspecifyingactivationcontextmanifestatthecommandpromptspanspecifying-activationcontext-manifest-at-the-command-prompt"></a><span id="Specifying_ActivationContext_manifest_at_the_Command_Prompt"></span><span id="specifying_activationcontext_manifest_at_the_command_prompt"></span><span id="SPECIFYING_ACTIVATIONCONTEXT_MANIFEST_AT_THE_COMMAND_PROMPT"></span>在命令提示符下指定 ActivationContext 清单


``` syntax
te MyUnitTest.dll /ActivationContext:ComctlV6.manifest
```

此命令使用 ComctlV6.manifest 文件中指定的激活上下文的执行 MyUnitTest.dll 中的所有测试

## <a name="span-idspecifyingactivationcontextmanifestastestmetadataspanspan-idspecifyingactivationcontextmanifestastestmetadataspanspan-idspecifyingactivationcontextmanifestastestmetadataspanspecifying-activationcontext-manifest-as-test-metadata"></a><span id="Specifying_ActivationContext_manifest_as_Test_metadata"></span><span id="specifying_activationcontext_manifest_as_test_metadata"></span><span id="SPECIFYING_ACTIVATIONCONTEXT_MANIFEST_AS_TEST_METADATA"></span>作为测试元数据指定 ActivationContext 清单


如果你想要运行特定测试用例在给定的激活上下文，可以通过将 ActivationContext 属性的值设置为你在测试方法上的清单文件来执行的操作。 例如以下测试方法声明运行仅测试方法 MyTestMethod 指定的激活上下文下运行的默认上下文的其他测试时：

```cpp
        BEGIN_TEST_METHOD(MyTestMethod)
            TEST_METHOD_PROPERTY(L"ActivationContext", L"ComctlV6.manifest")
        END_TEST_METHOD()
```

请注意，可以在与其他元数据属性一样的类和程序集级别上设置 ActivationContext 属性。









