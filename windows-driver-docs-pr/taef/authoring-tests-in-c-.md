---
title: 使用 C# 创作测试
description: 使用 C# 创作测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 232133acd736c6b98a766b01b385a207a3b04070
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790901"
---
# <a name="authoring-tests-in-c"></a>使用 C# 创作测试


下面的示例演示了一个 c # .cs 文件，其中包含一个简单的单个测试类，demostrates c # 测试标记。  (请注意，此示例仅适用于 demonstrational 目的，因此它将不会进行编译或运行。 ) 

```cpp
1    using Microsoft.VisualStudio.TestTools.UnitTesting;
2    using System;
3    using System.Collections;
4    using WEX.Logging.Interop;
5    using WEX.TestExecution;
6
7    [TestClass]
8    public class ManagedStartMenuTests
9    {
10       [AssemblyInitialize]
11       [TestProperty("Component", "Navigation")]
12       [TestProperty("SubComponent", "StartMenu")]
13       public static void RunModuleSetup(Object context)
14       {
15           defaultPolicy = SetObjectFactoryPolicy(PolicyClassic);
16       }
17
18       [AssemblyCleanup]
19       public static void RunModuleCleanup()
20       {
21           SetObjectFactoryPolicy(defaultPolicy);
22       }
23
24       [ClassInitialize]
25       [TestProperty("TeamOwner", "WEX")]
26       [TestProperty("GroupOwner", "MediaPlayerTest")]
27       public static void TestClassSetup(Object testContext)
28       {
29           objectFactory = new ObjectFactory();
30       }
31
32       [ClassCleanup]
33       public static void TestClassCleanup()
34       {
35           objectFactory.Dispose();
36       }
37
38       [TestInitialize]
39       public void TestMethodSetup()
40       {
41           startMenuObject = objectFactory.CreateObject();
42       }
43
44       [TestCleanup]
45       public void TestMethodCleanup()
46       {
47           startMenuObject.Dispose();
48       }
49
50
51       [TestMethod]
52       [Owner("Someone")]
53       [Priority(0)]
54       public void TestMethod1()
55       {
56           Verify.AreEqual(startMenuObject.size, expectedObjectSize);
57       }
58   }
```

对于声明 c \# 测试，TAEF 使用 VSTS 测试标记。

若要在 c # 中声明测试类，请在 \[ \] (第7行) 的普通 c # 类上使用 TestClass 特性，对于测试方法声明，请 \[ \] 在普通类方法 (第) 51 行使用 TestMethod 特性。

C # 测试标记还支持全部的安装和清理方法。

具有 \[ AssemblyInitialize 属性集的静态方法 \] 在任何其他类方法之前运行，并执行程序集级别初始化 (第10行) 。 因此，有一个程序集清理方法，AssemblyCleanup 属性集的静态方法， \[ \] 该方法在所有其他方法完成 (第18行) 完成后运行。

同样，存在类和测试安装和清理方法。  (参见行24、32、38、44) 与 c + + 中的不同，托管代码中的类安装和清理方法必须是静态的。

TAEF c # 测试标记支持 test、class 和 module 属性。

若要设置模块属性，请在程序集初始值设定项 (参见第11行和第12行) 。 与设置类级别属性相同，在类初始值设定项上设置属性 (参见第25行和第26行) 。 对于测试方法级别属性，只需将属性应用到特定的测试方法。  (参见52行和 53) 

## <a name="span-idrunning_under_vstsspanspan-idrunning_under_vstsspanspan-idrunning_under_vstsspanrunning-under-vsts"></a><span id="Running_under_VSTS"></span><span id="running_under_vsts"></span><span id="RUNNING_UNDER_VSTS"></span>在 VSTS 下运行


注意：为了减少对 VSTS 二进制文件的依赖，当前类和程序集的安装方法将对象作为第一个参数。

如果要从 VSTS 运行测试，请将该对象类型更改为 **TestContext** 类型。 请记住，这会在 *microsoft.visualstudio.qualitytools.unittestframework.dll* 和 *microsoft.visualstudio.qualitytools.resource.dll* 上添加依赖关系。

在 VSTS 下运行时，步骤稍有不同。 需要设置本地测试运行设置以复制非托管依赖项。 为此，请参阅：

-   测试- &gt; 编辑测试运行配置- &gt; 本地测试运行
-   单击 "部署"。输入需要为每个测试复制的 dll：
    -   Wex.Logger.dll
    -   Wex.Common.dll
    -   Wex.Common.Managed.dll
    -   Wex.Communication.dll
    -   Wex.Logger.Interop.dll

这是必需的，因为 VSTS 会创建一个新目录，并在每次运行测试用例时复制文件。 你可以在你的项目文件夹中查看计算机上的这些目录作为同级文件夹。

## <a name="span-idrunning_managed_tests_in_the_default_application_domainspanspan-idrunning_managed_tests_in_the_default_application_domainspanspan-idrunning_managed_tests_in_the_default_application_domainspanrunning-managed-tests-in-the-default-application-domain"></a><span id="Running_managed_tests_in_the_default_application_domain"></span><span id="running_managed_tests_in_the_default_application_domain"></span><span id="RUNNING_MANAGED_TESTS_IN_THE_DEFAULT_APPLICATION_DOMAIN"></span>在默认应用程序域中运行托管测试


默认情况下，对于测试代码隔离，TAEF 在特殊的测试应用程序域中执行托管测试。 但是，在使用非默认应用程序域时，本机代码调用托管代码的方案 (例如，托管代码使用的本机回调函数) 可能会导致消息出现错误： "无法跨 Appdomain 传递 GCHandle"。 对于这些情况，请使用 [/defaultAppDomain](te-exe-command-line-parameters.md#defaultappdomain) 开关强制托管测试在默认应用程序域中运行。

请注意，在默认应用程序域中运行托管测试与 [程序集配置文件](assembly-config-files.md)不兼容。

## <a name="span-idsupport_for_async_test_methodsspanspan-idsupport_for_async_test_methodsspanspan-idsupport_for_async_test_methodsspansupport-for-async-test-methods"></a><span id="Support_for_async_test_methods"></span><span id="support_for_async_test_methods"></span><span id="SUPPORT_FOR_ASYNC_TEST_METHODS"></span>支持异步测试方法


TAEF 的 NetFX 4.5 二进制文件支持异步 TAEF 测试方法的执行。 这意味着，用 **async** 关键字标记的 TAEF 测试可以 **等待** 异步操作。

**注意**  不要尝试将此功能与 TAEF 的 NetFX 2.0/3.5 二进制文件一起利用;只有 NetFX 4.5 二进制文件支持此功能。

 

TAEF 支持 async **void** 和 async **Task** 测试方法 (两者都将导致) 相同的功能：

```CSharp
            [TestMethod]
            public async Task MyAsyncTest()
            {
                await AsyncAPICall1();
                var result = await AsyncAPICall2();
                Verify.IsTrue(result);
            }
```

也可使用以下命令：

```CSharp
            [TestMethod]
            public async void MyAsyncTest2()
            {
                await AsyncAPICall1();
                var result = await AsyncAPICall2();
                Verify.IsTrue(result);
            }
```

 

 





