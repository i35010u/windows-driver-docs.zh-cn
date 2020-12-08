---
title: 验证框架
description: 验证框架
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52d3a3a05d9e690e26024f3cb130c76e355c0728
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806595"
---
# <a name="verify-framework"></a>验证框架


为了更轻松地编写测试，TAEF 提供了 "验证" 框架，该框架利用 [WexLogger](wexlogger.md) 只需少量的代码即可报告详细日志。 验证框架可帮助测试提供结构化日志输出，如果给定验证成功，它将输出成功的日志，如果验证失败，它将输出详细信息。

## <a name="span-idcplusplusspanspan-idcplusplusspanusing-verify-from-c"></a><span id="cplusplus"></span><span id="CPLUSPLUS"></span>使用 c + + 验证


验证 API 在 c + + 中显示为一组宏，这些宏在 "Verify .h" 标头文件中定义 (注意：不需要显式包含 Verify .h，而应包括 "WexTestClass"，其中包含标记 c + + 测试以及与验证和 WexLogger API 的) 交互所需的所有内容。

以下验证宏适用于本机 c + + 测试：

| 宏                                                                                     | 功能                                                                                                                                                                                                         |
|-------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 验证 \_ \_ (预期、实际的 \[ 可选消息是否相等 \])                                 | 验证两个指定的对象是否相等。 如果提供，还会记录自定义消息。                                                                                                                                |
| 验证 \_ \_ 不 \_ 等于 (应为，实际为 \[ 可选消息 \])                            | 验证两个指定的对象是否不相等。 如果提供，还会记录自定义消息。                                                                                                                            |
| VERIFY \_ \_ 大于 \_ (expectedGreater，expectedLess， \[ 可选消息 \])             | 验证第一个参数是否大于第二个参数。 如果提供，还会记录自定义消息。                                                                                                       |
| VERIFY \_ \_ 大于 \_ \_ \_ 等于 (expectedGreater，expectedLess， \[ 可选消息 \])  | 验证第一个参数是否大于或等于第二个参数。 如果提供，还会记录自定义消息。                                                                                           |
| 验证 \_ \_ 小于 \_ (expectedLess，expectedGreater， \[ 可选消息 \])                | 验证第一个参数是否小于第二个参数。 如果提供，还会记录自定义消息。                                                                                                          |
| VERIFY \_ \_ 小于 \_ \_ \_ 等于 (expectedLess，expectedGreater， \[ 可选消息 \])     | 验证第一个参数是否小于或等于第二个参数。 如果提供，还会记录自定义消息。                                                                                              |
| 验证 \_ \_ (需要、实际的 \[ 可选消息 \])                                  | 验证指定的两个参数是否引用同一对象。 如果提供，还会记录自定义消息。                                                                                                          |
| 验证 \_ \_ \_ (应为，但实际为 \[ 可选消息 \])                             | 验证指定的两个参数是否不引用相同的对象。 如果提供，还会记录自定义消息。                                                                                                   |
| 验证 \_ 失败 (\[ 可选消息 \])                                                        | 失败，不检查任何情况。 如果提供，还会记录自定义消息。                                                                                                                                        |
| 确认 \_ 为 \_ TRUE (条件， \[ 可选消息 \])                                          | 验证指定的布尔值是否为 true。 Call VERIFY \_ 为 \_ TRUE (！！ \_ \_条件) ，或验证 \_ win32 \_ bool 是否 \_ 成功 (\_ \_ 条件) 来测试 WIN32 bool。 如果提供，还会记录自定义消息。                      |
| 验证 \_ 为 \_ FALSE (条件， \[ 可选消息 \])                                         | 验证指定的 bool 是否为 false。 Call VERIFY \_ 为 \_ FALSE (！！ \_ \_条件) 或验证 \_ win32 \_ bool \_ 失败 (\_ \_ 条件) 来测试 WIN32 bool。 如果提供，还会记录自定义消息。                       |
| VERIFY \_ 为 \_ NULL (对象， \[ 可选消息 \])                                             | 验证指定的参数是否为 NULL。 如果提供，还会记录自定义消息。                                                                                                                                |
| 验证不为 \_ \_ \_ NULL (对象， \[ 可选消息 \])                                        | 验证指定的参数是否不为 NULL。 如果提供，还会记录自定义消息。                                                                                                                            |
| 验证 \_ 成功 (hresult， \[ 可选消息 \])                                           | 验证指定的 HRESULT 是否成功。 如果提供，还会记录自定义消息。                                                                                                                            |
| 验证 \_ 成功 \_ 返回 (hresult， \[ 可选消息 \])                                   | 验证指定的 HRESULT 是否成功，并返回传入宏的 HRESULT。 如果提供，还会记录自定义消息。                                                                     |
| 验证 \_ 失败 (hresult， \[ 可选消息 \])                                              | 验证指定的 HRESULT 是否未成功。 如果提供，还会记录自定义消息。                                                                                                                        |
| 验证 \_ 失败 \_ 返回 (hresult， \[ 可选消息 \])                                      | 验证指定的 HRESULT 是否不成功，并返回传入宏的 HRESULT。 如果提供，还会记录自定义消息。                                                                 |
| 验证 \_ 引发 (操作、异常、 \[ 可选消息 \])                                 | 验证指定的操作是否引发给定的异常类型。 如果提供，还会记录自定义消息。                                                                                                        |
| 验证 \_ 不 \_ (操作、 \[ 可选消息 \]) 的引发                                        | 验证指定的操作是否不引发异常。 如果提供，还会记录自定义消息。                                                                                                            |
| 验证 \_ WIN32 \_ SUCCEEDED (win32Result， \[ 可选消息 \])                                | 验证指定的 Win32 结果是否成功。 如果提供，还会记录自定义消息。                                                                                                                           |
| 验证 \_ WIN32 \_ 成功 \_ 返回 (win32Result， \[ 可选消息 \])                        | 验证指定的 Win32 结果是否成功并返回传入宏的 LONG。 如果提供，还会记录自定义消息。                                                                       |
| 验证 \_ WIN32 \_ 失败 (win32Result， \[ 可选消息 \])                                   | 验证指定的 Win32 结果是否失败。 如果提供，还会记录自定义消息。                                                                                                                              |
| 验证 \_ WIN32 \_ 失败 \_ 返回 (win32Result， \[ 可选消息 \])                           | 验证指定的 Win32 结果是否失败并返回传入宏的 LONG。 如果提供，还会记录自定义消息。                                                                          |
| 验证 \_ WIN32 \_ BOOL \_ SUCCEEDED (win32Bool， \[ 可选消息 \])                            | 验证指定的 Win32 BOOL 是否成功 (！ = FALSE) 。 如果验证失败，将记录 GetLastError ( # A1 的结果。 如果提供，还会记录自定义消息。                                                     |
| 验证 \_ WIN32 \_ BOOL \_ SUCCEEDED \_ RETURN (win32Bool， \[ 可选消息 \])                    | 验证指定的 Win32 BOOL 是否成功 (！ = FALSE) 并返回传入宏的布尔值。 如果验证失败，将记录 GetLastError ( # A1 的结果。 如果提供，还会记录自定义消息。 |
| 验证 \_ WIN32 \_ BOOL \_ 失败 (win32Bool， \[ 可选消息 \])                               | 验证指定的 Win32 BOOL (= = FALSE) 失败。 不记录 GetLastError ( # A1 的结果。 如果提供，还会记录自定义消息。                                                                          |
| 验证 \_ WIN32 \_ BOOL \_ 失败 \_ 返回 (win32Bool， \[ 可选消息 \])                       | 验证指定的 Win32 BOOL 是否失败 (= = FALSE) 并返回传入宏的布尔值。 不记录 GetLastError ( # A1 的结果。 如果提供，还会记录自定义消息。                      |



### <a name="span-idexception_cplusplusspanspan-idexception_cplusplusspanexception-based-verify-usage"></a><span id="exception_cplusplus"></span><span id="EXCEPTION_CPLUSPLUS"></span>基于异常的验证使用情况

如果已使用启用了 c + + 异常的源代码进行编译 (通过指定 "/EHsc" 命令行开关，或) 中的 "使用 \_ 本机 \_ EH = 1" 宏，则验证宏将默认为失败时记录错误，然后引发本机 c + + 异常。 引发的异常是 **WEX：： testexecution.completed：： VerifyFailureException**。 不需要捕获此异常-TAEF 框架将为您捕获此异常，并转到下一个测试用例。

（可选）如果想要在行中执行一系列验证，而不是在第一次验证失败时中止测试，可以使用 **DisableVerifyExceptions** 类。 对象的生存期控制禁用异常的时间量。

```cpp
if (NULL != m_key)
{
    DisableVerifyExceptions disable;
    VERIFY_WIN32_SUCCEEDED(::RegDeleteKey(HKEY_CURRENT_USER, zTempName));
    VERIFY_WIN32_SUCCEEDED(::RegCloseKey(m_key));
}
```

在上面的示例中，仅在 "if (NULL！ = m \_ key) " 块中禁用异常; 如果第一个验证调用失败，则仍会进行第二次验证调用。

**DisableVerifyExceptions** 类具有引用计数，并且还在每个线程的基础上起作用。

### <a name="span-idnonexception_cplusplusspanspan-idnonexception_cplusplusspannon-exception-based-verify-usage"></a><span id="nonexception_cplusplus"></span><span id="NONEXCEPTION_CPLUSPLUS"></span>基于非异常验证使用情况

如果你的源代码是 **_not_* _，并且已在 c + + 异常的情况下进行编译，则在验证失败时，验证宏不会引发本机 c + +。 此外，如果您的源代码是在已启用 c + + 异常的情况下编译的，但您想要禁用验证异常，则 \# \_ \_ 在包括 "WexTestClass" 之前，只需定义无验证异常。

在此模型中，您必须执行一系列嵌套的 if 语句，以便控制您的测试用例的流动，而不是依赖 c + + 异常。

```cpp
if (VERIFY_WIN32_SUCCEEDED(::RegDeleteKey(HKEY_CURRENT_USER, zTempName)))
{
    ...
}
```

### <a name="span-idoutsettings_cplusplusspanspan-idoutsettings_cplusplusspanverify-output-settings"></a><span id="outsettings_cplusplus"></span><span id="OUTSETTINGS_CPLUSPLUS"></span>验证输出设置

如果要自定义验证 Api 生成的输出，可以使用 _ *SetVerifyOutput** 类。 对象的生存期控制设置输出设置的时间。 **SetVerifyOutput** 类对每个线程进行引用计数和函数。

```cpp
if (NULL != m_key)
{
    SetVerifyOutput verifySettings(VerifyOutputSettings::LogOnlyFailures);
    VERIFY_IS_TRUE(true, L"Should NOT log a comment");
    VERIFY_IS_TRUE(false, L"Should log an error");
}
VERIFY_IS_TRUE(true, L"Should log a comment");
```

在上面的示例中，指定的设置仅适用于在 "if (NULL！ = m \_ key) " 块内进行的调用，并且 *仅* 会记录失败的验证调用。 但会记录第三个验证调用，即使成功。 这是因为 SetVerifyOutput 类超出了范围。

以下选项用于设置验证输出：

<span id="VerifyOutputSettings__LogOnlyFailures_"></span><span id="verifyoutputsettings__logonlyfailures_"></span><span id="VERIFYOUTPUTSETTINGS__LOGONLYFAILURES_"></span>VerifyOutputSettings::LogOnlyFailures   
仅记录失败的验证调用;所有成功的调用都将被忽略。

<span id="VerifyOutputSettings__LogFailuresAsBlocked_"></span><span id="verifyoutputsettings__logfailuresasblocked_"></span><span id="VERIFYOUTPUTSETTINGS__LOGFAILURESASBLOCKED_"></span>VerifyOutputSettings::LogFailuresAsBlocked   
将所有失败记录为已阻止，而不是记录错误。

<span id="VerifyOutputSettings__LogFailuresAsWarnings_"></span><span id="verifyoutputsettings__logfailuresaswarnings_"></span><span id="VERIFYOUTPUTSETTINGS__LOGFAILURESASWARNINGS_"></span>VerifyOutputSettings::LogFailuresAsWarnings   
将所有失败记录为警告，而不是记录错误。

<span id="VerifyOutputSettings__LogValuesOnSuccess_"></span><span id="verifyoutputsettings__logvaluesonsuccess_"></span><span id="VERIFYOUTPUTSETTINGS__LOGVALUESONSUCCESS_"></span>VerifyOutputSettings::LogValuesOnSuccess   
记录传入参数的值，即使在验证调用成功时也是如此。

验证输出设置可以是，也可以组合在一起启用多个设置：

```cpp
SetVerifyOutput verifySettings(VerifyOutputSettings::LogOnlyFailures | VerifyOutputSettings::LogFailuresAsBlocked);
```

### <a name="span-idoutcustom_cplusplusspanspan-idoutcustom_cplusplusspanproviding-value-output-for-custom-types"></a><span id="outcustom_cplusplus"></span><span id="OUTCUSTOM_CPLUSPLUS"></span>为自定义类型提供值输出

C + + 验证框架提供了生成任何自定义类型的详细输出的功能。 为此，必须实现 **WEX：： testexecution.completed：： VerifyOutputTraits** 类模板的专用化。

**WEX：： testexecution.completed** 命名空间中必须存在 **WEX：： Testexecution.completed：： VerifyOutputTraits** 类模板特殊化。 它还应提供名为 **ToString** 的公共静态方法，该方法采用对类的引用，并返回 **WEX：： Common：： NoThrowString** ，其中包含其值的字符串表示形式。

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

### <a name="span-idcomparators_cplusplusspanspan-idcomparators_cplusplusspanproviding-comparators-for-custom-types"></a><span id="comparators_cplusplus"></span><span id="COMPARATORS_CPLUSPLUS"></span>为自定义类型提供比较运算符

C + + Verify framework 提供了为未实现相应运算符重载 (运算符 =、运算符等) 的自定义类型定义比较运算符的能力 &lt; 。 为此，必须实现 **WEX：： testexecution.completed：： VerifyCompareTraits** 类模板的专用化。

**WEX：： testexecution.completed** 命名空间中必须存在 **WEX：： Testexecution.completed：： VerifyCompareTraits** 类模板特殊化。 还应提供名为 **assert.areequal**、 **AreSame**、 **IsLessThan**、 **IsGreaterThan** 和 **IsNull** 的公共静态方法。

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

## <a name="span-idcsharpspanspan-idcsharpspanusing-verify-from-c"></a><span id="csharp"></span><span id="CSHARP"></span>使用 C 验证#


C # 验证用法类似于 c + +。 不过，它是通过 WEX 提供的 **。Testexecution.completed** ，它位于 **Te.Managed.dll** 中。

以下验证方法可用于 c # 测试：

| 宏                                                                                       | 功能                                                                                                                                                                       |
|---------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 需要 Assert.areequal (对象，对象实际)                                                     | 验证两个指定的对象是否相等。                                                                                                                                      |
| Assert.areequal (对象、对象实际值、字符串消息)                                     | 验证两个指定的对象是否相等;在验证成功或失败时记录自定义消息。                                                                            |
| Assert.areequal &lt; t &gt; (应为 T，t 实际)                                                      | 验证两个指定的对象是否相等。                                                                                                                                      |
| Assert.areequal &lt; t &gt; (应为 t，而不是实际的字符串消息)                                      | 验证两个指定的对象是否相等;在验证成功或失败时记录自定义消息。                                                                            |
| 需要 AreNotEqual (对象，对象实际)                                                  | 验证两个指定的对象是否不相等。                                                                                                                                  |
| AreNotEqual (对象、对象实际值、字符串消息)                                  | 验证两个指定的对象是否不相等;在验证成功或失败时记录自定义消息。                                                                        |
| AreNotEqual &lt; t &gt; (应为 T，t 实际)                                                   | 验证两个指定的对象是否不相等。                                                                                                                                  |
| AreNotEqual &lt; t &gt; (应为 t，而不是实际的字符串消息)                                   | 验证两个指定的对象是否不相等;在验证成功或失败时记录自定义消息。                                                                        |
| 需要 AreSame (对象，对象实际)                                                      | 验证指定的两个参数是否引用同一对象。                                                                                                                |
| AreSame (对象、对象实际值、字符串消息)                                      | 验证指定的两个参数是否引用同一对象;在验证成功或失败时记录自定义消息。                                                      |
| 需要 AreNotSame (对象，对象实际)                                                   | 验证指定的两个参数是否不引用相同的对象。                                                                                                         |
| AreNotSame (对象、对象实际值、字符串消息)                                   | 验证指定的两个参数是否不引用相同的对象;在验证成功或失败时记录自定义消息。                                               |
| IsGreaterThan (IComparable expectedGreater，IComparable expectedLess)                         | 验证第一个参数是否大于第二个参数。                                                                                                             |
| IsGreaterThan (IComparable expectedGreater，IComparable expectedLess，string message)         | 验证第一个参数是否大于第二个参数;在验证成功或失败时记录自定义消息。                                                   |
| IsGreaterThanOrEqual (IComparable expectedGreater，IComparable expectedLess)                  | 验证第一个参数是否大于或等于第二个参数。                                                                                                 |
| IsGreaterThanOrEqual (IComparable expectedGreater，IComparable expectedLess，string message)  | 验证第一个参数是否大于或等于第二个参数;在验证成功或失败时记录自定义消息。                                       |
| IsLessThan (IComparable expectedLess，IComparable expectedGreater)                            | 验证第一个参数是否小于第二个参数。                                                                                                                |
| IsLessThan (IComparable expectedLess，IComparable expectedGreater，string message)            | 验证第一个参数是否小于第二个参数;在验证成功或失败时记录自定义消息。                                                      |
| IsLessThanOrEqual (IComparable expectedLess，IComparable expectedGreater)                     | 验证第一个参数是否小于或等于第二个参数。                                                                                                    |
| IsLessThanOrEqual (IComparable expectedLess，IComparable expectedGreater，string message)     | 验证第一个参数是否小于或等于第二个参数;在验证成功或失败时记录自定义消息。                                          |
|  (字符串消息失败)                                                                         | 失败，不检查任何情况。                                                                                                                                              |
| IsTrue (bool 条件)                                                                       | 验证指定的条件是否为 true。                                                                                                                                      |
| IsTrue (布尔条件，字符串消息)                                                       | 验证指定的条件是否为 true;在验证成功或失败时记录自定义消息。                                                                            |
| IsFalse (bool 条件)                                                                      | 验证指定的条件是否为 false。                                                                                                                                     |
| IsFalse (布尔条件，字符串消息)                                                      | 验证指定的条件是否为 false;在验证成功或失败时记录自定义消息。                                                                           |
| IsNull (对象 obj)                                                                           | 验证指定的参数是否为 NULL。                                                                                                                                      |
| IsNull (对象 obj，字符串消息)                                                           | 验证指定的参数是否为 NULL;在验证成功或失败时记录自定义消息。                                                                            |
| IsNotNull (对象 obj)                                                                        | 验证指定的参数是否不为 NULL。                                                                                                                                  |
| IsNotNull (对象 obj，字符串消息)                                                        | 验证指定的参数是否不为 NULL;在验证成功或失败时记录自定义消息。                                                                        |
| &lt; &gt; (VerifyOperation 操作引发 T)                                                   | 验证指定的操作是否引发给定的异常类型。 还返回异常以进行进一步检查。                                                           |
| 引发 &lt; T &gt; (VerifyOperation 操作，字符串消息)                                   | 验证指定的操作是否引发给定的异常类型;在验证成功或失败时记录自定义消息。 还返回异常以进行进一步检查。 |
| NoThrow (VerifyOperation 操作)                                                           | 验证指定的操作是否不引发异常。                                                                                                                  |
| NoThrow (VerifyOperation 操作，字符串消息)                                           | 验证指定的操作是否不引发异常;在验证成功或失败时记录自定义消息。                                                        |



### <a name="span-idexception_csharpspanspan-idexception_csharpspanexception-based-verify-usage"></a><span id="exception_csharp"></span><span id="EXCEPTION_CSHARP"></span>基于异常的验证使用情况

当 c # 测试用例中出现验证失败时，会将错误写入记录器和 **WEX。Testexecution.completed VerifyFailureException** 。 与在本机 c + + 模型中一样，无需担心捕获这些异常。 TAEF 框架将为您捕获它，并转到下一个测试用例。

（可选）如果想要在行中执行一系列验证，而不是在第一次验证失败时中止测试，可以使用 **DisableVerifyExceptions** 类。 对象的生存期控制禁用异常的时间量。 **DisableVerifyExceptions** 类对每个线程进行引用计数和函数。

```cpp
using (new DisableVerifyExceptions())
{
    Verify.AreSame(item1, item2);
    Verify.AreEqual(item1, item2);
}
```

在上述示例中，如果第一个验证调用失败，则仍进行第二次验证调用。

或者，您可以在验证操作（如下面所示的示例）前设置 **DisableVerifyExceptions = true** ，以获得相同的结果。

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

请注意，尽管此类选项可用，但仍建议在 using 块中将 DisableVerifyExeptions 声明为对象。

如果要在发生验证错误时在调试器中停止，请按 Ctrl + Alt + E)  (打开 "异常" 对话框，单击 "添加"，在下拉列表中选择 "公共语言运行时异常"，并将 "WEX" 放入其中。Testexecution.completed. VerifyFailureException "。

### <a name="span-idoutsettings_csharpspanspan-idoutsettings_csharpspanverify-output-settings"></a><span id="outsettings_csharp"></span><span id="OUTSETTINGS_CSHARP"></span>验证输出设置

如果要自定义验证 Api 生成的输出，可以使用 **SetVerifyOutput** 类。 对象的生存期控制设置输出设置的时间。 **SetVerifyOutput** 类对每个线程进行引用计数和函数。

```cpp
using (new SetVerifyOutput(VerifyOutputSettings.LogOnlyFailures))
{
    Log.Comment("Only the following error should be logged:");
    Verify.IsTrue(true, "Should NOT log a comment");
    Verify.IsTrue(false, "Should log an error");
}
Verify.IsTrue(true, "Should log a comment");
```

在上面的示例中，只应记录第二个验证调用，因为它是在 using 块中唯一失败的调用。 但 *会* 记录第三个验证调用，即使成功。 这是因为 SetVerifyOutput 类超出了范围。

或者，通过在验证操作之前设置 **OutputSettings = VerifyOutputSettings** （如下面所示的示例），可以获得相同的结果。

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

请注意，尽管此类选项可用，但仍建议在 using 块中将 SetVerifyOutput 声明为对象。

以下选项用于设置验证输出：

<span id="verifyoutputsettings.logonlyfailures_"></span><span id="VERIFYOUTPUTSETTINGS.LOGONLYFAILURES_"></span>VerifyOutputSettings.LogOnlyFailures   
仅记录失败的验证调用;所有成功的调用都将被忽略。

<span id="verifyoutputsettings.logfailuresasblocked_"></span><span id="VERIFYOUTPUTSETTINGS.LOGFAILURESASBLOCKED_"></span>VerifyOutputSettings.LogFailuresAsBlocked   
将所有失败记录为已阻止，而不是记录错误。

<span id="verifyoutputsettings.logfailuresaswarnings_"></span><span id="VERIFYOUTPUTSETTINGS.LOGFAILURESASWARNINGS_"></span>VerifyOutputSettings.LogFailuresAsWarnings   
将所有失败记录为警告，而不是记录错误。

验证输出设置可以是，也可以组合在一起启用多个设置：

```cpp
using (new SetVerifyOutput(VerifyOutputSettings.LogFailuresAsBlocked | VerifyOutputSettings.LogOnlyFailures))
{
...
}
```

## <a name="span-idscriptspanspan-idscriptspanusing-verify-from-script"></a><span id="script"></span><span id="SCRIPT"></span>使用脚本验证


还为脚本语言显示了验证 API，遵循与 c + + 和 c # 相同的使用模式。

### <a name="span-idinstallationspanspan-idinstallationspanspan-idinstallationspaninstallation"></a><span id="Installation"></span><span id="installation"></span><span id="INSTALLATION"></span>安装

在 TAEF 测试方法中使用可编写脚本的验证 API 时，无需安装-所需 API 是使用 "注册免费 COM" 注册的。 若要从 TAEF 测试方法外部使用可编写脚本的 API (外部 TAEF 或子) 进程中，只需在提升的命令提示符下使用 regsvr32 注册 Te.Common.dll 二进制值;例如：

``` syntax
regsvr32 Te.Common.dll
```

使用部署文件部署 TAEF 时，将自动注册 Te.Common.dll。

### <a name="span-idusage_scriptspanspan-idusage_scriptspanusage"></a><span id="usage_script"></span><span id="USAGE_SCRIPT"></span>用法

可编写脚本的验证 API 通过 "TE. Verify" COM 类进行呈现-只需实例化该类并对其调用方法，Verify 类就会自动与 WEXLogger 一起使用，将传递和失败验证写入日志。

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

此示例定义了一个 TAEF 脚本测试类，其中包含一个 "HelloWorld" 方法。 第6行使用 "object" 元素来定义全局范围内的验证变量。 第8行使用 "reference" 元素包括指定类型库中的所有常量 (在本例中，Te.Common.dll 的类型库) 到脚本的全局范围内;在这种情况下，它将添加 "VerifySettings" 常数。 第16行和第17行只显示验证 API 的用法。 执行时，此示例将生成以下输出：

``` syntax
Test Authoring and Execution Framework v2.7 Build 6.2.7922.0 (fbl_esc_end_dev(mschofie).110202-1000) For x86

StartGroup: Example::HelloWorld
Verify: IsTrue
Verify: IsFalse
EndGroup: Example::HelloWorld [Passed]

Summary: Total=1, Passed=1, Failed=0, Blocked=0, Not Run=0, Skipped=0
```

### <a name="span-idapi_scriptspanspan-idapi_scriptspanscriptable-verify-api"></a><span id="api_script"></span><span id="API_SCRIPT"></span>可脚本验证 API

可编写脚本的验证 API 上的验证方法如下所示：

| 方法                                                                                | 功能                                                                                                                                                                                                                                                                                                                  |
|---------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| bool Assert.areequal (应为，实际为 \[ 可选消息 \])                           | 验证两个值是否相等。 如果 "VerifySettings \_ CoerceTypes" 设置已启用，则此方法使用相等性的 JScript 定义，如果 \_ 未启用 "VerifySettings CoerceTypes" 设置，则该方法将使用标识的 JScript 定义。 **\_默认情况下，"VerifySettings CoerceTypes" 处于打开状态。**     |
| bool AreNotEqual (应为，实际为 \[ 可选消息 \])                        | 验证两个值是否不相等。 如果 "VerifySettings \_ CoerceTypes" 设置已启用，则此方法使用相等性的 JScript 定义，如果 \_ 未启用 "VerifySettings CoerceTypes" 设置，则该方法将使用标识的 JScript 定义。 **\_默认情况下，"VerifySettings CoerceTypes" 处于打开状态。** |
| bool IsGreaterThan (expectedGreater，expectedLess， \[ 可选消息 \])         | 验证第一个值是否大于第二个值。                                                                                                                                                                                                                                                                      |
| bool IsGreaterThanOrEqual (expectedGreater，expectedLess， \[ 可选消息 \])  | 验证第一个值是否大于或等于第二个值。                                                                                                                                                                                                                                                          |
| bool IsLessThan (expectedLess，expectedGreater， \[ 可选消息 \])            | 验证第一个值是否小于第二个值。                                                                                                                                                                                                                                                                         |
| bool IsLessThanOrEqual (expectedLess，expectedGreater， \[ 可选消息 \])     | 验证第一个值是否小于或等于第二个值。                                                                                                                                                                                                                                                             |
| bool AreSame (应为，实际为 \[ 可选消息 \])                            | 验证值是否相同。                                                                                                                                                                                                                                                                                         |
| bool AreNotSame (应为，实际为 \[ 可选消息 \])                         | 验证这些值是否相同。                                                                                                                                                                                                                                                                                     |
| bool 验证。 (\[ 可选消息失败 \])                                                 | 在未检查条件的情况下失败。                                                                                                                                                                                                                                                                                             |
| bool IsTrue (表达式， \[ 可选消息 \])                                   | 验证给定的表达式的计算结果是否为 true。                                                                                                                                                                                                                                                                          |
| bool IsFalse (表达式， \[ 可选消息 \])                                  | 验证给定的表达式的计算结果是否为 false。                                                                                                                                                                                                                                                                         |
| 布尔验证 (应为 \[ 可选消息 \])                                     | 验证给定的值是否为 "null"。                                                                                                                                                                                                                                                                                       |
| 需要 (布尔值， \[ 可选消息 \])                                  | 验证给定的值是否不是 "null"。                                                                                                                                                                                                                                                                                   |
| bool 验证。引发 (函数、 \[ 可选消息 \])                                     | 验证给定函数是否引发了异常。                                                                                                                                                                                                                                                                         |
| bool NoThrow (函数， \[ 可选消息 \])                                    | 验证给定函数不引发异常。                                                                                                                                                                                                                                                                 |



Verify 类上有两种方法可用于控制设置：

| 方法                                  | 功能                                         |
|-----------------------------------------|-------------------------------------------------------|
| 对象 EnableSettings (设置)   | 将启用指定的设置标志或标志。  |
| 对象 DisableSettings (设置)  | 将禁用指定的设置标志或标志。 |



传递给 EnableSettings 或 DisableSettings 方法的设置值可以是以下值之一：

<span id="VerifySettings_LogOnlyFailures___0x01"></span><span id="verifysettings_logonlyfailures___0x01"></span><span id="VERIFYSETTINGS_LOGONLYFAILURES___0X01"></span>VerifySettings \_ LogOnlyFailures = 0x01  
仅记录失败-成功的验证调用无输出。

<span id="VerifySettings_LogFailuresAsBlocked___0x02"></span><span id="verifysettings_logfailuresasblocked___0x02"></span><span id="VERIFYSETTINGS_LOGFAILURESASBLOCKED___0X02"></span>VerifySettings \_ LogFailuresAsBlocked = 0x02  
失败记录为 "已阻止"，而不是默认的 "错误"。

<span id="VerifySettings_LogFailuresAsWarnings___0x04"></span><span id="verifysettings_logfailuresaswarnings___0x04"></span><span id="VERIFYSETTINGS_LOGFAILURESASWARNINGS___0X04"></span>VerifySettings \_ LogFailuresAsWarnings = 0x04  
失败记录为 "警告"，而不是默认的 "错误"。

<span id="VerifySettings_LogValuesOnSuccess___0x08"></span><span id="verifysettings_logvaluesonsuccess___0x08"></span><span id="VERIFYSETTINGS_LOGVALUESONSUCCESS___0X08"></span>VerifySettings \_ LogValuesOnSuccess = 0x08  
要验证的参数的值作为验证日志消息的一部分写入。 **默认情况下，这是打开的。**

<span id="VerifySettings_CoerceTypes___0x1000"></span><span id="verifysettings_coercetypes___0x1000"></span><span id="VERIFYSETTINGS_COERCETYPES___0X1000"></span>VerifySettings \_ CoerceTypes = 0x1000  
传递给验证方法的值将按照 JScript 强制规则强制转换。 **默认情况下，这是打开的。**

<span id="VerifySettings_DisableExceptions___0x2000"></span><span id="verifysettings_disableexceptions___0x2000"></span><span id="VERIFYSETTINGS_DISABLEEXCEPTIONS___0X2000"></span>VerifySettings \_ DisableExceptions = 0x2000  
当验证失败时，将不会引发异常。

### <a name="span-idsettings_scriptspanspan-idsettings_scriptspanverify-settings"></a><span id="settings_script"></span><span id="SETTINGS_SCRIPT"></span>验证设置

验证 API 提供设置来配置其行为。 "EnableSettings" 和 "DisableSettings" 方法可用于启用或禁用 Verify 类维护的特定设置。 方法采用一个或多个设置来启用或禁用。

```cpp
    Verify.EnableSettings(VerifySettings_LogOnlyFailures);
```

若要在一个调用中启用或禁用多个设置，可以包含多个 "VerifySettings" 标志：

```cpp
    Verify.EnableSettings(VerifySettings_LogOnlyFailures | VerifySettings_DisableExceptions);
```

EnableSettings 和 DisableSettings 方法返回一个对象，该对象可用于还原原始设置，允许在给定范围内启用或禁用设置;

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

在此示例中，将 EnableSettings 方法传递到 "VerifySettings \_ LogOnlyFailures"，该方法将与验证对象上已存在的设置合并。 验证调用是在 try finally 块内进行的，因此，在 finally 块中，可以使用 "guard" 对象来还原原始设置。

### <a name="span-idexception_scriptspanspan-idexception_scriptspanexception-based-verify-usage"></a><span id="exception_script"></span><span id="EXCEPTION_SCRIPT"></span>基于异常的验证使用情况

默认情况下，验证方法会在验证失败时引发异常。 如果在测试方法中引发异常时在 TAEF 下运行，则测试将失败。 例如：

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

在此示例中，不会进行第二次验证调用，因为第一次验证调用将引发异常并使测试失败。 验证 API 上的设置支持可用于更改此行为，因此失败的验证不会引发，这允许进行后续验证调用。 这对于验证一组参数特别有用，请确保所有验证都已写出。

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

由于异常已禁用，这两种验证都将写入日志。

### <a name="span-idoutsideapi_scriptspanspan-idoutsideapi_scriptspanusing-the-scriptable-verify-api-outside-taef"></a><span id="outsideapi_script"></span><span id="OUTSIDEAPI_SCRIPT"></span>在 TAEF 外使用可编写脚本的验证 API

可脚本验证 API 可在 TAEF 之外使用。 请确保注册了 Te.Common.dll，如 [安装部分](#installation)中所述，简单地创建 "TE" 类。

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

前面的代码在通过 cscript 执行时，将生成以下控制台输出：

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

["WEX"。记录器 .Log API](wexlogger.md)可用于根据需要配置 WEX 记录器 (例如，) 子进程，并且可编写脚本的验证 API 将利用该配置。









