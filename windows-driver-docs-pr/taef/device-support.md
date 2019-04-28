---
title: 设备支持
description: 设备支持
ms.assetid: 41316BB1-0AE0-4100-AE7B-0014FE9FD0E7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fef842911670299c4df585aed6a799023bcabcd6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341181"
---
# <a name="device-support"></a>设备支持


如果您的测试自动化依赖于存在的设备或测试资源，请参考示例 TestResourceExample，并按照如何利用设备支持或 TAEF 中可用的资源支持的测试。 请确保您熟悉如何创建在继续之前使用 TAEF 和 TAEF 基本执行基本测试。

## <a name="span-idauthoringfordevicesupport-sourcesfilespanspan-idauthoringfordevicesupport-sourcesfilespanspan-idauthoringfordevicesupport-sourcesfilespanauthoring-for-device-support---sources-file"></a><span id="Authoring_for_device_support_-_Sources_file"></span><span id="authoring_for_device_support_-_sources_file"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_SOURCES_FILE"></span>创作的设备支持的源文件


除了需要创作 TAEF 中的为测试其他库需要 Te.Common.lib。

## <a name="span-idauthoringfordevicesupport-testresourcedefinitionspanspan-idauthoringfordevicesupport-testresourcedefinitionspanspan-idauthoringfordevicesupport-testresourcedefinitionspanauthoring-for-device-support---test-resource-definition"></a><span id="Authoring_for_device_support_-_Test_Resource_definition"></span><span id="authoring_for_device_support_-_test_resource_definition"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_TEST_RESOURCE_DEFINITION"></span>创作的设备支持的测试资源定义


用户负责创建其自己的测试资源 （设备） 定义。 若要执行此操作，需要实现 ITestResource。 ITestResource ITestResource.h 在已发布的标头文件中定义，如下所示：

```cpp
namespace WEX { namespace TestExecution
{
    namespace TestResourceProperty
    {
        // the following are reserved and must have properties for any TestResource definition
        static const wchar_t c_szName[] = L"Name";
        static const wchar_t c_szId[] = L"Id";
        static const wchar_t c_szGuid[] = L"GUID";
        static const wchar_t c_szType[] = L"Type";
    }

    struct __declspec(novtable) __declspec(uuid("79098e4c-b78d-434b-854d-2b59f5c4acc5")) ITestResource : public IUnknown
    {
    public:
        virtual HRESULT STDMETHODCALLTYPE GetGuid(GUID* pGuid) = 0;
        virtual HRESULT STDMETHODCALLTYPE SetGuid(GUID guid) = 0;
        virtual HRESULT STDMETHODCALLTYPE GetValue(BSTR name, BSTR* pValue) = 0;
        virtual HRESULT STDMETHODCALLTYPE SetValue(BSTR name, BSTR value) = 0;
    };
} /*namespace TestExecution*/ } /*namespace WEX*/
```

在本示例中，类 MyTestResource 实现 ITestResource COM 接口。 在 ITestResource.h，您还将找到"必须具备"属性定义的列表。 它应该可以获取使用 GetGuid(..) 和名称、 Id 和资源使用 GetValue(...) 类型的测试资源的 GUID。如果上述任一缺少 TestResource，TAEF 将 consisder 中无效，并不维护它的信息。（请参阅后面的"构建资源列表"部分）。

## <a name="span-idauthoringfordevicesupport-specifyingresourcedependentmetadataspanspan-idauthoringfordevicesupport-specifyingresourcedependentmetadataspanspan-idauthoringfordevicesupport-specifyingresourcedependentmetadataspanauthoring-for-device-support---specifying-resource-dependent-metadata"></a><span id="Authoring_for_device_support_-_Specifying_resource_dependent_metadata"></span><span id="authoring_for_device_support_-_specifying_resource_dependent_metadata"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_SPECIFYING_RESOURCE_DEPENDENT_METADATA"></span>创作的设备支持-指定资源依赖于元数据


若要指定测试模块具有测试资源相关的测试方法，模块级元数据属性**TestResourceDependent"** 必须设置为"true"。 通过测试模块中的所有类以及这些类中的所有测试方法，获取继承属性。 如果任何模块中的测试方法是不进行测试的资源依赖，则它应显式重新设置为 false 的元数据值。 所有其他依赖于测试资源的测试方法必须提供使用测试资源的"Id"和/或"类型"选择查询。

以下是一些快速示例"ResourceSelection"为我们的示例资源列表和每个表示：

-   "@Id= HD\*'": 与"HD"开头的 Id 相匹配的每个资源
-   "@Type= PCI": 匹配每个资源类型"PCI"
-   "@Id= PCI\*' OR @Id= HD\*'": 匹配开头"PCI"或以"HD"开头的每个资源
-   "@Type= PCI 和@id=\*37'": 与以"37"结尾的名称相匹配每个资源类型"PCI"之一

在示例代码中，这种情况，如下所示：

```cpp
BEGIN_MODULE()
    MODULE_PROPERTY(L"TestResourceDependent", L"true")
END_MODULE()

    class TestResourceExample
    {
        TEST_CLASS(TestResourceExample);

        BEGIN_TEST_METHOD(NoTestResourceTest)
            TEST_METHOD_PROPERTY(L"TestResourceDependent", L"false")
        END_TEST_METHOD()

        BEGIN_TEST_METHOD(OneHDAudioTest)
            TEST_METHOD_PROPERTY(L"ResourceSelection", L"@Id='HD*'")
        END_TEST_METHOD()

        ...

        BEGIN_TEST_METHOD(HDorPCITest)
            TEST_METHOD_PROPERTY(L"ResourceSelection", L"@Id='PCI*' OR @Id='HD*'")
        END_TEST_METHOD()
        ...
    };
```

在上面的示例中，您将看到的模块已标记为"TestResourceDependent"。 NoTestResourceTest 显式设置为"false"的"TestRssourceDependent"元数据标记为不依赖于任何测试资源。 所有其他测试方法指定他们感兴趣的执行的测试资源选择条件。

选择条件语法是非常类似于可供 TAEF 的命令行选择查询语法。 对于资源选择但是，它是限制为使用的资源 Id 和类型。 由于资源 Id 是一个字符串，它必须括在单引号。 可以使用通配符"\*"？"在指定的 Id 值。 在我们上面示例中，在 OneHDAudioTest，资源选择指定与匹配的 Id 与 HD 的开始位置的任何资源。 同样，对于 HDorPCITest，资源选择将匹配 Id 的开头为 HD 或 PCI 开头的任何资源。 务必要注意选择的资源并不区分大小写的即 pci，Pci 和 PCI 都将被视为相同。

基于对资源所选内容，TAEF 将重新调用测试方法，以及测试级别设置和清理方法 （如果已指定） 一次为每个与选定范围的测试资源。 以下各节将介绍如何指定资源的列表，并将其提供给 TAEF 和测试方法如何检索下一节中的资源的详细信息。

## <a name="span-idauthoringfordevicesupport-buildingtheresourcelistspanspan-idauthoringfordevicesupport-buildingtheresourcelistspanspan-idauthoringfordevicesupport-buildingtheresourcelistspanauthoring-for-device-support---building-the-resource-list"></a><span id="Authoring_for_device_support_-_Building_the_resource_list"></span><span id="authoring_for_device_support_-_building_the_resource_list"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_BUILDING_THE_RESOURCE_LIST"></span>创作的设备支持-构建资源列表


只要 TAEF 遇到 TestResourceDependent 测试模块，它将查找并调用 dll 导出方法 BuildResourceList。 它是在 BuildResourceList 其中用户可以创建新的测试资源并将其添加到获取中作为参数传递到 BuildResourceList 接口的实现。 在本示例中，让我们看一看此方法的实现：

```cpp
using namespace WEX::TestExecution;
HRESULT __cdecl BuildResourceList(ResourceList& resourceList)
{
    Log::Comment(L"In BuildResourceList");

    GUID myGuid;
    VERIFY_SUCCEEDED(::CoCreateGuid(&myGuid));

    CComPtr<ITestResource> spTestResource;
    spTestResource.Attach(new MyTestResource(L"HDAudio1", L"HDAudio-deviceid-1", myGuid, L"HD"));
    resourceList.Add(spTestResource);

    spTestResource.Attach(new MyTestResource(L"HDAudio2", L"HDAudio-deviceid-2", myGuid, L"HD"));
    resourceList.Add(spTestResource);

    spTestResource.Attach(new MyTestResource(L"PCI1", L"PCI-deviceid-1", myGuid, L"PCI"));
    resourceList.Add(spTestResource);

    spTestResource.Attach(new MyTestResource(L"PCI2", L"PCI-deviceid-2", myGuid, L"PCI"));
    resourceList.Add(spTestResource);

    spTestResource.Attach(new MyTestResource(L"PCI3", L"PCI-deviceid-3", myGuid, L"PCI"));
    resourceList.Add(spTestResource);

    return S_OK;
}
```

BuildResourceList 作为其参数接受对 WEX::TestExecution::ResourceList 的引用。 ResourceList ResourceList.h 在已发布的标头文件中定义。 ResourceList 上使用 add （...） 方法，用户可以添加所有测试资源发现或创建 TAEF 来管理和使用。 上面的示例添加 5 个此类测试资源。

如果要添加的测试资源将无法返回资源的"名称"、"Id"、"类型"或 GUID，Add 方法将失败。

ResourceList 将保持不变的整个生存期的测试模块-即，直到完成所有测试方法和清理方法正在执行。 如果 BuildResourceList 返回失败 HRESULT 值，测试模块中的所有资源相关的测试方法都将都记录为阻止而不执行。 而不考虑将执行所有非测试资源。

BuildResourceList 测试模块中的任何其他方法之前调用。 （在 BuildResourceList) 生成资源列表后，"ResourceSelection"元数据用于匹配资源列表中的可用资源。 如果找到匹配项后, 跟该测试方法本身调用所有安装程序方法 （模块、 类、 测试顺序）。 每个测试在调用后调用测试级别的清理方法。

在后台，TAEF 保留对其应用资源选择 ResourceList。 例如，对于 OneHDAudioTest 测试方法，具有 Id"HDAudio-deviceid-1"和"HDAudio deviceid 2"测试资源将同时匹配 HD\*并为每个测试方法将重新调用通过 TAEF （一次为每个）。 此外将隐式索引与测试的每个调用相关联。 您还会看到&lt;命名空间限定符&gt;OneHDAudioTest\#0 并&lt;命名空间限定符&gt;OneHDAudioTest\#1 作为两次调用。

## <a name="span-idauthoringfordevicesupport-retrievingthedeviceinatestmethodspanspan-idauthoringfordevicesupport-retrievingthedeviceinatestmethodspanspan-idauthoringfordevicesupport-retrievingthedeviceinatestmethodspanauthoring-for-device-support---retrieving-the-device-in-a-test-method"></a><span id="Authoring_for_device_support_-_Retrieving_the_device_in_a_test_method"></span><span id="authoring_for_device_support_-_retrieving_the_device_in_a_test_method"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_RETRIEVING_THE_DEVICE_IN_A_TEST_METHOD"></span>创作的设备支持-检索测试方法中的设备


前面几节介绍了如何在模块、 类和测试方法级别添加必要的元数据。 他们还了解了如何定义自定义测试资源以及如何将它们添加到 ResourceList BuildResourceList 的实现中。 后面的下一步部分正在检索测试方法中的资源。 在本示例中，让我们看一下简单的测试方法之一：

```cpp
1   void TestResourceExample::OneHDAudioTest()
2   {
3       Log::Comment(L"In HD audio test");
4       size_t count = Resources::Count();
5       size_t index = 0;
6       VERIFY_ARE_EQUAL(count, (index + 1));
7
8       CComPtr<ITestResource> spTestResource;
9       VERIFY_SUCCEEDED(Resources::Item(index, &spTestResource));
10
11      // Get Resource Id
12      CComBSTR value;
13      VERIFY_SUCCEEDED(spTestResource->GetValue(CComBSTR(TestResourceProperty::c_szId), &value));
14      Log::Comment(L"Resource Id is " + String(value));
15  }
```

在 OneHDAudioTest，资源选择其中的资源 Id 开头 HD 一次选择一个测试资源。 静态资源 ResourceList.h 中定义的类提供用于检索计数，以及在任何给定调用的测试过程中可用的实际资源的 Api。 在这种情况下，您可以看到行 4、 9 和 13 在上面的示例中，资源:: count （） 提供的测试在测试方法的当前调用过程中可用的资源数的计数。 在此测试方法中，这应为 1。 可以使用 TAEF (Verify.h) 中可用的验证宏来验证此值。 您知道，如果任一验证调用失败异常基于 TAEF 测试中，执行将在该点终止，并且测试方法将标记为失败。

接下来，使用 Resources::Item(...)API 并传入要检索的资源 （在这种情况下调用期间，只能有一个测试资源将可用，因为索引将始终为 0），可以检索测试资源的索引。 根据所需的测试，测试方法可以进一步使用检索到的测试资源。

所有测试方法中后面是相同的基本原则。 在此示例以获取更好地了解看看其他测试方法。

## <a name="span-idexecutingatestresourcedependenttestmodulespanspan-idexecutingatestresourcedependenttestmodulespanspan-idexecutingatestresourcedependenttestmodulespanexecuting-a-test-resource-dependent-test-module"></a><span id="Executing_a_test_resource_dependent_test_module"></span><span id="executing_a_test_resource_dependent_test_module"></span><span id="EXECUTING_A_TEST_RESOURCE_DEPENDENT_TEST_MODULE"></span>执行测试的资源依赖测试模块


使用测试资源依赖测试现在编写和构建，你现在可以执行它使用 TAEF。 需要注意的关键一点是，TestResourceDependent 测试只能执行进程。 这意味着，即使未显式指定 **"/ inproc"** 开关，它会在将添加只要 TAEF 发现测试资源依赖测试模块。 如您所知，可以在给定 TAEF 执行过程中执行只能有一个测试模块中的测试时"/ inproc"有开关，则。 这意味着如果测试模块依赖的资源，不能指定多个测试模块在命令行。

若要实际在我们测试模块中执行所有测试，您可以只需运行：

``` syntax
te Examples\Cpp.TestResource.Example.dll
```

只需获取的所有测试方法调用和数据和元数据组合的列表而不实际运行测试方法的有用方法是使用 **/listproperties**在命令行开关。 让我们看看输出。

``` syntax
te Examples\Cpp.TestResource.Example.dll /listproperties

Test Authoring and Execution Framework v2.9.3k for x86
In BuildResourceList
Verify: SUCCEEDED(::CoCreateGuid(&myGuid))

        f:\toolsdev.binaries.x86chk\WexTest\CuE\TestExecution\Examples\Cpp.TestResource.Example.dll
                Property[TestResourceDependent] = true

            WEX::TestExecution::Examples::TestResourceExample
                WEX::TestExecution::Examples::TestResourceExample::NoTestResourceTest
                        Property[TestResourceDependent] = false

                WEX::TestExecution::Examples::TestResourceExample::OneHDAudioTest#0
                        Property[ResourceSelection] = @Id='HD*' 
                
                            Resource#0
                                Id = HDAudio-deviceid-1
                                Name = HDAudio1
                                Type = HD

                WEX::TestExecution::Examples::TestResourceExample::OneHDAudioTest#1
                        Property[ResourceSelection] = @Id='HD*'
                        
                            Resource#0
                                Id = HDAudio-deviceid-2
                                Name = HDAudio2
                                Type = HD

                WEX::TestExecution::Examples::TestResourceExample::OnePCIDeviceTest#0
                        Property[ResourceSelection] = @Id='PCI*'
                        
                            Resource#0
                                Id = PCI-deviceid-1
                                Name = PCI1
                                Type = PCI

                WEX::TestExecution::Examples::TestResourceExample::OnePCIDeviceTest#1
                        Property[ResourceSelection] = @Id='PCI*'
                        
                            Resource#0
                                Id = PCI-deviceid-2
                                Name = PCI2
                                Type = PCI

                WEX::TestExecution::Examples::TestResourceExample::OnePCIDeviceTest#2
                         Property[ResourceSelection] = @Id='PCI*'
                        
                            Resource#0
                                Id = PCI-deviceid-3
                                Name = PCI3
                                Type = PCI

                WEX::TestExecution::Examples::TestResourceExample::HDorPCITest#0
                        Property[ResourceSelection] = @Id='PCI*' OR @Id='HD*'
                        
                            Resource#0
                                Id = HDAudio-deviceid-1
                                Name = HDAudio1
                                Type = HD

                WEX::TestExecution::Examples::TestResourceExample::HDorPCITest#1
                         Property[ResourceSelection] = @Id='PCI*' OR @Id='HD*'
                        
                            Resource#0
                                Id = HDAudio-deviceid-2
                                Name = HDAudio2
                                Type = HD

                WEX::TestExecution::Examples::TestResourceExample::HDorPCITest#2
                         Property[ResourceSelection] = @Id='PCI*' OR @Id='HD*'
                        
                            Resource#0
                                Id = PCI-deviceid-1
                                Name = PCI1
                                Type = PCI

                WEX::TestExecution::Examples::TestResourceExample::HDorPCITest#3
                         Property[ResourceSelection] = @Id='PCI*' OR @Id='HD*'
                        
                            Resource#0
                                Id = PCI-deviceid-2
                                Name = PCI2
                                Type = PCI

                WEX::TestExecution::Examples::TestResourceExample::HDorPCITest#4
                         Property[ResourceSelection] = @Id='PCI*' OR @Id='HD*'
                        
                            Resource#0
                                Id = PCI-deviceid-3
                                Name = PCI3
                                Type = PCI

                WEX::TestExecution::Examples::TestResourceExample::PCI1AudioTest #0
                         Property[ResourceSelection] = @Id='PCI*' AND @Id='*1'
                        
                            Resource#0
                                Id = PCI-deviceid-1
                                Name = PCI1
                                Type = PCI
```

测试资源 depent 每次调用期间添加到测试方法名称的隐式索引的通知获取测试方法。 ResourceSelection 属性显示跟一系列将可供就可以使用它们的顺序中的测试方法的所有资源。 例如，对于第三个调用 HDAudioHDAudioPCITest (HDAudioHDAudioPCITest\#2)，HDAudio deviceid 1 将 Resources::Item(...) 中索引 0 处可用的资源。

你可以更细致地指出你感兴趣使用命令行选择查询语言中 TAEF 提供哪些测试调用。 若要选择的测试方法测试资源"PCI 的 deviceid-3"已上市的所有调用示例，可以使用选择条件：

``` syntax
te Examples\Cpp.TestResource.Example.dll /list
          /select:"@Resource:Id='PCI-deviceid-3'"

Test Authoring and Execution Framework v2.9.3k for x86
In BuildResourceList
Verify: SUCCEEDED(::CoCreateGuid(&myGuid))

        f: \Examples\Cpp.TestResource.Example.dll
            WEX::TestExecution::Examples::TestResourceExample
                WEX::TestExecution::Examples::TestResourceExample::OnePCIDeviceTest#2
                WEX::TestExecution::Examples::TestResourceExample::HDorPCITest#4
```

同样，若要按名称 （请注意测试方法名称是追加最后调用索引以及完全限定） 选择特定测试方法，可以按如下所示使用所选内容查询：

``` syntax
te Examples\Cpp.TestResource.Example.dll /name:*OneHDAudioTest#1
Test Authoring and Execution Framework v2.2 Build 6.1.7689.0 (release.091218-1251) for x86

Discovered a test resource dependent test module. Assuming /InProc execution.

In BuildResourceList
Verify: SUCCEEDED(::CoCreateGuid(&myGuid))

StartGroup: WEX::TestExecution::Examples::TestResourceExample::OneHDAudioTest#1
In HD audio test
Verify: AreEqual(count, (index + 1))
Verify: SUCCEEDED(Resources::Item(index, &spTestResource))
Verify: SUCCEEDED(spTestResource->GetValue(CComBSTR(TestResourceProperty::c_szId), &value))
Resource Id is HDAudio-deviceid-2
WEX::TestExecution::Examples::TestResourceExample::OneHDAudioTest#1 [Passed]

Summary: Total=1, Passed=1, Failed=0, Blocked=0, Not Run=0, Skipped=0
```

请注意隐式进程内添加上面的示例中的第三个行中的警告。 上面的选择查询必须与所选内容查询相同的效果：**/选择:"@Name='\*OneHDAudio\*和@Resource:Index= 1"**。 还有可能选择使用其名称或类型 （或 Id 如上所示） 的资源。 例如， **/选择:"@Name='\*PCIHDAudioTest\*和@Resource:Name= PCI3"** 将选择测试方法 PCIHDAudioTest\#4 和 PCIHDAudioTest\#5。

尝试这些和其他选择查询的命令提示符处是留给大家练练手为读取器。

 

 





