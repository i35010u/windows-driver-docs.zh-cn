---
title: 运行时参数
description: 运行时参数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b9c4280353dc7019c9f57265bfe5ff1aef281aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816491"
---
# <a name="runtime-parameters"></a>运行时参数


TAEF 提供了一些功能，可用于将运行时参数传递到其执行的测试。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


若要将参数传递给测试，请按以下格式将此参数作为命令行参数提供 te.exe：

``` syntax
Te.exe /p:ParameterName1=ParameterValue1  /p:ParameterName2=ParameterValue2
```

如果参数值包含空格，则用引号将参数名称和参数值括起来：

``` syntax
Te.exe /p:"ParameterName3=The quick brown fox jumps over the lazy dog"
```

## <a name="span-idbuilt-in_parametersspanspan-idbuilt-in_parametersspanspan-idbuilt-in_parametersspanbuilt-in-parameters"></a><span id="Built-in_Parameters"></span><span id="built-in_parameters"></span><span id="BUILT-IN_PARAMETERS"></span>内置参数


TAEF 对以下运行时参数提供内置支持：

-   TestDeploymentDir：测试二进制目录。
-   TestName：当前正在运行的测试的名称。
-   FullTestName：包含变体限定符的测试的完整名称。 这是 TAEF 为 StartGroup 和 EndGroup 记录的名称。
-   TestResult：在此清理函数的作用域内执行的测试的最坏大小写结果。 从最佳到最差：通过、NotRun、跳过、阻止、失败。 例如，如果你的类中至少一个测试已阻止但未测试失败，则结果将被 "阻止" (仅) 的清理函数中可用。

## <a name="span-idaccessing_runtime_parameters_from_testsspanspan-idaccessing_runtime_parameters_from_testsspanspan-idaccessing_runtime_parameters_from_testsspanaccessing-runtime-parameters-from-tests"></a><span id="Accessing_Runtime_Parameters_from_Tests"></span><span id="accessing_runtime_parameters_from_tests"></span><span id="ACCESSING_RUNTIME_PARAMETERS_FROM_TESTS"></span>从测试访问运行时参数


### <a name="span-idnative_testsspanspan-idnative_testsspanspan-idnative_testsspannative-tests"></a><span id="Native_Tests"></span><span id="native_tests"></span><span id="NATIVE_TESTS"></span>本机测试

运行时参数在安装、清理和测试方法中可用。 使用 RuntimeParameters：： TryGetValue API 获取它们：

```cpp
String value;
VERIFY_SUCCEEDED(RuntimeParameters::TryGetValue(L"ParameterName3", value));
```

注意：若要从测试请求运行时参数，需要链接到 Te 类库。

### <a name="span-idmanaged_testsspanspan-idmanaged_testsspanspan-idmanaged_testsspanmanaged-tests"></a><span id="Managed_Tests"></span><span id="managed_tests"></span><span id="MANAGED_TESTS"></span>托管测试

运行时参数在安装和测试方法中可用。 若要获取它们，请使用类的 TestContext 属性。

示例 (类或程序集设置) ：

```cpp
[ClassInitialize]

public static void ClassSetup(TestContext context)
{
    String parameterName3  = context.Properties["ParameterName3"];

}
```

同样，从测试：

```cpp
[TestMethod]

public void VerifyRuntimeParametersTest()
{
    String parameterName3  = m_testContext.Properties["ParameterName3"].ToString());
}

// Note, that to work with runtime parameters, as well as with your tests,  you need to add
// definition of test context property to your class

private TestContext m_testContext;

public TestContext TestContext
{
    get { return m_testContext; }
    set { m_testContext = value; }
}
```

### <a name="span-idscript_testsspanspan-idscript_testsspanspan-idscript_testsspanscript-tests"></a><span id="Script_Tests"></span><span id="script_tests"></span><span id="SCRIPT_TESTS"></span>脚本测试

运行时参数在安装、清理和测试方法中可用。 若要检索运行时参数，请从 Te 定义并实例化 RuntimeParameters 对象：

```cpp
<object id="RuntimeParameters" progid="Te.Common.RuntimeParameters" />
```

实例化 RuntimeParameters 对象后，可以使用 RuntimeParameters ( " &lt; 运行时参数名称 &gt; " ) 方法来查询是否提供了运行时参数并可用于测试。 如果它返回 true，则可以使用 RuntimeParameters ( " &lt; 运行时参数名称 &gt; " ) 检索它。 请注意，如果运行时参数不可用，则 RuntimeParameters ( ... ) 会引发。 下面的示例来自我们的 VBScript 示例：

```cpp
       <script language="VBScript">
            <![CDATA[
                Function TestOne()
                    dim param
                    param = "No runtime param"
                    If RuntimeParameters.Contains("param") Then
                         param = RuntimeParameters.GetValue("param")
                    End If
                    Log.Comment("Param is " + param)

                    dim testDir
                    If RuntimeParameters.Contains("testDir") Then
                        testDir = RuntimeParameters.GetValue("TestDir")
                    End If
                    Log.Comment("The test harness is running in " + testDir)
                End Function
            ]] >
        </script>
```

 

 





