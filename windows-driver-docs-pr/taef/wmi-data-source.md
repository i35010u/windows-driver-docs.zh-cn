---
title: WMI 数据源
description: WMI 数据源
ms.assetid: 1C9D0EEC-6542-4249-B7E0-CA3ED63FB120
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfe2f28e487a0dd48106225c101996af591bf197
ms.sourcegitcommit: 7ca2d3e360a4ae1d4d3c3092bd34492a2645ef74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89403264"
---
# <a name="wmi-data-source"></a>WMI 数据源


请确保熟悉 TAEF 的基本执行，并知道如何使用它创作测试，然后再继续此部分。

## <a name="span-idbackgroundspanspan-idbackgroundspanspan-idbackgroundspanbackground"></a><span id="Background"></span><span id="background"></span><span id="BACKGROUND"></span>背景


"WMI" 代表 "Windows Management Instrumentation"。 使用通用信息模型 (CIM) ，这是表示系统的行业标准。 Windows Management Instrumentation 提供了一种统一的方法来访问系统管理信息。

## <a name="span-idhow_does_it_help_my_tests_spanspan-idhow_does_it_help_my_tests_spanspan-idhow_does_it_help_my_tests_spanhow-does-it-help-my-tests"></a><span id="How_does_it_help_my_tests_"></span><span id="how_does_it_help_my_tests_"></span><span id="HOW_DOES_IT_HELP_MY_TESTS_"></span>它如何帮助我的测试？


使用 WMI 查询支持作为 TAEF 中的 WMI 数据源，可以在测试中添加一个前置条件，还可以在运行测试前获取有关测试计算机上资源的信息。 下面是可以使用 WMI 进行的查询类型的一些示例：

-   检查运行测试的计算机是否为便携式计算机，并仅在其为便携式计算机时才运行测试。
-   检查是否已在测试计算机上安装了 Service Pack 并仅在测试计算机上运行了测试。
-   检索测试计算机上的所有可移动驱动器和本地硬盘驱动器，并为与该查询匹配的每个驱动器运行测试。
-   仅在未加入域的测试计算机上运行测试，或
-   仅在测试计算机已加入域并检索域名时才运行测试。

这会给您带来一些想法，希望您可以在何处以及如何使用 WMI 数据源进行测试。 让我们看看如何在创作 TAEF 测试的同时添加此 WMI 查询支持。

测试 WMI 数据源所需的唯一特殊元数据是 "数据源"。 数据源语法必须如下所示：

```cpp
[DataSource("WMI:<WQL query>")]
```

或在本机代码中：

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"WMI:<WQL query>")]
```

您必须注意到，DataSource 值以 "WMI：" 开头，这使 TAEF 知道这确实是依赖于 WMI 查询结果的测试的数据源，并将其与数据驱动的测试区分开来。 这是一种很好的机会，指出当前 TAEF 不支持既是数据驱动的测试，也不支持依赖于 WMI 查询结果的测试。

下一个问题是如何为您要查找的内容编写 WQL 查询？ WQL 查询语法非常类似于简化的 SQL 查询。 [脚本和应用程序的 WMI 任务](/windows/win32/wmisdk/wmi-tasks-for-scripts-and-applications)中提供了一些很好的查询示例。 以下是一些示例：

<span id="SELECT_Description__DesktopInteract__ProcessId_FROM_Win32_Service_WHERE_Name__Themes_"></span><span id="select_description__desktopinteract__processid_from_win32_service_where_name__themes_"></span><span id="SELECT_DESCRIPTION__DESKTOPINTERACT__PROCESSID_FROM_WIN32_SERVICE_WHERE_NAME__THEMES_"></span>选择 \_ Name = ' Themes ' 的 Win32 服务中的 DesktopInteract 说明  
确定要在测试中使用的 "主题" 服务的说明、DesktopInteract 和 ProcessId 属性后，在 "主题" 服务上运行测试。

<span id="SELECT_Capabilities__CapabilityDescriptions_FROM_Win32_Printe"></span><span id="select_capabilities__capabilitydescriptions_from_win32_printe"></span><span id="SELECT_CAPABILITIES__CAPABILITYDESCRIPTIONS_FROM_WIN32_PRINTE"></span>SELECT 功能，CapabilityDescriptions 从 Win32 \_ Printe  
对连接到此计算机的每个打印机运行测试。 允许测试访问每台打印机的功能和 CapabilityDescriptions。

<span id="SELECT_Name__User__Location_FROM_Win32_StartupCommand"></span><span id="select_name__user__location_from_win32_startupcommand"></span><span id="SELECT_NAME__USER__LOCATION_FROM_WIN32_STARTUPCOMMAND"></span>选择名称、用户、从 Win32 StartupCommand 的位置 \_  
针对在 Windows 启动时运行的每个进程运行测试。 对于每个进程，让测试知道进程的名称是什么，它位于 (位置) ，以及进程运行的用户。

您可以在上面提到的文档中找到更多示例，还可以在打开的示例中找到 .cs 文件和标头文件中的更多示例。 一般的、经过简化的语法如下所示：

```cpp
SELECT <comma separated properties> FROM <WMI Class name> [WHERE <add condition on some properties>]
```

在刚刚看到的示例中，Win32 \_ 服务、win32 \_ Printer 和 win32 \_ STARTUPCOMMAND 都是 WMI 类。 可以在 [wmi 类](/windows/win32/wmisdk/wmi-classes)中查找 wmi 类。

TAEF 不支持检索系统属性。

在场景 TAEF 后，将执行查询并确认结果。 如果至少有一个对象作为查询结果返回，则为每个返回的对象执行该测试。 如果 WQL 查询不返回任何对象，则会将此信息记录为已阻止，并执行到下一次测试。

在创作测试之前检查或验证查询似乎是一个很好的想法，这是一个非常简单的过程：

-   从 "运行" 对话框或命令提示符调用 "wbemtest.exe"
-   单击右上角的 "连接" 按钮。
-   在 \\ 右上角再次单击 "连接" 之前，请确保命名空间为 "根 cimv2"。
-   在 "IWbemServices" 下，单击 "查询"
-   在出现的编辑框中输入查询，然后单击 "应用"

注意： "IWbemService" 有多个其他选项可帮助你进行查询。 例如，使用 "Enum 类" 并将单选按钮改为 "递归" 将有助于您查看系统中的所有 WMI 类。

## <a name="span-idretrieving_properties_queried_using_the_wmi_queryspanspan-idretrieving_properties_queried_using_the_wmi_queryspanspan-idretrieving_properties_queried_using_the_wmi_queryspanretrieving-properties-queried-using-the-wmi-query"></a><span id="Retrieving_properties_queried_using_the_WMI_query"></span><span id="retrieving_properties_queried_using_the_wmi_query"></span><span id="RETRIEVING_PROPERTIES_QUERIED_USING_THE_WMI_QUERY"></span>检索使用 WMI 查询查询的属性


现在，你已了解如何在创作测试的同时，为测试方法提供 WMI 查询，以及如何将其作为元数据应用。 还知道如何使用 wbemtest.exe 确认查询是否有效。 现在，让我们看看如何检索所查找的属性值。

检索此信息的基础知识与检索数据驱动测试的值非常类似。 例如，在托管代码中，这将如下所示：

```cpp
1 namespace WEX.Examples
2 {
3     using Microsoft.VisualStudio.TestTools.UnitTesting;
4     using System;
5     using System.Collections;
6     using System.Data;
7     using WEX.Logging.Interop;
8     using WEX.TestExecution;
9
10    [TestClass]
11    public class CSharpWmiDataSourceExample
12    {
13        [TestMethod]
14        [DataSource("WMI:SELECT Description, DesktopInteract, ProcessId FROM Win32_Service WHERE Name='Themes'")]
15        public void ThemesTest()
16        {
17            String description = (String)m_testContext.DataRow["Description"];
18            Boolean desktopInteract = (Boolean)m_testContext.DataRow["DesktopInteract"];
19            UInt32 processId = (UInt32)m_testContext.DataRow["ProcessId"];
20            Log.Comment("Themes service is running on process " + processId.ToString() + " with desktop interact set to "
                           + desktopInteract.ToString());
21            Log.Comment("Themes service description: " + description);
22        }
23        ...
24        public TestContext TestContext
25        {
26            get { return m_testContext; }
27            set { m_testContext = value; }
28        }
29
30        private TestContext m_testContext;
31    }
32}
```

上面示例中的行24-30 是托管数据驱动测试所需的内容。 你定义了 private TestContext 属性并在其上提供了公共 getter 和 setter，以便 TAEF 设置正确的值。 使用 private TestContext 属性，您可以检索从 TAEF 检索到的任何 WMI 查询结果对象属性的当前值。

用于检索 WMI 属性的本机代码非常相似。 与本机数据驱动测试一样，你将使用 TestData 来获取属性值。 例如，让我们考虑一下获取默认打印机的属性的测试。 此测试的头文件作者如下所示：

```cpp
1        // Test on the default printer and its driver name
2        BEGIN_TEST_METHOD(DefaultPrinterTest)
3            TEST_METHOD_PROPERTY(L"DataSource",
              L"WMI:SELECT DriverName, DeviceId, LanguagesSupported FROM Win32_Printer WHERE Default = True")
4        END_TEST_METHOD()
```

为此，在 cpp 文件中，检索代码如下所示：

```cpp
1     void WmiExample::DefaultPrinterTest()
2     {
3         String deviceId;
4         VERIFY_SUCCEEDED(TestData::TryGetValue(L"DeviceId", deviceId));
5
6         String driverName;
7         VERIFY_SUCCEEDED(TestData::TryGetValue(L"DriverName", driverName));
8
9         TestDataArray<unsigned int> languagesSupported;
10        VERIFY_SUCCEEDED(TestData::TryGetValue(L"LanguagesSupported", languagesSupported));
11
12        Log::Comment(L"The default driver is " + deviceId + L" which is a " + driverName);
13        size_t count = languagesSupported.GetSize();
14        for (size_t i = 0; i < count; i++)
15        {
16            Log::Comment(String().Format(L"Language supported: %d", languagesSupported[i]));
17        }
18    }
```

## <a name="span-idaccounting_for_possible_null_property_valuesspanspan-idaccounting_for_possible_null_property_valuesspanspan-idaccounting_for_possible_null_property_valuesspanaccounting-for-possible-null-property-values"></a><span id="Accounting_for_possible_NULL_property_values"></span><span id="accounting_for_possible_null_property_values"></span><span id="ACCOUNTING_FOR_POSSIBLE_NULL_PROPERTY_VALUES"></span>考虑可能的 NULL 属性值


要记住的部分是 WMI 查询不能始终返回非 null 属性。 有时，返回的 WMI 属性值为 "null"。 如果你认为你要查找的属性在某些情况下可能为 "null"，则在验证或尝试使用它之前，请检查是否存在这种情况。

例如，在托管测试代码中，TestContext 将 null 值存储为 DBNull 类型的对象。 在尝试将生成的值强制转换为所需的类型之前，必须检查对象是否为 DBNull 类型。 我们一起来看一下：

```cpp
1 namespace WEX.Examples
2 {
3     using Microsoft.VisualStudio.TestTools.UnitTesting;
4     using System;
5     using System.Collections;
6     using System.Data;
7     using WEX.Logging.Interop;
8     using WEX.TestExecution;
9
10    [TestClass]
11    public class CSharpWmiDataSourceExample
12    {
13        [TestMethod]
14        [DataSource("WMI:SELECT MaximumComponentLength, Availability, DeviceId, DriveType, Compressed
                         FROM Win32_LogicalDisk WHERE DriveType=2 Or DriveType=3")]
15        public void LogicalDiskTest()
16        {
17            UInt32 driveType = (UInt32)m_testContext.DataRow["DriveType"];
18            Log.Comment("DeviceId is " + m_testContext.DataRow["DeviceId"]);
19            Log.Comment("DriveType is " + driveType.ToString());
20
21            object nullCheckCompressed = m_testContext.DataRow["Compressed"];
22            Log.Comment("Compressed's type is: " + nullCheckCompressed.GetType().ToString());
23            if (nullCheckCompressed.GetType() == typeof(DBNull))
24            {
25                Log.Comment("Compressed is NULL");
26            }
27            else
28            {
29                Boolean compressed = (Boolean)nullCheckCompressed;
30                Log.Comment("Compressed is " + compressed.ToString());
31            }
32
33            object nullCheckMaxComponentLength = m_testContext.DataRow["MaximumComponentLength"];
34            if (nullCheckMaxComponentLength.GetType() == typeof(DBNull))
35            {
36                Log.Comment("MaxComponentLength is NULL");
37            }
38            else
39            {
40                UInt32 maxComponentLength = (UInt32)nullCheckMaxComponentLength;
41                Log.Comment("MaxComponentLength is " + maxComponentLength.ToString());
42            }
43
44            object nullCheckAvailability = m_testContext.DataRow["Availability"];
45            if (nullCheckAvailability.GetType() == typeof(DBNull))
46            {
47                Log.Comment("Availability is NULL");
48            }
49            else
50            {
51                UInt32 availability = (UInt32)nullCheckAvailability;
52                Log.Comment("Availability is " + availability.ToString());
53            }
54        }
55        ...
56        public TestContext TestContext
57        {
58            get { return m_testContext; }
59            set { m_testContext = value; }
60        }
61
62        private TestContext m_testContext;
63    }
64}
```

例如，在上面的测试中，在某些情况下，"已压缩"、"MaximumComponentLength" 和 "可用性" 可以为 null (查询返回可移动驱动器，如软盘驱动器) 。 你需要确保在这种情况下测试的行为正确。 为此，请将属性值作为对象检索，并检查它是否为 "DBNull" 类型。 如果是，则表示返回的属性值为 null。 如果不是，则返回的值不为 null，因此有效-因此，将其转换为适当的类型并将其用于测试。

同样，对于本机检索 Api 也是如此，返回的属性值可能为 NULL。 这意味着，需要检查 TestData 是否已成功检索值，而无需使用验证调用 (因为由于值为 null) ，因此无法检索。 例如，你可能有一个依赖于 WMI 查询的测试方法：

```cpp
1        // Test on only local (drive type = 3) or removable (drive type = 2) harddrive
2        BEGIN_TEST_METHOD(LocalOrRemovableHardDriveTest)
3            TEST_METHOD_PROPERTY(L"DataSource", L"WMI:SELECT DeviceId, DriveType, Availability,
                  MaximumComponentLength FROM Win32_LogicalDisk WHERE DriveType=2 OR DriveType=3")
4        END_TEST_METHOD()
```

您可能已将 "可用性" 和 "MaximumComponentLength" 返回为 NULL 值。 因此请编写测试来考虑这一点，如下所示：

```cpp
1     void WmiExample::LocalOrRemovableHardDriveTest()
2     {
3         String deviceId;
4         VERIFY_SUCCEEDED(TestData::TryGetValue(L"DeviceId", deviceId));
5         int driveType;
6         VERIFY_SUCCEEDED(TestData::TryGetValue(L"DriveType", driveType));
7
8         unsigned int maxComponentLength;
9         if (SUCCEEDED(TestData::TryGetValue(L"MaximumComponentLength", maxComponentLength)))
10        {
11            Log::Comment(String().Format(L"MaximumComponentLength: %d", maxComponentLength));
12        }
13
14        unsigned int availability;
15        if (SUCCEEDED(TestData::TryGetValue(L"Availability", availability)))
16        {
17            Log::Comment(String().Format(L"Availability: %d", availability));
18        }
19
20        Log::Comment(L"DeviceId: " + deviceId);
21        Log::Comment(String().Format(L"DriveType: %d", driveType));
22    }
```

 

