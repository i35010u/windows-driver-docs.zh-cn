---
title: 设备支持
description: 设备支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a15173d94989c9ac3919012133d73b08ccd38fc1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840467"
---
# <a name="device-support"></a>设备支持


如果测试自动化依赖于设备或测试资源的存在，请参阅示例 TestResourceExample，并按如何利用 TAEF 中提供的设备支持或测试资源支持。 请确保熟悉如何使用 TAEF 创建基本测试和 TAEF 的基本执行，然后再继续。

## <a name="span-idauthoring_for_device_support_-_sources_filespanspan-idauthoring_for_device_support_-_sources_filespanspan-idauthoring_for_device_support_-_sources_filespanauthoring-for-device-support---sources-file"></a><span id="Authoring_for_device_support_-_Sources_file"></span><span id="authoring_for_device_support_-_sources_file"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_SOURCES_FILE"></span>设备支持的创作-源文件


Te 除了需要其他库，还需要在 TAEF 中创作测试。

## <a name="span-idauthoring_for_device_support_-_test_resource_definitionspanspan-idauthoring_for_device_support_-_test_resource_definitionspanspan-idauthoring_for_device_support_-_test_resource_definitionspanauthoring-for-device-support---test-resource-definition"></a><span id="Authoring_for_device_support_-_Test_Resource_definition"></span><span id="authoring_for_device_support_-_test_resource_definition"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_TEST_RESOURCE_DEFINITION"></span>创作设备支持-测试资源定义


用户负责创建自己的测试资源 (设备) 定义。 为此，需要实现 ITestResource。 ITestResource 在已发布的头文件 ITestResource 中定义，如下所示：

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

在本示例中，类 MyTestResource 实现了 ITestResource COM 接口。 在 ITestResource 中，还会找到定义了 "必须具有" 属性的列表。 应该可以使用 GetGuid ( 获取测试资源的 GUID。使用 GetValue ( ... ) ) 和名称、Id 和类型。如果 TestResource 中缺少任何一个，则 TAEF 会将其 consisder 为无效，并且不保留其信息。 (参阅) 的 "构建资源列表" 一节。

## <a name="span-idauthoring_for_device_support_-_specifying_resource_dependent_metadataspanspan-idauthoring_for_device_support_-_specifying_resource_dependent_metadataspanspan-idauthoring_for_device_support_-_specifying_resource_dependent_metadataspanauthoring-for-device-support---specifying-resource-dependent-metadata"></a><span id="Authoring_for_device_support_-_Specifying_resource_dependent_metadata"></span><span id="authoring_for_device_support_-_specifying_resource_dependent_metadata"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_SPECIFYING_RESOURCE_DEPENDENT_METADATA"></span>设备支持的创作-指定资源相关的元数据


为了指定测试模块具有测试资源相关测试方法，必须将模块级元数据属性 **"TestResourceDependent"** 设置为 "true"。 此属性由测试模块中的所有类以及这些类中的所有测试方法继承。 如果模块中的测试方法中有任何一个依赖于测试资源，则应将元数据值显式重新设置为 false。 依赖于测试资源的所有其他测试方法必须使用测试资源的 "Id" 和/或 "Type" 提供选择查询。

下面是示例资源列表的一些快速示例 "ResourceSelection"，其中每个示例都表示：

-   " @Id = ' HD \* '"：匹配 Id 以 "hd" 开头的每个资源
-   " @Type = ' Pci '"：匹配类型为 "pci" 的每个资源
-   " @Id = ' Pci \* ' 或 @Id = ' hd \* '"：匹配以 "pci" 开头或以 "hd" 开头的每个资源
-   " @Type = ' Pci ' and @id = ' \* 37 '"：匹配类型为 "pci"、名称以 "37" 结尾的每个资源

在我们的示例代码中，如下所示：

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

在上面的示例中，你将看到模块标记为 "TestResourceDependent"。 通过将 "TestRssourceDependent" 元数据设置为 "false"，可将 NoTestResourceTest 显式标记为不依赖于任何测试资源。 所有其他测试方法均为其对执行所需的测试资源指定选择条件。

选择条件语法与可用于 TAEF 的命令行选择查询语法非常类似。 但在资源选择时，限制使用资源 Id 的和类型。 由于资源 Id 是一个字符串，因此需要用单引号引起来。 可以 \* 在 Id 值规范中使用通配符 "" 或 "？"。 在上面的示例中，在 OneHDAudioTest 中，资源选择指定与 Id 以 "HD" 开头的任何资源匹配。 同样，如果是 HDorPCITest，则资源选择将匹配 Id 以 "HD" 开头或以 "PCI" 开头的任何资源。 请务必注意，资源选择不区分大小写，即，"pci"、"Pci" 和 "PCI" 将全部视为相同的。

根据资源选择，TAEF 将重新调用测试方法，并将测试级别的设置和清理方法) 指定给每个与所选内容匹配的测试资源 (。 以下各节将介绍有关如何指定资源列表并将其提供给 TAEF 的详细信息，以及测试方法可以如何检索下一部分中的资源的详细信息。

## <a name="span-idauthoring_for_device_support_-_building_the_resource_listspanspan-idauthoring_for_device_support_-_building_the_resource_listspanspan-idauthoring_for_device_support_-_building_the_resource_listspanauthoring-for-device-support---building-the-resource-list"></a><span id="Authoring_for_device_support_-_Building_the_resource_list"></span><span id="authoring_for_device_support_-_building_the_resource_list"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_BUILDING_THE_RESOURCE_LIST"></span>创作设备支持-生成资源列表


TAEF 遇到 TestResourceDependent 测试模块后，它将查找并调用 dll 导出的方法 BuildResourceList。 它位于 BuildResourceList 的实现中，用户可以在其中创建新的测试资源，并将其添加到作为参数传入到 BuildResourceList 的接口。 在本示例中，让我们看一下此方法的实现：

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

BuildResourceList 接受对 WEX：： Testexecution.completed：： ResourceList 作为其参数的引用。 ResourceList 在已发布的头文件 ResourceList 中定义。 用户可以使用 ResourceList 上的 "添加 ( ..." ) 方法，添加发现或为 TAEF 创建的所有测试资源，以管理和使用。 上面的示例添加了5个这样的测试资源。

如果要添加的测试资源未能返回资源的 "名称"、"Id"、"类型" 或 GUID，Add 方法将失败。

将通过测试模块的生存期维护 ResourceList，即直到所有测试方法和清理方法执行完毕。 如果 BuildResourceList 返回失败的 HRESULT 值，则会将测试模块中的所有资源相关测试方法记录为 "已阻止"，而不执行。 不管如何，都将执行所有非测试资源。

在测试模块中的任何其他方法之前调用 BuildResourceList。  (在 BuildResourceList) 中生成资源列表后，将使用 "ResourceSelection" 元数据来匹配资源列表中的可用资源。 如果找到匹配项，则会调用所有安装方法， (模块、类、测试顺序) ，然后调用测试方法本身。 测试级别清理方法在每次测试调用后调用。

在幕后，TAEF 将保留应用资源选择的 ResourceList。 例如，对于 OneHDAudioTest 测试方法，Id 为 "HDAudio" 和 "HDAudio" 的测试资源将与 "HD" 匹配，每个都将为 \* 每个) 重新 (调用一次该测试方法。 还会有一个与每个测试调用关联的隐式索引。 因此，您将看到 &lt; 命名空间限定符 &gt; OneHDAudioTest \# 0， &lt; 命名空间限定符 &gt; OneHDAudioTest \# 1 作为两次调用。

## <a name="span-idauthoring_for_device_support_-_retrieving_the_device_in_a_test_methodspanspan-idauthoring_for_device_support_-_retrieving_the_device_in_a_test_methodspanspan-idauthoring_for_device_support_-_retrieving_the_device_in_a_test_methodspanauthoring-for-device-support---retrieving-the-device-in-a-test-method"></a><span id="Authoring_for_device_support_-_Retrieving_the_device_in_a_test_method"></span><span id="authoring_for_device_support_-_retrieving_the_device_in_a_test_method"></span><span id="AUTHORING_FOR_DEVICE_SUPPORT_-_RETRIEVING_THE_DEVICE_IN_A_TEST_METHOD"></span>创作设备支持-在测试方法中检索设备


前面几节介绍了如何在模块、类和测试方法级别添加必要的元数据。 它们还介绍了如何定义自定义测试资源，以及如何将它们添加到 BuildResourceList 实现中的 ResourceList。 接下来的下一部分是检索测试方法中的资源。 让我们看一下我们的示例中的一个简单的测试方法：

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

在 OneHDAudioTest 中，资源选择在资源 Id 以 "HD" 开头的一次选择一个测试资源。 ResourceList 中定义的静态类资源提供了用于检索计数的 Api，以及在测试的任何给定调用期间可用的实际资源。 在这种情况下，如上面的示例中所示，在上面的示例中，资源：： Count ( # A1 提供了在当前调用测试方法期间可用的测试资源数。 在此测试方法中，此项应为1。 可以通过使用 TAEF 中提供的验证宏 (验证 .h) 来验证此值。 如您所知，如果任何验证调用在基于异常的 TAEF 测试中失败，则执行将在该点终止，并将测试方法标记为失败。

接下来，使用 resource：： Item ( ... ) API 并传入检索 (资源的索引，在这种情况下，因为在调用期间仅有一个测试资源可用，所以索引将始终为 0) ，你可以检索测试资源。 测试方法可以进一步使用检索到的测试资源，因为它需要进行测试。

所有测试方法都遵循相同的基本原则。 请查看示例中的其他测试方法，以更好地了解。

## <a name="span-idexecuting_a_test_resource_dependent_test_modulespanspan-idexecuting_a_test_resource_dependent_test_modulespanspan-idexecuting_a_test_resource_dependent_test_modulespanexecuting-a-test-resource-dependent-test-module"></a><span id="Executing_a_test_resource_dependent_test_module"></span><span id="executing_a_test_resource_dependent_test_module"></span><span id="EXECUTING_A_TEST_RESOURCE_DEPENDENT_TEST_MODULE"></span>执行测试资源相关测试模块


现在创作和生成测试资源相关测试后，可以使用 TAEF 执行该测试。 需要注意的要点是只能以 inproc 执行 TestResourceDependent 测试。 这意味着，即使你未显式指定 **"/inproc"** 开关，它也会在 TAEF 发现测试资源相关测试模块后立即添加。 如您所知，在出现 "/inproc" 开关时，只能在给定的 TAEF 执行中执行一个测试模块的测试。 这意味着，如果测试模块依赖于资源，则不能在命令行中指定多个测试模块。

若要实际执行测试模块中的所有测试，只需运行：

``` syntax
te Examples\Cpp.TestResource.Example.dll
```

若要获取所有测试方法调用的列表以及数据和元数据组合的列表，而无需实际运行测试方法，则可以在命令行中使用 **/listproperties** 开关。 让我们看一下输出。

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

请注意，在每次调用测试资源 depent 测试方法的过程中，将添加到测试方法名称的隐式索引。 ResourceSelection 属性后跟将可用于测试方法的所有资源的列表，这些资源将按可用的顺序提供。 例如，如果第三次调用 HDAudioHDAudioPCITest (HDAudioHDAudioPCITest \# 2) ，则 HDAudio--1 将是资源：： Item ( ... ) 中索引0处可用的资源。

您可以使用 TAEF 中提供的命令行选择查询语言，更具体地了解您感兴趣的测试调用。 例如，若要选择测试资源 "PCI-X" 可用的测试方法的所有调用，可以使用选择条件：

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

同样，若要按名称选择特定的测试方法 (注意测试方法名称是完全限定的，以及末尾) 中追加的调用索引，可以按如下所示使用选择查询：

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

请注意上面的示例的第三行中的隐式 inproc 添加的警告。 上述选择查询与选择查询具有相同的效果：**/select： " @Name = ' \* OneHDAudio \* ' And @Resource:Index = 1"**。 还可以使用其名称或类型 (或 Id （如上所示）选择资源) 。 例如， **/select： " @Name = ' \* PCIHDAudioTest \* ' and @Resource:Name = ' PCI3 '"** 将选择测试方法 PCIHDAudioTest \# 4 和 PCIHDAudioTest \# 5。

在命令提示符下尝试这些查询和其他选择查询仍可作为读者的练习。

 

 





