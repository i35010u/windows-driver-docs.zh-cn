---
title: 运行时参数
description: 运行时参数
ms.assetid: 5CE5D2C3-F967-4318-B799-38CE8E8B15A6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed22b05a45fc5e440ba36f9ef99b9ef375335d52
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324728"
---
# <a name="runtime-parameters"></a>运行时参数


TAEF 提供了用于将运行时参数传递给它的执行的测试功能。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


若要将参数传递给你的测试，作为以下窗体中的命令行参数提供此参数为 te.exe:

``` syntax
Te.exe /p:ParameterName1=ParameterValue1  /p:ParameterName2=ParameterValue2
```

如果参数值包含空格，加上双引号参数名称和参数值：

``` syntax
Te.exe /p:"ParameterName3=The quick brown fox jumps over the lazy dog"
```

## <a name="span-idbuilt-inparametersspanspan-idbuilt-inparametersspanspan-idbuilt-inparametersspanbuilt-in-parameters"></a><span id="Built-in_Parameters"></span><span id="built-in_parameters"></span><span id="BUILT-IN_PARAMETERS"></span>内置参数


TAEF 具有对以下运行时参数的内置支持：

-   TestDeploymentDir:测试二进制目录。
-   测试名称：当前运行的测试的名称。
-   FullTestName:测试包括变体限定符的全名。 这是 TAEF StartGroup 和 EndGroup 记录该名称。
-   TestResult:此清理函数的作用域内执行的测试的最坏的情况聚合结果。 按顺序从最好到最差：传递未运行，跳过，已阻止、 失败。 例如，如果至少一个测试类中的被阻止，但没有任何测试失败，结果将被"阻止"（只有在清除函数中）。

## <a name="span-idaccessingruntimeparametersfromtestsspanspan-idaccessingruntimeparametersfromtestsspanspan-idaccessingruntimeparametersfromtestsspanaccessing-runtime-parameters-from-tests"></a><span id="Accessing_Runtime_Parameters_from_Tests"></span><span id="accessing_runtime_parameters_from_tests"></span><span id="ACCESSING_RUNTIME_PARAMETERS_FROM_TESTS"></span>从测试访问运行时参数


### <a name="span-idnativetestsspanspan-idnativetestsspanspan-idnativetestsspannative-tests"></a><span id="Native_Tests"></span><span id="native_tests"></span><span id="NATIVE_TESTS"></span>本机测试

安装程序、 清理和测试方法中提供了运行时参数。 使用 RuntimeParameters::TryGetValue API 来获取它们：

```cpp
String value;
VERIFY_SUCCEEDED(RuntimeParameters::TryGetValue(L"ParameterName3", value));
```

注意：若要从你的测试请求运行时参数，需要针对 Te.Common.lib 库进行链接。

### <a name="span-idmanagedtestsspanspan-idmanagedtestsspanspan-idmanagedtestsspanmanaged-tests"></a><span id="Managed_Tests"></span><span id="managed_tests"></span><span id="MANAGED_TESTS"></span>托管的测试

安装和测试方法中提供了运行时参数。 若要获取它们，请使用您的类的 TestContext 属性。

示例 （类或程序集的安装程序）：

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

### <a name="span-idscripttestsspanspan-idscripttestsspanspan-idscripttestsspanscript-tests"></a><span id="Script_Tests"></span><span id="script_tests"></span><span id="SCRIPT_TESTS"></span>脚本的测试

安装程序、 清理和测试方法中提供了运行时参数。 若要检索运行时参数，定义并实例化从 Te.Common RuntimeParameters 对象：

```cpp
<object id="RuntimeParameters" progid="Te.Common.RuntimeParameters" />
```

一旦 RuntimeParameters 对象被实例化，可以使用 RuntimeParameters.Contains ("&lt;运行时参数名称&gt;") 查询，如果运行时参数提供，它是可用于测试的方法。 如果它返回 true，则可以使用 RuntimeParameters.GetValue ("&lt;运行时参数名称&gt;") 来对其进行检索。 请注意，如果未提供运行时参数，将引发 RuntimeParameters.GetValue(...)。 下面的示例是从我们的 VBScript 示例：

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

 

 





