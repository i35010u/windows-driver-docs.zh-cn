---
ms.assetid: 8BADC31C-6446-41FA-82F3-F46D66954481
title: 如何添加测试元数据
description: 使用 Windows 驱动程序工具包 (WDK) 以及测试创作和执行框架 (TAEF) 来创建适用于 Windows 8 的测试内容。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d28281ed52474270cdd340d9bd9cf7e03db7e4a2
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "67364207"
---
# <a name="how-to-add-test-metadata"></a>如何添加测试元数据

对于 Windows 8，Windows 驱动程序工具包 (WDK) 使用[测试创作和执行框架 (TAEF)](https://docs.microsoft.com/windows-hardware/drivers/taef/index) 来创建测试内容。 TAEF 测试是以包含多个方法的动态链接库 (DLL) 形式实现的对象，其中的每个方法均映射到特定的测试方案。 TAEF 对象将相关方法合并为一个测试组。 对于每个测试，均有一组描述该测试的元数据。 为了提高测试可移植性和封装，TAEF 将测试元数据存储在测试对象本身中。 在使用驱动程序测试模板创建自己的驱动程序测试时，你需要添加该元数据，以便驱动程序测试可用，并可以使用 Visual Studio 部署。

### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件

-   使用其中一个驱动程序测试模板编写的驱动程序测试的源代码。 有关信息，请参阅[如何使用驱动程序测试模板编写驱动程序测试](how-to-write-a-driver-test-.md)。

### <a name="span-idto_add_test_metadata_attributesspanspan-idto_add_test_metadata_attributesspanspan-idto_add_test_metadata_attributesspanto-add-test-metadata-attributes"></a><span id="To_add_test_metadata_attributes"></span><span id="to_add_test_metadata_attributes"></span><span id="TO_ADD_TEST_METADATA_ATTRIBUTES"></span>添加测试元数据属性

1.  将所需的测试属性元数据添加到测试的源文件。
2.  例如，如果你使用“驱动程序测试”模板创建 SurpriseRemove 测试的版本，则添加以下元数据。 编辑测试说明、显示名称、类别和结果文件属性。

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>// Declare the test class method DoSurpriseRemove - the main test method within this class
        BEGIN_TEST_METHOD(DoSurpriseRemove)
        // Required properties for driver tests
        TEST_METHOD_PROPERTY(L"Kits.Drivers", L"TRUE")
        TEST_METHOD_PROPERTY(L"Kits.Parameter", L"DQ")
        TEST_METHOD_PROPERTY(L"Kits.Parameter.DQ.Description", L"A WDTF SDEL query that is used to identify the target device(s) - https://go.microsoft.com/fwlink/p/?linkid=232678")
        TEST_METHOD_PROPERTY(L"Kits.Parameter.DQ.Default", L"INF::OriginalInfFileName='%InfFileName%'")  
        TEST_METHOD_PROPERTY(L"RebootPossible", L"true")
        // TODO: Required properties to be customized to match your test requirements
        TEST_METHOD_PROPERTY(L"Description", L"Plug and Play Surprise Remove Generated Template")
        TEST_METHOD_PROPERTY(L"Kits.DisplayName", L"My Plug and Play Surprise Remove Test") 
        TEST_METHOD_PROPERTY(L"Kits.Category", L"My Test Category")
        // Optional properties for driver tests
        TEST_METHOD_PROPERTY(L"Kits.Drivers.ResultFile", L"TestTextLog.log")
        // TODO: (see Windows Driver Kit documentation for additional optional properties)
        END_TEST_METHOD()</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="CSharp"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C#</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>//
        // DoSurpriseRemove is a test method as identified by the [TestMethod] tag. 
        // More methods can be added by following this basic pattern.
        // The name of the function defines the name of the test.
        //
        [TestMethod]
        // Required properties (see Windows Driver Kit documentation for more information):
        [TestProperty("Kits.Drivers", "TRUE")]
        [TestProperty("Kits.Parameter", "DQ")]
        [TestProperty("Kits.Parameter.DQ.Description", "A WDTF SDEL query that is used to identify the target device(s) - https://go.microsoft.com/fwlink/p/?linkid=232678")]
        [TestProperty("Kits.Parameter.DQ.Default", "INF::OriginalInfFileName='%InfFileName%'")]
        // TODO: Required properties to be customized to match your test requirements.
        [TestProperty("Description", "Plug and Play Surprise Remove Generated Template")]
        [TestProperty("Kits.DisplayName", "My Plug and Play Surprise Remove Test")]
        [TestProperty("Kits.Category", "My Test Category")]
        [TestProperty("RebootPossible", "true")]
        // Optional properties (see Windows Driver Kit documentation for additional optional properties):
        [TestProperty("Kits.Drivers.ResultFile", "TestTextLog.log")]</code></pre></td>
    </tr>
    </tbody>
    </table>

    Windows 脚本组件 (.wsc)

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>&lt;!-- Define a test method with metadata: --&gt;
        &lt;method name="PlugAndPlaySurpriseRemoveTest"&gt;
        &lt;!-- Required properties for ERT--&gt;
        &lt;TestMethodProperty name="Kits.Drivers" value="TRUE"/&gt;
        &lt;TestMethodProperty name="Kits.Parameter" value="DQ"/&gt;
        &lt;TestMethodProperty name="Kits.Parameter.DQ.Description" value="A WDTF SDEL query that is used to identify the target device(s) - https://go.microsoft.com/fwlink/p/?linkid=232678"/&gt;
        &lt;TestMethodProperty name="Kits.Parameter.DQ.Default" value="INF::OriginalInfFileName='%InfFileName%'"/&gt;
        &lt;TestMethodProperty name="RebootPossible" value="true" /&gt;
        &lt;!-- TODO: Properties to be customized to match your test requirements --&gt;
        &lt;TestMethodProperty name="Description" value="Plug and Play Surprise Remove Generated Template"/&gt;
        &lt;TestMethodProperty name="Kits.DisplayName" value="My Plug and Play Surprise Remove Test"/&gt;
        &lt;TestMethodProperty name="Kits.Category" value="My Test Category"/&gt;
        &lt;!-- Optional properties for ERT--&gt;
        &lt;TestMethodProperty name="Kits.Drivers.ResultFile" value="TestTextLog.log"/&gt;
        &lt;!-- (see Windows Driver Kit documentation for additional optional properties) --&gt;
        &lt;/method&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

3.  下表介绍测试的属性特性。 在编辑或添加测试元数据时，请使用示例作为指南。

    <span id="Description"></span><span id="description"></span><span id="DESCRIPTION"></span>**Description**  
    对测试任务的简短说明。

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 
      &lt; TestProperty name="Description" value= "This test cycles the system through various sleep states and performs IO on devices before and after each sleep state cycle"/&gt;
    </code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[C++]
      
     TEST_METHOD_PROPERTY(L"Description", L"Plug and Play Surprise Remove Generated Template")</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="DisplayName"></span><span id="displayname"></span><span id="DISPLAYNAME"></span>**DisplayName**  
    在“驱动程序测试”中显示的测试名称。

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 
      
     &lt; TestProperty name="Kits.DisplayName" value="Sleep with IO Before and After"/&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code> [C++]

      TEST_METHOD_PROPERTY(L"Kits.DisplayName", L"My Plug and Play Surprise Remove Test") </code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Parameter"></span><span id="kits.parameter"></span><span id="KITS.PARAMETER"></span>**Kits.Parameter**  
    方法调用的标准参数。 一个测试可以有多个参数。

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 

    &lt;ModuleProperty name="Kits.Parameter" value="TM"/&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[C++]

    TEST_METHOD_PROPERTY(L"Kits.Parameter", L"DQ")</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Parameter._ParameterName_.Description"></span><span id="kits.parameter._parametername_.description"></span><span id="KITS.PARAMETER._PARAMETERNAME_.DESCRIPTION"></span>**Kits.Parameter.***&lt;ParameterName&gt;***.Description**  
    参数的说明。

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 
      
    &lt; TestProperty name="Kits.Parameter.TM.Description" value="Test mode parameter: Logo or Simple"/&gt; </code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code> 
    [C++]

    TEST_METHOD_PROPERTY(L"Kits.Parameter.DQ.Description", L"A WDTF SDEL query that is used to identify the target device(s)")</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Parameter._ParameterName_.Default"></span><span id="kits.parameter._parametername_.default"></span><span id="KITS.PARAMETER._PARAMETERNAME_.DEFAULT"></span>**Kits.Parameter.***&lt;ParameterName&gt;***.Default**  
    参数的默认值。

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 

    &lt; TestProperty name="Kits.Parameter.TM.Default" value="Logo"/&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[C++]

     TEST_METHOD_PROPERTY(L"Kits.Parameter.DQ.Default", L"INF::OriginalInfFileName='%InfFileName%'")  </code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Drivers"></span><span id="kits.drivers"></span><span id="KITS.DRIVERS"></span>**Kits.Drivers**  
    此特性将测试标记为包括在 WDK 中。

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 
      
    &lt; TestProperty name="Kits.Drivers" value=""/&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[C++]

     TEST_METHOD_PROPERTY(L"Kits.Drivers", L"TRUE")</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Category"></span><span id="kits.category"></span><span id="KITS.CATEGORY"></span>**Kits.Category**  
    描述测试的类别。

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code> [Script] 
      
    &lt; TestProperty name="Kits.Category" value="Logo\Device Fundamentals"/&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code> [C++]

    TEST_METHOD_PROPERTY(L"Kits.Category", L"My Test Category")</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Deploymentitem"></span><span id="deploymentitem"></span><span id="DEPLOYMENTITEM"></span>**Deploymentitem**  
    将文件和/或文件夹标识为测试依赖项。 这些可能包含运行测试所需的任何资源。 有关使用此元数据的详细信息，请参阅 [DeploymentItem 元数据](https://docs.microsoft.com/windows-hardware/drivers/taef/deploymentitem-metadata)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [如何使用“驱动程序测试”模板编写驱动程序测试](how-to-write-a-driver-test-.md)
 

 






