---
title: 验证框架
description: 验证框架
ms.assetid: A954B5E2-E3C7-4021-BE53-AE1257139607
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a9aaf7a41b6a6d0f1c137c2c456cf0283d22a98
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383033"
---
# <a name="verify-framework"></a>验证框架


若要使编写测试更容易，TAEF，提供了"验证"框架，利用[WexLogger](wexlogger.md)来报告使用极少量的代码的详细的日志。 验证框架可帮助测试，以提供结构化的日志输出-它将输出登录成功，如果给定的验证成功，并且它将输出的详细的信息，如果验证失败。

## <a name="span-idcplusplusspanspan-idcplusplusspanusing-verify-from-c"></a><span id="cplusplus"></span><span id="CPLUSPLUS"></span>从使用验证C++


验证 API 显示在C++为一系列"Verify.h"标头文件中定义的宏 (注意：不需要显式包括 Verify.h，应包括包含全部所需标记的"WexTestClass.h"C++测试和与验证和 WexLogger API 进行交互)。

以下验证宏是可用于本机C++测试：

| 宏                                                                                     | 功能                                                                                                                                                                                                         |
|-------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 验证\_都\_相等 (expected，实际\[可选消息\])                                | 验证两个指定的对象相等。 如果提供，还记录自定义消息。                                                                                                                                |
| 验证\_都\_不\_相等 (expected，实际\[可选消息\])                           | 验证两个指定的对象不相等。 如果提供，还记录自定义消息。                                                                                                                            |
| 验证是否\_IS\_GREATER\_个 (expectedGreater，expectedLess，\[可选消息\])            | 验证第一个参数大于第二个参数。 如果提供，还记录自定义消息。                                                                                                       |
| 验证是否\_IS\_GREATER\_个\_或者\_相等 (expectedGreater，expectedLess，\[可选消息\]) | 验证第一个参数大于或等于第二个参数。 如果提供，还记录自定义消息。                                                                                           |
| 验证是否\_IS\_较少\_个 (expectedLess，expectedGreater，\[可选消息\])               | 验证第一个参数小于第二个参数。 如果提供，还记录自定义消息。                                                                                                          |
| 验证是否\_IS\_较少\_个\_或者\_相等 (expectedLess，expectedGreater，\[可选消息\])    | 验证第一个参数小于或等于第二个参数。 如果提供，还记录自定义消息。                                                                                              |
| 验证\_都\_SAME (expected，实际\[可选消息\])                                 | 验证指定的两个参数引用同一个对象。 如果提供，还记录自定义消息。                                                                                                          |
| 验证\_都\_不\_SAME (expected，实际\[可选消息\])                            | 验证指定的两个参数执行引用同一对象。 如果提供，还记录自定义消息。                                                                                                   |
| 验证是否\_失败 (\[可选消息\])                                                       | 失败且不检查任何条件。 如果提供，还记录自定义消息。                                                                                                                                        |
| 验证是否\_IS\_，则返回 TRUE (条件\[可选消息\])                                         | 验证指定的布尔值为 true。 调用验证\_IS\_TRUE （!!\_\_条件)，或验证\_WIN32\_BOOL\_SUCCEEDED (\_\_条件) 来测试 Win32 BOOL。 如果提供，还记录自定义消息。                      |
| 验证是否\_IS\_FALSE (条件\[可选消息\])                                        | 验证指定的布尔值为 false。 调用验证\_IS\_FALSE （!!\_\_条件)，或验证\_WIN32\_BOOL\_失败 (\_\_条件) 来测试 Win32 BOOL。 如果提供，还记录自定义消息。                       |
| 验证是否\_IS\_NULL (对象\[可选消息\])                                            | 验证指定的参数为 NULL。 如果提供，还记录自定义消息。                                                                                                                                |
| 验证是否\_IS\_不\_NULL (对象\[可选消息\])                                       | 验证指定的参数不为 NULL。 如果提供，还记录自定义消息。                                                                                                                            |
| 验证是否\_SUCCEEDED (hresult，\[可选消息\])                                          | 验证指定的 HRESULT 成功。 如果提供，还记录自定义消息。                                                                                                                            |
| 验证是否\_SUCCEEDED\_返回 (hresult，\[可选消息\])                                  | 验证指定的 HRESULT 成功并返回 HRESULT，它已传递到宏。 如果提供，还记录自定义消息。                                                                     |
| 验证是否\_失败 (hresult，\[可选消息\])                                             | 验证指定的 HRESULT 不成功。 如果提供，还记录自定义消息。                                                                                                                        |
| 验证是否\_失败\_返回 (hresult，\[可选消息\])                                     | 验证指定的 HRESULT 未成功并返回 HRESULT，它已传递到宏。 如果提供，还记录自定义消息。                                                                 |
| 验证是否\_将引发 (操作、 异常\[可选消息\])                                | 验证指定的操作将引发给定的异常类型。 如果提供，还记录自定义消息。                                                                                                        |
| 验证是否\_否\_引发 (操作\[可选消息\])                                        | 验证指定的操作不会引发异常。 如果提供，还记录自定义消息。                                                                                                            |
| 验证是否\_WIN32\_SUCCEEDED (win32Result，\[可选消息\])                               | 验证指定的 Win32 结果已成功。 如果提供，还记录自定义消息。                                                                                                                           |
| 验证是否\_WIN32\_SUCCEEDED\_返回 (win32Result，\[可选消息\])                       | 验证指定的 Win32 结果成功并返回 long 类型的值已传递到宏。 如果提供，还记录自定义消息。                                                                       |
| 验证是否\_WIN32\_失败 (win32Result，\[可选消息\])                                  | 验证指定的 Win32 结果失败。 如果提供，还记录自定义消息。                                                                                                                              |
| 验证是否\_WIN32\_FAILED\_返回 (win32Result，\[可选消息\])                          | 验证指定的 Win32 结果失败并返回 long 类型的值已传递到宏。 如果提供，还记录自定义消息。                                                                          |
| 验证是否\_WIN32\_BOOL\_SUCCEEDED (win32Bool，\[可选消息\])                           | 验证指定的 Win32 BOOL 成功 (！ = FALSE)。 如果验证失败，将记录 getlasterror （） 的结果。 如果提供，还记录自定义消息。                                                     |
| 验证是否\_WIN32\_BOOL\_SUCCEEDED\_返回 (win32Bool，\[可选消息\])                   | 验证指定的 Win32 BOOL 成功 (！ = FALSE)，并返回已传递到宏的布尔值。 如果验证失败，将记录 getlasterror （） 的结果。 如果提供，还记录自定义消息。 |
| 验证是否\_WIN32\_BOOL\_失败 (win32Bool，\[可选消息\])                              | 验证指定的 Win32 BOOL 失败 （= = FALSE）。 不会记录 getlasterror （） 的结果。 如果提供，还记录自定义消息。                                                                          |
| 验证是否\_WIN32\_BOOL\_FAILED\_返回 (win32Bool，\[可选消息\])                      | 验证指定的 Win32 BOOL 失败 （= = FALSE），并返回已传递到宏的布尔值。 不会记录 getlasterror （） 的结果。 如果提供，还记录自定义消息。                      |



### <a name="span-idexceptioncplusplusspanspan-idexceptioncplusplusspanexception-based-verify-usage"></a><span id="exception_cplusplus"></span><span id="EXCEPTION_CPLUSPLUS"></span>基于异常验证使用情况

如果你的源代码编译使用C++启用的异常 (通过指定"/ EHsc"命令行开关或"使用\_本机\_EH = 1" 宏源文件中的)，验证宏将默认为日志记录失败，错误遵循通过引发一个本机C++异常。 引发的异常**WEX::TestExecution::VerifyFailureException**。 不需要捕获此异常-TAEF 框架将为你捕获并转到下一步的测试用例。

（可选） 如果你想要执行一系列验证中的行，而不是无需在测试时中止第一次的验证失败，则可以使用**DisableVerifyExceptions**类。 对象的生存期控制异常处于禁用状态的时间量。

```cpp
if (NULL != m_key)
{
    DisableVerifyExceptions disable;
    VERIFY_WIN32_SUCCEEDED(::RegDeleteKey(HKEY_CURRENT_USER, zTempName));
    VERIFY_WIN32_SUCCEEDED(::RegCloseKey(m_key));
}
```

异常仅在禁用在上面的示例中，"如果 (NULL ！ = m\_密钥)"块中，并且如果第一个验证调用失败，仍进行第二次验证调用。

**DisableVerifyExceptions**类是引用计数，并且还在每个线程进行函数。

### <a name="span-idnonexceptioncplusplusspanspan-idnonexceptioncplusplusspannon-exception-based-verify-usage"></a><span id="nonexception_cplusplus"></span><span id="NONEXCEPTION_CPLUSPLUS"></span>非基于异常验证使用情况

如果你的源代码***不***编译的C++启用的异常，验证宏将不会引发一个本机C++当验证失败。 此外，如果你的源代码编译使用C++启用的例外，但想要禁用验证例外情况，只需\#定义无\_验证\_之前包括"WexTestClass.h"的异常。

在此模型中，您必须执行一系列嵌套如果语句以便控制流的测试用例中，而是依赖于比C++异常。

```cpp
if (VERIFY_WIN32_SUCCEEDED(::RegDeleteKey(HKEY_CURRENT_USER, zTempName)))
{
    ...
}
```

### <a name="span-idoutsettingscplusplusspanspan-idoutsettingscplusplusspanverify-output-settings"></a><span id="outsettings_cplusplus"></span><span id="OUTSETTINGS_CPLUSPLUS"></span>验证输出设置

如果你想要自定义验证 Api 生成的输出，则可以使用**SetVerifyOutput**类。 对象的生存期控制的输出设置的时间量。 **SetVerifyOutput**类是引用计数，并在每个线程进行函数。

```cpp
if (NULL != m_key)
{
    SetVerifyOutput verifySettings(VerifyOutputSettings::LogOnlyFailures);
    VERIFY_IS_TRUE(true, L"Should NOT log a comment");
    VERIFY_IS_TRUE(false, L"Should log an error");
}
VERIFY_IS_TRUE(true, L"Should log a comment");
```

在上面的示例中，指定的设置仅适用于在所做的调用"如果 (NULL ！ = m\_密钥)"块，并*仅*将记录失败的验证调用。 但是，即使它成功，则将记录第三个验证调用。 这是由于 SetVerifyOutput 类已超出范围。

用于设置验证输出存在以下选项：

<span id="VerifyOutputSettings__LogOnlyFailures_"></span><span id="verifyoutputsettings__logonlyfailures_"></span><span id="VERIFYOUTPUTSETTINGS__LOGONLYFAILURES_"></span>VerifyOutputSettings::LogOnlyFailures   
仅失败的验证的调用将记入日志;所有成功的调用将被忽略。

<span id="VerifyOutputSettings__LogFailuresAsBlocked_"></span><span id="verifyoutputsettings__logfailuresasblocked_"></span><span id="VERIFYOUTPUTSETTINGS__LOGFAILURESASBLOCKED_"></span>VerifyOutputSettings::LogFailuresAsBlocked   
为受阻而不是日志记录错误记录所有失败。

<span id="VerifyOutputSettings__LogFailuresAsWarnings_"></span><span id="verifyoutputsettings__logfailuresaswarnings_"></span><span id="VERIFYOUTPUTSETTINGS__LOGFAILURESASWARNINGS_"></span>VerifyOutputSettings::LogFailuresAsWarnings   
记录为警告而不是日志记录错误的所有失败。

<span id="VerifyOutputSettings__LogValuesOnSuccess_"></span><span id="verifyoutputsettings__logvaluesonsuccess_"></span><span id="VERIFYOUTPUTSETTINGS__LOGVALUESONSUCCESS_"></span>VerifyOutputSettings::LogValuesOnSuccess   
记录验证调用成功，即使在中，传递的参数值。

验证是否可以输出设置或必须一起启用多个设置：

```cpp
SetVerifyOutput verifySettings(VerifyOutputSettings::LogOnlyFailures | VerifyOutputSettings::LogFailuresAsBlocked);
```

### <a name="span-idoutcustomcplusplusspanspan-idoutcustomcplusplusspanproviding-value-output-for-custom-types"></a><span id="outcustom_cplusplus"></span><span id="OUTCUSTOM_CPLUSPLUS"></span>提供为自定义类型的值输出

C++验证框架提供的功能，以生成的任何自定义类型的详细的输出。 要执行此操作，其中一个必须实现的专用化**WEX::TestExecution::VerifyOutputTraits**类模板。

**WEX::TestExecution::VerifyOutputTraits**类模板专用化必须存在于**WEX::TestExecution**命名空间。 它还应提供名为的公共静态方法**ToString**，它将引用您的类，并返回**WEX::Common::NoThrowString**包含其值的字符串表示形式.

```cpp
    class MyClass
    {
    public:
        MyClass(int value)
            : m_myValue(value)
        {
        }

        int GetValue()
        {
            return m_myValue;
        }

    private:
        int m_myValue;
    }

    namespace WEX { namespace TestExecution
    {
        template <>
        class VerifyOutputTraits<MyClass>
        {
        public:
            static WEX::Common::NoThrowString ToString(const MyClass& myClass)
            {
                return WEX::Common::NoThrowString().Format(L"%d", myClass.GetValue());
            }
        };
    }}
```

### <a name="span-idcomparatorscplusplusspanspan-idcomparatorscplusplusspanproviding-comparators-for-custom-types"></a><span id="comparators_cplusplus"></span><span id="COMPARATORS_CPLUSPLUS"></span>为自定义类型提供比较运算符

C++验证框架提供的功能来定义未实现相应的运算符重载的自定义类型的比较运算符 (运算符 =、 运算符&lt;等)。 要执行此操作，其中一个必须实现的专用化**WEX::TestExecution::VerifyCompareTraits**类模板。

**WEX::TestExecution::VerifyCompareTraits**类模板专用化必须存在于**WEX::TestExecution**命名空间。 它还应提供一种公共静态方法调用**AreEqual**， **AreSame**， **IsLessThan**， **IsGreaterThan**，和**IsNull**。

```cpp
    class MyClass
    {
    public:
        MyClass(int value)
            : m_myValue(value)
        {
        }

        int GetValue()
        {
            return m_myValue;
        }

    private:
        int m_myValue;
    }

    namespace WEX { namespace TestExecution
    {
        template <>
        class VerifyCompareTraits<MyClass, MyClass>
        {
        public:
            static bool AreEqual(const MyClass& expected, const MyClass& actual)
            {
                return expected.GetValue() == actual.GetValue();
            }

            static bool AreSame(const MyClass& expected, const MyClass& actual)
            {
                return &expected == &actual;
            }

            static bool IsLessThan(const MyClass& expectedLess, const MyClass& expectedGreater)
            {
                return (expectedLess.GetValue() < expectedGreater.GetValue());
            }

            static bool IsGreaterThan(const MyClass& expectedGreater, const MyClass& expectedLess)
            {
                return (expectedGreater.GetValue() > expectedLess.GetValue());
            }

            static bool IsNull(const MyClass& object)
            {
                return object.GetValue() == 0;
            }
        };
    }}
```

## <a name="span-idcsharpspanspan-idcsharpspanusing-verify-from-c"></a><span id="csharp"></span><span id="CSHARP"></span>从使用验证C#


C#验证使用情况是类似于C++。 但是，通过提供**WEX。TestExecution.Verify**类，该类是位于**Te.Managed.dll**。

下面的验证方法是可用于C#测试：

| 宏                                                                                       | 功能                                                                                                                                                                       |
|---------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AreEqual(object expected, object actual)                                                    | 验证两个指定的对象相等。                                                                                                                                      |
| AreEqual （应为对象，对象实际，字符串消息）                                    | 验证两个指定的对象相等，则记录上验证成功或失败的自定义消息。                                                                            |
| AreEqual&lt;T&gt;(T expected，实际的 T)                                                     | 验证两个指定的对象相等。                                                                                                                                      |
| AreEqual&lt;T&gt;（应为 T，T 实际，字符串消息）                                     | 验证两个指定的对象相等，则记录上验证成功或失败的自定义消息。                                                                            |
| AreNotEqual(object expected, object actual)                                                 | 验证两个指定的对象不相等。                                                                                                                                  |
| AreNotEqual(object expected, object actual, string message)                                 | 验证两个指定的对象不相等;记录上验证成功或失败的自定义消息。                                                                        |
| AreNotEqual&lt;T&gt;(T expected，实际的 T)                                                  | 验证两个指定的对象不相等。                                                                                                                                  |
| AreNotEqual&lt;T&gt;（应为 T，T 实际，字符串消息）                                  | 验证两个指定的对象不相等;记录上验证成功或失败的自定义消息。                                                                        |
| AreSame （应为对象、 对象实际）                                                     | 验证指定的两个参数引用同一个对象。                                                                                                                |
| AreSame （应为对象，对象实际，字符串消息）                                     | 验证指定的两个参数引用同一个对象;记录上验证成功或失败的自定义消息。                                                      |
| AreNotSame(object expected, object actual)                                                  | 验证指定的两个参数执行引用同一对象。                                                                                                         |
| AreNotSame （应为对象，对象实际，字符串消息）                                  | 验证指定的两个参数不会对同一对象; 请参阅记录上验证成功或失败的自定义消息。                                               |
| IsGreaterThan （IComparable expectedGreater、 IComparable expectedLess）                        | 验证第一个参数大于第二个参数。                                                                                                             |
| IsGreaterThan （IComparable expectedGreater，IComparable expectedLess，字符串消息）        | 验证第一个参数大于第二个参数;记录上验证成功或失败的自定义消息。                                                   |
| IsGreaterThanOrEqual （IComparable expectedGreater、 IComparable expectedLess）                 | 验证第一个参数大于或等于第二个参数。                                                                                                 |
| IsGreaterThanOrEqual （IComparable expectedGreater，IComparable expectedLess，字符串消息） | 验证第一个参数大于或等于第二个参数;记录上验证成功或失败的自定义消息。                                       |
| IsLessThan （IComparable expectedLess、 IComparable expectedGreater）                           | 验证第一个参数小于第二个参数。                                                                                                                |
| IsLessThan （IComparable expectedLess，IComparable expectedGreater，字符串消息）           | 验证第一个参数小于第二个参数;记录上验证成功或失败的自定义消息。                                                      |
| IsLessThanOrEqual （IComparable expectedLess、 IComparable expectedGreater）                    | 验证第一个参数小于或等于第二个参数。                                                                                                    |
| IsLessThanOrEqual （IComparable expectedLess，IComparable expectedGreater，字符串消息）    | 验证第一个参数小于或等于第二个参数;记录上验证成功或失败的自定义消息。                                          |
| 失败 （字符串消息）                                                                        | 失败且不检查任何条件。                                                                                                                                              |
| IsTrue （布尔值条件）                                                                      | 验证指定的条件为 true。                                                                                                                                      |
| IsTrue （布尔值条件，字符串消息）                                                      | 验证指定的条件为 true;记录上验证成功或失败的自定义消息。                                                                            |
| IsFalse （布尔值条件）                                                                     | 验证指定的条件为 false。                                                                                                                                     |
| IsFalse （布尔值条件，字符串消息）                                                     | 验证指定的条件为 false;记录上验证成功或失败的自定义消息。                                                                           |
| IsNull(object obj)                                                                          | 验证指定的参数为 NULL。                                                                                                                                      |
| IsNull （对象 obj、 字符串消息）                                                          | 验证指定的参数为 NULL。记录上验证成功或失败的自定义消息。                                                                            |
| IsNotNull(object obj)                                                                       | 验证指定的参数不为 NULL。                                                                                                                                  |
| IsNotNull(object obj, string message)                                                       | 验证指定的参数不为 NULL;记录上验证成功或失败的自定义消息。                                                                        |
| 将引发&lt;T&gt;（VerifyOperation 操作）                                                  | 验证指定的操作将引发给定的异常类型。 此外会返回用于进一步调查的异常。                                                           |
| 将引发&lt;T&gt;（VerifyOperation 操作，字符串消息）                                  | 验证指定的操作将引发给定的异常类型;记录上验证成功或失败的自定义消息。 此外会返回用于进一步调查的异常。 |
| NoThrow(VerifyOperation operation)                                                          | 验证指定的操作不会引发异常。                                                                                                                  |
| NoThrow(VerifyOperation operation, string message)                                          | 验证指定的操作不会引发异常;记录上验证成功或失败的自定义消息。                                                        |



### <a name="span-idexceptioncsharpspanspan-idexceptioncsharpspanexception-based-verify-usage"></a><span id="exception_csharp"></span><span id="EXCEPTION_CSHARP"></span>基于异常验证使用情况

验证失败时出现在C#的测试用例，将错误写入到记录器，和一个**WEX。TestExecution.VerifyFailureException**引发。 就像本机一样C++模型中，您不需要担心如何捕获这些异常。 TAEF 框架将为您捕获，并转到下一步的测试用例。

（可选） 如果你想要执行一系列验证中的行，而不是无需在测试时中止第一次的验证失败，则可以使用**DisableVerifyExceptions**类。 对象的生存期控制异常处于禁用状态的时间量。 **DisableVerifyExceptions**类是引用计数，并在每个线程进行函数。

```cpp
using (new DisableVerifyExceptions())
{
    Verify.AreSame(item1, item2);
    Verify.AreEqual(item1, item2);
}
```

在上面的示例中，如果第一个验证调用失败，第二个验证仍进行调用。

或者，设置可以实现相同的结果**Verify.DisableVerifyExceptions = true**之前的验证操作，例如如下所示的示例。

```cpp
Verify.DisableVerifyExceptions = true;
try
{
    Verify.AreSame(item1, item2);
    Verify.AreEqual(item1, item2);
}
finally
{
    Verify.DisableVerifyExceptions = false;
}
```

请注意，即使此类选项可用，将 DisableVerifyExeptions 声明中使用的对象为块仍是建议的选项。

如果你想要打开异常对话框 (Ctrl + Alt + E) 发生验证错误时停止调试器中，单击添加，从下拉列表中选择"公共语言运行时异常"放"WEX。TestExecution.VerifyFailureException"在名称字段中。

### <a name="span-idoutsettingscsharpspanspan-idoutsettingscsharpspanverify-output-settings"></a><span id="outsettings_csharp"></span><span id="OUTSETTINGS_CSHARP"></span>验证输出设置

如果你想要自定义验证 Api 生成的输出，则可以使用**SetVerifyOutput**类。 对象的生存期控制的输出设置的时间量。 **SetVerifyOutput**类是引用计数，并在每个线程进行函数。

```cpp
using (new SetVerifyOutput(VerifyOutputSettings.LogOnlyFailures))
{
    Log.Comment("Only the following error should be logged:");
    Verify.IsTrue(true, "Should NOT log a comment");
    Verify.IsTrue(false, "Should log an error");
}
Verify.IsTrue(true, "Should log a comment");
```

由于它是在使用的唯一调用，则应记录在上面的示例中，只有第二个验证对调用块。 但是，第三个验证调用*将*即使它成功记录。 这是由于 SetVerifyOutput 类已超出范围。

或者，设置可以实现相同的结果**Verify.OutputSettings = VerifyOutputSettings.LogOnlyFailures**之前的验证操作，例如如下所示的示例。

```cpp
Verify.OutputSettings = VerifyOutputSettings.LogFailuresAsWarnings
try
{
    Verify.AreSame(item1, item2);
    Verify.AreEqual(item1, item2);
}
finally
{
    Verify.OutputSettings = VerifyOutputSettings.None;
}
```

请注意，即使此类选项可用，将 SetVerifyOutput 声明中使用的对象为块仍是建议的选项。

用于设置验证输出存在以下选项：

<span id="verifyoutputsettings.logonlyfailures_"></span><span id="VERIFYOUTPUTSETTINGS.LOGONLYFAILURES_"></span>VerifyOutputSettings.LogOnlyFailures   
仅失败的验证的调用将记入日志;所有成功的调用将被忽略。

<span id="verifyoutputsettings.logfailuresasblocked_"></span><span id="VERIFYOUTPUTSETTINGS.LOGFAILURESASBLOCKED_"></span>VerifyOutputSettings.LogFailuresAsBlocked   
为受阻而不是日志记录错误记录所有失败。

<span id="verifyoutputsettings.logfailuresaswarnings_"></span><span id="VERIFYOUTPUTSETTINGS.LOGFAILURESASWARNINGS_"></span>VerifyOutputSettings.LogFailuresAsWarnings   
记录为警告而不是日志记录错误的所有失败。

验证是否可以输出设置或必须一起启用多个设置：

```cpp
using (new SetVerifyOutput(VerifyOutputSettings.LogFailuresAsBlocked | VerifyOutputSettings.LogOnlyFailures))
{
...
}
```

## <a name="span-idscriptspanspan-idscriptspanusing-verify-from-script"></a><span id="script"></span><span id="SCRIPT"></span>使用脚本验证


验证 API 还可以找出脚本语言，遵循相同的使用情况模式为C++和C#。

### <a name="span-idinstallationspanspan-idinstallationspanspan-idinstallationspaninstallation"></a><span id="Installation"></span><span id="installation"></span><span id="INSTALLATION"></span>安装

使用可编写脚本验证 API 的时从 TAEF 测试方法中没有安装必要-使用免注册 COM 注册所需的 API。 若要使用外部 TAEF 测试中的可编写脚本 API 方法 （外部 TAEF，或在子进程中） 只需注册 Te.Common.dll 二进制文件使用 regsvr32 从提升的命令提示符;例如：

``` syntax
regsvr32 Te.Common.dll
```

在部署 TAEF 实验室执行使用部署文件时，会自动注册 Te.Common.dll。

### <a name="span-idusagescriptspanspan-idusagescriptspanusage"></a><span id="usage_script"></span><span id="USAGE_SCRIPT"></span>使用情况

可编写脚本验证 API 的显示通过 TE.Common.Verify COM 类-只需实例化，它的类和调用方法验证类将自动使用 WEXLogger 编写通过和失败验证到日志。

```cpp
1   <?xml version="1.0" ?>
2   <?component error="false" debug="false"?>
3   <package>
4     <component id="Example">
5       <object id="Log" progid="Wex.Logger.Log" />
6       <object id="Verify" progid="Te.Common.Verify" />
7       <reference guid="e65ef678-a232-42a7-8a36-63108d719f31" version="1.0"/>
8       <reference guid="f8bb9db9-e54e-4555-b3e5-e3ddf2fef401" version="1.0"/>
9
10      <public>
11        <method name="HelloWorld"/>
12      </public>
13
14      <script language="JScript">
15          function HelloWorld() {
16              Verify.IsTrue(true);
17              Verify.IsFalse(false);
18          }
19      </script>
20    </component>
21  </package>
```

此示例使用一个 hello World 的方法定义 TAEF 脚本测试类。 第 6 行中使用 object 元素来在全局范围中定义验证变量。 第 8 行使用引用元素到脚本; 全局作用域包括从指定的类型库 （在此情况下，Te.Common.dll 的类型库） 的所有常量在这种情况下，它将添加 VerifySettings 常量。 第 16 和 17 行显示只需使用了验证 API。 执行时，该示例将生成以下输出：

``` syntax
Test Authoring and Execution Framework v2.7 Build 6.2.7922.0 (fbl_esc_end_dev(mschofie).110202-1000) For x86

StartGroup: Example::HelloWorld
Verify: IsTrue
Verify: IsFalse
EndGroup: Example::HelloWorld [Passed]

Summary: Total=1, Passed=1, Failed=0, Blocked=0, Not Run=0, Skipped=0
```

### <a name="span-idapiscriptspanspan-idapiscriptspanscriptable-verify-api"></a><span id="api_script"></span><span id="API_SCRIPT"></span>可编写脚本验证 API

可编写脚本的验证 API 上的验证的方法如下所示：

| 方法                                                                                | 功能                                                                                                                                                                                                                                                                                                                  |
|---------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| bool Verify.AreEqual (expected，实际\[可选消息\])                          | 验证两个值相等。 如果 VerifySettings\_CoerceTypes' 设置为启用，此方法使用 JScript 定义的相等性，如果 VerifySettings\_CoerceTypes' 设置不启用，该方法使用标识的 JScript 定义。 **VerifySettings\_CoerceTypes' 处于打开状态。**     |
| bool Verify.AreNotEqual (expected，实际\[可选消息\])                       | 验证两个值不相等。 如果 VerifySettings\_CoerceTypes' 设置为启用，此方法使用 JScript 定义的相等性，如果 VerifySettings\_CoerceTypes' 设置不启用，该方法使用标识的 JScript 定义。 **VerifySettings\_CoerceTypes' 处于打开状态。** |
| bool Verify.IsGreaterThan (expectedGreater，expectedLess，\[可选消息\])        | 验证的第一个值大于第二个。                                                                                                                                                                                                                                                                      |
| bool Verify.IsGreaterThanOrEqual (expectedGreater，expectedLess，\[可选消息\]) | 验证的第一个值大于或等于第二个。                                                                                                                                                                                                                                                          |
| bool Verify.IsLessThan (expectedLess，expectedGreater，\[可选消息\])           | 验证第一个值小于第二个。                                                                                                                                                                                                                                                                         |
| bool Verify.IsLessThanOrEqual (expectedLess，expectedGreater，\[可选消息\])    | 验证的第一个值小于或等于第二个。                                                                                                                                                                                                                                                             |
| bool Verify.AreSame (expected，实际\[可选消息\])                           | 验证值相同。                                                                                                                                                                                                                                                                                         |
| bool Verify.AreNotSame (expected，实际\[可选消息\])                        | 验证的值不是相同。                                                                                                                                                                                                                                                                                     |
| bool Verify.Fail (\[可选消息\])                                                | 失败且不检查条件。                                                                                                                                                                                                                                                                                             |
| bool Verify.IsTrue (表达式中，\[可选消息\])                                  | 验证给定的表达式计算结果为 true。                                                                                                                                                                                                                                                                          |
| bool Verify.IsFalse (表达式中，\[可选消息\])                                 | 验证给定的表达式计算结果为 false。                                                                                                                                                                                                                                                                         |
| bool Verify.IsNull (预期\[可选消息\])                                    | 验证给定的值是 null。                                                                                                                                                                                                                                                                                       |
| bool Verify.IsNotNull (预期\[可选消息\])                                 | 验证给定的值不是 null。                                                                                                                                                                                                                                                                                   |
| bool Verify.Throws (函数\[可选消息\])                                    | 验证给定的函数将引发和异常。                                                                                                                                                                                                                                                                         |
| bool Verify.NoThrow (函数\[可选消息\])                                   | 验证给定的函数不会引发和异常。                                                                                                                                                                                                                                                                 |



控制设置的验证类中有两种方法：

| 方法                                  | 功能                                         |
|-----------------------------------------|-------------------------------------------------------|
| 对象 Verify.EnableSettings(settings)  | 指定将启用设置标志。  |
| 对象 Verify.DisableSettings(settings) | 指定设置标志将被禁用。 |



传递给 Verify.EnableSettings 或 Verify.DisableSettings 方法的设置值可以是以下值之一：

<span id="VerifySettings_LogOnlyFailures___0x01"></span><span id="verifysettings_logonlyfailures___0x01"></span><span id="VERIFYSETTINGS_LOGONLYFAILURES___0X01"></span>VerifySettings\_LogOnlyFailures = 0x01  
只有失败日志记录，没有任何输出上成功验证调用。

<span id="VerifySettings_LogFailuresAsBlocked___0x02"></span><span id="verifysettings_logfailuresasblocked___0x02"></span><span id="VERIFYSETTINGS_LOGFAILURESASBLOCKED___0X02"></span>VerifySettings\_LogFailuresAsBlocked = 0x02  
故障记录为已阻止，而不是默认值 Error。

<span id="VerifySettings_LogFailuresAsWarnings___0x04"></span><span id="verifysettings_logfailuresaswarnings___0x04"></span><span id="VERIFYSETTINGS_LOGFAILURESASWARNINGS___0X04"></span>VerifySettings\_LogFailuresAsWarnings = 0x04  
故障记录为警告，而不是默认值 Error。

<span id="VerifySettings_LogValuesOnSuccess___0x08"></span><span id="verifysettings_logvaluesonsuccess___0x08"></span><span id="VERIFYSETTINGS_LOGVALUESONSUCCESS___0X08"></span>VerifySettings\_LogValuesOnSuccess = 0x08  
要验证的参数值编写为验证日志消息的一部分。 **这是在默认情况下。**

<span id="VerifySettings_CoerceTypes___0x1000"></span><span id="verifysettings_coercetypes___0x1000"></span><span id="VERIFYSETTINGS_COERCETYPES___0X1000"></span>VerifySettings\_CoerceTypes = 0x1000  
将以下 JScript 强制转换规则强制转换的值传递给验证方法。 **这是在默认情况下。**

<span id="VerifySettings_DisableExceptions___0x2000"></span><span id="verifysettings_disableexceptions___0x2000"></span><span id="VERIFYSETTINGS_DISABLEEXCEPTIONS___0X2000"></span>VerifySettings\_DisableExceptions = 0x2000  
在验证失败时，将不会引发异常。

### <a name="span-idsettingsscriptspanspan-idsettingsscriptspanverify-settings"></a><span id="settings_script"></span><span id="SETTINGS_SCRIPT"></span>验证设置

验证 API 提供了设置来配置它的行为。 EnableSettings 和 DisableSettings 方法可用于启用或禁用特定的验证类维护的设置。 这些方法采用一个或多个要启用或禁用的设置。

```cpp
    Verify.EnableSettings(VerifySettings_LogOnlyFailures);
```

若要启用或禁用在一个调用中的多个设置，可以包括多个 VerifySettings 标志：

```cpp
    Verify.EnableSettings(VerifySettings_LogOnlyFailures | VerifySettings_DisableExceptions);
```

EnableSettings 和 DisableSettings 方法返回可用于还原原始设置，给定作用域; 从而使得设置来启用或禁用的对象

```cpp
1    var guard = Verify.EnableSettings(VerifySettings_LogOnlyFailures);
2    try
3    {
4        Verify.AreEqual(10, 0xa);
5    }
6    finally
7    {
8        guard.Restore();
9    }
```

在此示例中，传递 Verify.EnableSettings 方法 VerifySettings\_LogOnlyFailures'，这将使用已验证对象上存在的设置合并。 Try finally 块中进行验证调用，以便在 finally 块中，可以使用保护对象来还原原始设置。

### <a name="span-idexceptionscriptspanspan-idexceptionscriptspanexception-based-verify-usage"></a><span id="exception_script"></span><span id="EXCEPTION_SCRIPT"></span>基于异常验证使用情况

默认情况下验证方法将引发异常时验证失败。 在运行下 TAEF 如果测试方法引发异常时，测试将会失败。 例如：

```cpp
1    var guard = Verify.EnableSettings(VerifySettings_CoerceTypes);
2    try
3    {
4        Verify.AreEqual(1, "1");
5        Verify.AreEqual("1", 1);
6    }
7    finally
8    {
9        guard.Restore();
10   }
```

在此示例中，第二次验证调用将永远不会进行，因为第一个将引发异常，并使测试失败。 可以使用验证 API 上的设置支持要更改此行为，以便失败的验证不会引发，这将允许进行的后续验证调用。 这是特别有用，若要验证的一组参数，并确保所有验证后被写出。

```cpp
1    var guard = Verify.EnableSettings(VerifySettings_CoerceTypes | VerifySettings_DisableExceptions);
2    try
3    {
4        Verify.AreEqual(1, "1");
5        Verify.AreEqual("1", 1);
6    }
7    finally
8    {
9        guard.Restore();
10   }
```

异常已禁用，因为这两个验证将写入到日志中。

### <a name="span-idoutsideapiscriptspanspan-idoutsideapiscriptspanusing-the-scriptable-verify-api-outside-taef"></a><span id="outsideapi_script"></span><span id="OUTSIDEAPI_SCRIPT"></span>使用可编写脚本来验证 API 外部 TAEF

外部 TAEF，可以使用可编写脚本的验证 API。 请确保注册时 Te.Common.dll 中, 所述[安装部分](#installation)，以及创建"TE.Common.Verify"类的简单。

```cpp
var VerifySettings_DisableExceptions = 0x2000;

var Verify = new ActiveXObject("TE.Common.Verify");
var Log = new ActiveXObject("WEX.Logger.Log");

Verify.EnableSettings(VerifySettings_DisableExceptions);

Log.StartGroup("Group A");
Verify.AreEqual(1, 2);
Log.EndGroup("Group A");

Log.StartGroup("Group B");
Verify.AreEqual(2, 2);
Log.EndGroup("Group B");
```

前面的代码将生成以下控制台输出通过 cscript 执行时：

``` syntax
StartGroup: Group A
Error: Verify: AreEqual - Values (1, 2)
EndGroup: Group A [Failed]

StartGroup: Group B
Verify: AreEqual - Values (2, 2)
EndGroup: Group B [Passed]

Non-passing Tests:

    Group A [Failed]

Summary: Total=2, Passed=1, Failed=1, Blocked=0, Not Run=0, Skipped=0
```

[WEX。Logger.Log API](wexlogger.md)可用于配置 WEX 记录器根据需要 （例如，作为子进程），并可编写脚本的验证 API 将充分利用该配置。









