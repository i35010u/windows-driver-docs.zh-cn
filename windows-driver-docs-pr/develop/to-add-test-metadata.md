---
ms.assetid: 8BADC31C-6446-41FA-82F3-F46D66954481
title: 如何添加测试元数据
description: 使用 Windows 驱动程序工具包 (WDK) 以及测试创作和执行框架 (TAEF) 来创建适用于 Windows 8 的测试内容。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b419ea4377228394c78b29925dc500be8d63878e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518076"
---
# <a name="how-to-add-test-metadata"></a>如何添加测试元数据

对于 Windows 8，Windows 驱动程序工具包 (WDK) 使用[测试创作和执行框架 (TAEF)](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439725) 来创建测试内容。 TAEF 测试是以包含多个方法的动态链接库 (DLL) 形式实现的对象，其中的每个方法均映射到特定的测试方案。 TAEF 对象将相关方法合并为一个测试组。 对于每个测试，均有一组描述该测试的元数据。 为了提高测试可移植性和封装，TAEF 将测试元数据存储在测试对象本身中。 在使用驱动程序测试模板创建自己的驱动程序测试时，你需要添加该元数据，以便驱动程序测试可用，并可以使用 Visual Studio 部署。

### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件

-   使用其中一个驱动程序测试模板编写的驱动程序测试的源代码。 有关信息，请参阅[如何使用驱动程序测试模板编写驱动程序测试](how-to-write-a-driver-test-.md)。

### <a name="span-idtoaddtestmetadataattributesspanspan-idtoaddtestmetadataattributesspanspan-idtoaddtestmetadataattributesspanto-add-test-metadata-attributes"></a><span id="To_add_test_metadata_attributes"></span><span id="to_add_test_metadata_attributes"></span><span id="TO_ADD_TEST_METADATA_ATTRIBUTES"></span>添加测试元数据属性

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
        TEST_METHOD_PROPERTY(L&quot;Kits.Drivers&quot;, L&quot;TRUE&quot;)
        TEST_METHOD_PROPERTY(L&quot;Kits.Parameter&quot;, L&quot;DQ&quot;)
        TEST_METHOD_PROPERTY(L&quot;Kits.Parameter.DQ.Description&quot;, L&quot;A WDTF SDEL query that is used to identify the target device(s) - https://go.microsoft.com/fwlink/p/?linkid=232678&quot;)
        TEST_METHOD_PROPERTY(L&quot;Kits.Parameter.DQ.Default&quot;, L&quot;INF::OriginalInfFileName=&#39;%InfFileName%&#39;&quot;)  
        TEST_METHOD_PROPERTY(L&quot;RebootPossible&quot;, L&quot;true&quot;)
        // TODO: Required properties to be customized to match your test requirements
        TEST_METHOD_PROPERTY(L&quot;Description&quot;, L&quot;Plug and Play Surprise Remove Generated Template&quot;)
        TEST_METHOD_PROPERTY(L&quot;Kits.DisplayName&quot;, L&quot;My Plug and Play Surprise Remove Test&quot;) 
        TEST_METHOD_PROPERTY(L&quot;Kits.Category&quot;, L&quot;My Test Category&quot;)
        // Optional properties for driver tests
        TEST_METHOD_PROPERTY(L&quot;Kits.Drivers.ResultFile&quot;, L&quot;TestTextLog.log&quot;)
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
        [TestProperty(&quot;Kits.Drivers&quot;, &quot;TRUE&quot;)]
        [TestProperty(&quot;Kits.Parameter&quot;, &quot;DQ&quot;)]
        [TestProperty(&quot;Kits.Parameter.DQ.Description&quot;, &quot;A WDTF SDEL query that is used to identify the target device(s) - https://go.microsoft.com/fwlink/p/?linkid=232678&quot;)]
        [TestProperty(&quot;Kits.Parameter.DQ.Default&quot;, &quot;INF::OriginalInfFileName=&#39;%InfFileName%&#39;&quot;)]
        // TODO: Required properties to be customized to match your test requirements.
        [TestProperty(&quot;Description&quot;, &quot;Plug and Play Surprise Remove Generated Template&quot;)]
        [TestProperty(&quot;Kits.DisplayName&quot;, &quot;My Plug and Play Surprise Remove Test&quot;)]
        [TestProperty(&quot;Kits.Category&quot;, &quot;My Test Category&quot;)]
        [TestProperty(&quot;RebootPossible&quot;, &quot;true&quot;)]
        // Optional properties (see Windows Driver Kit documentation for additional optional properties):
        [TestProperty(&quot;Kits.Drivers.ResultFile&quot;, &quot;TestTextLog.log&quot;)]</code></pre></td>
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
        &lt;method name=&quot;PlugAndPlaySurpriseRemoveTest&quot;&gt;
        &lt;!-- Required properties for ERT--&gt;
        &lt;TestMethodProperty name=&quot;Kits.Drivers&quot; value=&quot;TRUE&quot;/&gt;
        &lt;TestMethodProperty name=&quot;Kits.Parameter&quot; value=&quot;DQ&quot;/&gt;
        &lt;TestMethodProperty name=&quot;Kits.Parameter.DQ.Description&quot; value=&quot;A WDTF SDEL query that is used to identify the target device(s) - https://go.microsoft.com/fwlink/p/?linkid=232678&quot;/&gt;
        &lt;TestMethodProperty name=&quot;Kits.Parameter.DQ.Default&quot; value=&quot;INF::OriginalInfFileName=&#39;%InfFileName%&#39;&quot;/&gt;
        &lt;TestMethodProperty name=&quot;RebootPossible&quot; value=&quot;true&quot; /&gt;
        &lt;!-- TODO: Properties to be customized to match your test requirements --&gt;
        &lt;TestMethodProperty name=&quot;Description&quot; value=&quot;Plug and Play Surprise Remove Generated Template&quot;/&gt;
        &lt;TestMethodProperty name=&quot;Kits.DisplayName&quot; value=&quot;My Plug and Play Surprise Remove Test&quot;/&gt;
        &lt;TestMethodProperty name=&quot;Kits.Category&quot; value=&quot;My Test Category&quot;/&gt;
        &lt;!-- Optional properties for ERT--&gt;
        &lt;TestMethodProperty name=&quot;Kits.Drivers.ResultFile&quot; value=&quot;TestTextLog.log&quot;/&gt;
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
      &lt; TestProperty name=&quot;Description&quot; value= &quot;This test cycles the system through various sleep states and performs IO on devices before and after each sleep state cycle&quot;/&gt;
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
      
     TEST_METHOD_PROPERTY(L&quot;Description&quot;, L&quot;Plug and Play Surprise Remove Generated Template&quot;)</code></pre></td>
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
      
     &lt; TestProperty name=&quot;Kits.DisplayName&quot; value=&quot;Sleep with IO Before and After&quot;/&gt;</code></pre></td>
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

      TEST_METHOD_PROPERTY(L&quot;Kits.DisplayName&quot;, L&quot;My Plug and Play Surprise Remove Test&quot;) </code></pre></td>
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

    &lt;ModuleProperty name=&quot;Kits.Parameter&quot; value=&quot;TM&quot;/&gt;</code></pre></td>
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

    TEST_METHOD_PROPERTY(L&quot;Kits.Parameter&quot;, L&quot;DQ&quot;)</code></pre></td>
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
      
    &lt; TestProperty name=&quot;Kits.Parameter.TM.Description&quot; value=&quot;Test mode parameter: Logo or Simple&quot;/&gt; </code></pre></td>
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

    TEST_METHOD_PROPERTY(L&quot;Kits.Parameter.DQ.Description&quot;, L&quot;A WDTF SDEL query that is used to identify the target device(s)&quot;)</code></pre></td>
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

    &lt; TestProperty name=&quot;Kits.Parameter.TM.Default&quot; value=&quot;Logo&quot;/&gt;</code></pre></td>
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

     TEST_METHOD_PROPERTY(L&quot;Kits.Parameter.DQ.Default&quot;, L&quot;INF::OriginalInfFileName=&#39;%InfFileName%&#39;&quot;)  </code></pre></td>
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
      
    &lt; TestProperty name=&quot;Kits.Drivers&quot; value=&quot;&quot;/&gt;</code></pre></td>
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

     TEST_METHOD_PROPERTY(L&quot;Kits.Drivers&quot;, L&quot;TRUE&quot;)</code></pre></td>
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
      
    &lt; TestProperty name=&quot;Kits.Category&quot; value=&quot;Logo\Device Fundamentals&quot;/&gt;</code></pre></td>
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

    TEST_METHOD_PROPERTY(L&quot;Kits.Category&quot;, L&quot;My Test Category&quot;)</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Deploymentitem"></span><span id="deploymentitem"></span><span id="DEPLOYMENTITEM"></span>**Deploymentitem**  
    将文件和/或文件夹标识为测试依赖项。 这些可能包含运行测试所需的任何资源。 有关使用此元数据的详细信息，请参阅 [DeploymentItem 元数据](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439604)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [如何使用“驱动程序测试”模板编写驱动程序测试](how-to-write-a-driver-test-.md)
 

 






