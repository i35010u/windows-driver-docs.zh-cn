---
title: WMI 数据源
description: WMI 数据源
ms.assetid: 1C9D0EEC-6542-4249-B7E0-CA3ED63FB120
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1e72d3a653f0b4235e954b00a607c9d05d7b789
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543945"
---
# <a name="wmi-data-source"></a>WMI 数据源


请确保您熟悉基本的 TAEF 执行，并且知道如何使用它，然后继续进行本部分中创建测试。

## <a name="span-idbackgroundspanspan-idbackgroundspanspan-idbackgroundspanbackground"></a><span id="Background"></span><span id="background"></span><span id="BACKGROUND"></span>背景


"WMI"代表"Windows Management Instrumentation"。 使用通用信息模型 (CIM)，这是行业标准来表示系统。 Windows Management Instrumentation 提供统一的方式，用于访问系统管理信息。

## <a name="span-idhowdoesithelpmytestsspanspan-idhowdoesithelpmytestsspanspan-idhowdoesithelpmytestsspanhow-does-it-help-my-tests"></a><span id="How_does_it_help_my_tests_"></span><span id="how_does_it_help_my_tests_"></span><span id="HOW_DOES_IT_HELP_MY_TESTS_"></span>它如何帮助我的测试？


使用作为 TAEF 中 WMI 数据源可用的 WMI 查询支持，您可以将前置条件添加到你的测试，以及获取信息的资源的相关测试计算机上运行你的测试之前。 下面是类型的一些您能够使用 WMI 查询的示例：

-   检查是否在计算机上运行该测试是便携式计算机，并运行测试，仅当它是便携式计算机。
-   检查是否已在测试计算机上安装并运行测试，仅当已被 service pack。
-   检索所有可移动驱动器和测试计算机上的本地硬盘磁盘驱动器并运行测试，以便每个驱动器与查询相匹配。
-   运行测试，仅当测试计算机不是域加入的或
-   仅当测试计算机已加入域，并且检索的域名，请运行测试。

将希望为您提供有关在何处以及如何为您的测试，你可以利用 WMI 数据源的一些思路。 让我们看看如何添加创作 TAEF 测试时此 WMI 查询支持。

您需要使 WMI 数据源测试的测试的唯一特殊元数据是"数据源"。 数据源语法必须如下所示：

```cpp
[DataSource("WMI:<WQL query>")]
```

或在本机代码中：

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"WMI:<WQL query>")]
```

您必须已经注意到数据源值开头"WMI:"它可让 TAEF 知道这确实取决于 WMI 查询结果并也使它从数据驱动测试的测试的数据源。 这是很好的机会，说目前 TAEF 不支持一个测试，以是同时-数据驱动的测试，也取决于 WMI 查询结果的测试。

下一个问题自然是如何编写 WQL 查询的要查找的内容？ WQL 查询语法是非常类似于简化的 SQL 查询。 有一些非常好的示例的查询上提供[ https://msdn2.microsoft.com/library/aa394585(VS.85).aspx。](https://msdn2.microsoft.com/library/aa394585(VS.85).aspx) 以下是几个示例：

<span id="SELECT_Description__DesktopInteract__ProcessId_FROM_Win32_Service_WHERE_Name__Themes_"></span><span id="select_description__desktopinteract__processid_from_win32_service_where_name__themes_"></span><span id="SELECT_DESCRIPTION__DESKTOPINTERACT__PROCESSID_FROM_WIN32_SERVICE_WHERE_NAME__THEMES_"></span>SELECT Description, DesktopInteract, ProcessId FROM Win32\_Service WHERE Name='Themes'  
找出它的描述、 DesktopInteract 和 ProcessId 属性想要使用它在你的测试后，请在"主题"服务中运行测试。

<span id="SELECT_Capabilities__CapabilityDescriptions_FROM_Win32_Printe"></span><span id="select_capabilities__capabilitydescriptions_from_win32_printe"></span><span id="SELECT_CAPABILITIES__CAPABILITYDESCRIPTIONS_FROM_WIN32_PRINTE"></span>选择功能，CapabilityDescriptions 从 Win32\_Printe  
运行测试，以便连接到此计算机每台打印机。 允许测试后，若要访问的功能和 CapabilityDescriptions 的每个打印机。

<span id="SELECT_Name__User__Location_FROM_Win32_StartupCommand"></span><span id="select_name__user__location_from_win32_startupcommand"></span><span id="SELECT_NAME__USER__LOCATION_FROM_WIN32_STARTUPCOMMAND"></span>选择名称、 用户、 位置从 Win32\_StartupCommand  
运行测试，以便获取在 Windows 启动时运行每个进程。 对于每个进程让测试知道进程名称是什么，其中是位于 （位置），以及用户作为进程运行。

可以如下所示的.cs 文件和标头文件中已打开的示例以及上述文档中找到更多示例。 简化的常规语法如下所示：

```cpp
SELECT <comma separated properties> FROM <WMI Class name> [WHERE <add condition on some properties>]
```

在示例，您刚才看到的而 Win32\_服务、 Win32\_打印机和 Win32\_StartupCommand 是所有的 WMI 类。 您可以查看哪些测试此处感兴趣的 WMI 类： [ https://msdn2.microsoft.com/library/aa394554(VS.85).aspx。](https://msdn2.microsoft.com/library/aa394554(VS.85).aspx)

TAEF 不支持检索系统属性。

在场景的背面 TAEF 将为您执行查询，并确认结果。 如果查询返回至少一个对象，获取为每个返回的对象执行测试。 如果 WQL 查询不返回任何对象，该测试使用此信息获取记录为已阻止并执行转到下一个测试。

检查或创作你的测试之前验证您的查询似乎是不错的选择，并且是一个非常简单的过程：

-   从运行对话框或命令提示符调用"wbemtest.exe"
-   单击右上角上的"连接"按钮。
-   请确保你的命名空间是"根\\cimv2"之前再次在右上角单击"连接"。
-   在"iwbemservices 下面"，单击"查询"
-   显示并单击"应用"编辑框中输入您的查询

注意："IWbemService"具有多个其他选项，能够帮助您解决您的查询。 例如，使用"枚举类"，并将单选按钮更改为"递归"将帮助您在系统上看到的所有 WMI 类。

## <a name="span-idretrievingpropertiesqueriedusingthewmiqueryspanspan-idretrievingpropertiesqueriedusingthewmiqueryspanspan-idretrievingpropertiesqueriedusingthewmiqueryspanretrieving-properties-queried-using-the-wmi-query"></a><span id="Retrieving_properties_queried_using_the_WMI_query"></span><span id="retrieving_properties_queried_using_the_wmi_query"></span><span id="RETRIEVING_PROPERTIES_QUERIED_USING_THE_WMI_QUERY"></span>检索使用 WMI 查询进行查询的属性


现在可以了解如何附带测试方法的 WMI 查询以及如何将测试创作时将其应用作为元数据。 您还知道如何确认查询有效使用 wbemtest.exe。 现在让我们看看如何检索所需的属性值。

检索此信息的基础知识是非常类似于检索值的数据驱动测试。 例如，在托管代码中这将如下所示：

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
14        [DataSource("WMI:SELECT Description, DesktopInteract, ProcessId FROM Win32_Service WHERE Name=&#39;Themes&#39;")]
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

在上面的示例行 24-30 是完全托管的数据驱动测试的要求。 定义了一个专用的 TestContext 属性和提供公共 getter 和 setter 上为 TAEF 设置正确的值。 使用专用的 TestContext 属性，您可以检索任何 TAEF 中检索到的 WMI 查询结果对象的属性的当前值。

检索 WMI 属性的本机代码是非常相似。 像使用本机数据驱动的测试，你将使用 TestData 获取属性值。 例如，让我们考虑用于获取属性的默认打印机的测试。 标头文件编写此测试如下所示：

```cpp
1        // Test on the default printer and its driver name
2        BEGIN_TEST_METHOD(DefaultPrinterTest)
3            TEST_METHOD_PROPERTY(L"DataSource",
              L"WMI:SELECT DriverName, DeviceId, LanguagesSupported FROM Win32_Printer WHERE Default = True")
4        END_TEST_METHOD()
```

为此，我们 cpp 文件中的检索代码如下所示：

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

## <a name="span-idaccountingforpossiblenullpropertyvaluesspanspan-idaccountingforpossiblenullpropertyvaluesspanspan-idaccountingforpossiblenullpropertyvaluesspanaccounting-for-possible-null-property-values"></a><span id="Accounting_for_possible_NULL_property_values"></span><span id="accounting_for_possible_null_property_values"></span><span id="ACCOUNTING_FOR_POSSIBLE_NULL_PROPERTY_VALUES"></span>有关可能的 NULL 属性值的记帐


需要注意的部分是 WMI 查询可能会始终返回非 null 属性。 可能有的时间时返回的 WMI 属性值为"null"。 如果您认为您正在寻找的属性可能是"null"，在某些情况下，则验证或尝试使用它之前检查它。

在托管测试代码，如 TestContext 将为 DBNull 类型的对象存储 null 值。 必须检查 DBNull 类型的对象是否尝试强制转换为类型结果值之前在预期进行。 让我们来看：

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
22            Log.Comment("Compressed&#39;s type is: " + nullCheckCompressed.GetType().ToString());
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

例如，在上述测试中，"压缩"、"MaximumComponentLength"和"可用性"可以为 null 在某些情况下 （当该查询将返回如软盘驱动器的可移动驱动器）。 你想要确保测试在这种情况下正确行为。 为达到此目的，检索属性值作为对象并检查它是否为类型"DBNull"。 如果是，这意味着返回的属性值为 null。 如果不是，返回的值不为 null，因此有效-因此将其转换为合适的类型，并使用它进行测试。

这同样适用以及本机检索 Api-返回的属性值可以为 NULL。 这意味着您需要检查是否 TestData 成功检索值而无需使用验证调用 （因为无法检索可能是因为值为 null）。 例如，您可能必须依赖于 WMI 查询的测试方法：

```cpp
1        // Test on only local (drive type = 3) or removable (drive type = 2) harddrive
2        BEGIN_TEST_METHOD(LocalOrRemovableHardDriveTest)
3            TEST_METHOD_PROPERTY(L"DataSource", L"WMI:SELECT DeviceId, DriveType, Availability,
                  MaximumComponentLength FROM Win32_LogicalDisk WHERE DriveType=2 OR DriveType=3")
4        END_TEST_METHOD()
```

您可能有"可用性和"MaximumComponentLength"返回为 NULL 值。 因此编写测试，因此考虑此类似：

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

 

 





