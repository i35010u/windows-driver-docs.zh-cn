---
title: 使用 C# 创作测试
description: 使用 C# 创作测试
ms.assetid: 4DD1D673-FEAF-44a4-8BAD-0E55318DC64B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb66992ef2f12ed5e6f9993827bc33e5edb76dbd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361803"
---
# <a name="authoring-tests-in-c"></a>使用 C# 创作测试


以下示例所示C#.cs 文件具有一个简单的单个测试类该 demostratesC#测试标记。 （请注意此示例中是 demonstrational 仅用于目的，因此它不会编译或运行。）

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

声明 c\#测试、 TAEF 使用 VSTS 测试标记。

若要声明中的测试类C#，你使用\[TestClass\]普通属性C#类 (第 7 行) 并测试方法声明，使用\[TestMethod\]上的普通类方法 (第 51 行中的属性).

C#测试标记还支持完整范围的设置和清理方法。

带有静态方法\[AssemblyInitialize\]属性集类的任何其他方法之前运行并执行程序集级别初始化 (行 10)。 因此，这里有一个程序集清理方法，使用静态方法\[AssemblyCleanup\]属性在所有其他方法完成 (行 18) 后运行的设置。

同样，存在类和测试设置和清理方法。 （请参阅行 24、 32、 38、 44）不同于在C++，在托管代码中的类设置和清理方法必须是静态的。

TAEFC#测试标记支持测试、 类和模块的属性。

若要设置模块属性，请在程序集初始值设定项上设置特性 （请参阅第 11 和 12 行）。 同样要设置类级别属性，请设置类初始值设定项的属性 （请参阅第 25 和 26 行）。 对于测试方法级别的属性，可以只需将属性应用于特定测试方法。 （请参阅第 52 和 53 行）

## <a name="span-idrunningundervstsspanspan-idrunningundervstsspanspan-idrunningundervstsspanrunning-under-vsts"></a><span id="Running_under_VSTS"></span><span id="running_under_vsts"></span><span id="RUNNING_UNDER_VSTS"></span>在 VSTS 下运行


注意： 若要减少对 VSTS 的二进制文件的依赖关系，当前类和程序集安装方法将对象作为第一个参数。

如果你想要从 VSTS 中运行测试，请更改该对象类型设置为**TestContext**类型。 请记住，这将添加的依赖项*microsoft.visualstudio.qualitytools.unittestframework.dll*并*microsoft.visualstudio.qualitytools.resource.dll*。

在 VSTS 下运行时，步骤会稍有不同。 您需要设置你的本地测试运行设置，以通过非托管依赖项。 若要执行此操作，请转到：

-   测试-&gt;编辑测试运行配置-&gt;本地测试运行
-   单击的 Deployment.Enter 为每个测试通过复制所需的 dll:
    -   Wex.Logger.dll
    -   Wex.Common.dll
    -   Wex.Common.Managed.dll
    -   Wex.Communication.dll
    -   Wex.Logger.Interop.dll

由于访问的 VSTS 使新的目录和每次它运行测试用例时，通过复制文件，这是必需的。 您可以看到这些目录在计算机上作为同级文件夹到项目文件夹。

## <a name="span-idrunningmanagedtestsinthedefaultapplicationdomainspanspan-idrunningmanagedtestsinthedefaultapplicationdomainspanspan-idrunningmanagedtestsinthedefaultapplicationdomainspanrunning-managed-tests-in-the-default-application-domain"></a><span id="Running_managed_tests_in_the_default_application_domain"></span><span id="running_managed_tests_in_the_default_application_domain"></span><span id="RUNNING_MANAGED_TESTS_IN_THE_DEFAULT_APPLICATION_DOMAIN"></span>默认应用程序域中运行托管的测试


默认情况下，对于测试代码隔离，TAEF 执行特殊的测试应用程序域中托管的测试。 但是，在使用非默认应用程序域时，本机代码调用到托管代码中 （例如本机回调函数的托管代码使用） 的方案会与消息导致错误："不能将传递一个 GCHandle 跨 Appdomain"。 对于这种情况，强制使用默认应用程序域中运行的托管的测试[/defaultAppDomain](te-exe-command-line-parameters.md#defaultappdomain)切换。

请注意该运行托管在默认应用程序域中的测试是否与不兼容[程序集配置文件](assembly-config-files.md)。

## <a name="span-idsupportforasynctestmethodsspanspan-idsupportforasynctestmethodsspanspan-idsupportforasynctestmethodsspansupport-for-async-test-methods"></a><span id="Support_for_async_test_methods"></span><span id="support_for_async_test_methods"></span><span id="SUPPORT_FOR_ASYNC_TEST_METHODS"></span>对异步测试方法的支持


TAEF 的 NetFX 4.5 二进制文件支持异步 TAEF 测试方法的执行。 这意味着，TAEF 测试对标记有**异步**关键字将能够**await**异步操作。

**请注意**  不尝试利用此功能通过 TAEF 的 NetFX 2.0/3.5 二进制文件; 只能 NetFX 4.5 二进制文件支持此功能。

 

TAEF 支持这两个异步**void**和 async**任务**测试的方法 （同时将导致出现相同的功能）：

```CSharp
            [TestMethod]
            public async Task MyAsyncTest()
            {
                await AsyncAPICall1();
                var result = await AsyncAPICall2();
                Verify.IsTrue(result);
            }
```

或者：

```CSharp
            [TestMethod]
            public async void MyAsyncTest2()
            {
                await AsyncAPICall1();
                var result = await AsyncAPICall2();
                Verify.IsTrue(result);
            }
```

 

 





