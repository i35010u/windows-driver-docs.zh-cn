---
title: 激活上下文
description: 激活上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af7510b5259d9e232cef708d58f0f5b3dae2ca6a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819935"
---
# <a name="activation-context"></a>激活上下文


TAEF 提供了一种机制，用于指定应在其下运行测试的 "激活上下文"。

提供 "激活上下文" 使用户能够从系统中的各种并行程序集选择特定版本二进制文件。 必需的 "激活上下文" 是在清单文件中指定的，并且可以通过 "ActivationContext" 属性传递给 TAEF。 可以将 "ActivationContext" 属性指定为运行时参数或测试元数据。

## <a name="span-idsample_activation_context_manifest_filespanspan-idsample_activation_context_manifest_filespanspan-idsample_activation_context_manifest_filespansample-activation-context-manifest-file"></a><span id="Sample_Activation_Context_manifest_file"></span><span id="sample_activation_context_manifest_file"></span><span id="SAMPLE_ACTIVATION_CONTEXT_MANIFEST_FILE"></span>示例激活上下文清单文件


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

上面所示的清单文件 **"Comctlv6"** 指定在测试执行过程中使用的 comctl32.dll 版本6。 若要了解有关清单文件的详细信息，请参阅 [清单文件引用](/windows/desktop/SbsCs/manifest-files-reference)

## <a name="span-idspecifying_activationcontext_manifest_at_the_command_promptspanspan-idspecifying_activationcontext_manifest_at_the_command_promptspanspan-idspecifying_activationcontext_manifest_at_the_command_promptspanspecifying-activationcontext-manifest-at-the-command-prompt"></a><span id="Specifying_ActivationContext_manifest_at_the_Command_Prompt"></span><span id="specifying_activationcontext_manifest_at_the_command_prompt"></span><span id="SPECIFYING_ACTIVATIONCONTEXT_MANIFEST_AT_THE_COMMAND_PROMPT"></span>在命令提示符处指定 ActivationContext manifest


``` syntax
te MyUnitTest.dll /ActivationContext:ComctlV6.manifest
```

此命令使用 ComctlV6 文件中指定的激活上下文执行 "MyUnitTest.dll" 中的所有测试。

## <a name="span-idspecifying_activationcontext_manifest_as_test_metadataspanspan-idspecifying_activationcontext_manifest_as_test_metadataspanspan-idspecifying_activationcontext_manifest_as_test_metadataspanspecifying-activationcontext-manifest-as-test-metadata"></a><span id="Specifying_ActivationContext_manifest_as_Test_metadata"></span><span id="specifying_activationcontext_manifest_as_test_metadata"></span><span id="SPECIFYING_ACTIVATIONCONTEXT_MANIFEST_AS_TEST_METADATA"></span>将 ActivationContext 清单指定为测试元数据


如果只想在给定激活上下文下运行特定的测试用例，则可以通过将 "ActivationContext" 属性的值设置为测试方法上的清单文件来执行此操作。 例如，下面的测试方法声明在默认上下文下运行其他测试时仅在指定激活上下文下运行测试方法 "MyTestMethod"：

```cpp
        BEGIN_TEST_METHOD(MyTestMethod)
            TEST_METHOD_PROPERTY(L"ActivationContext", L"ComctlV6.manifest")
        END_TEST_METHOD()
```

请注意，"ActivationContext" 属性可以在类和程序集级别上进行设置，如其他元数据属性。
