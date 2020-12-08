---
title: 使用脚本语言创作数据驱动的测试
description: 使用脚本语言创作数据驱动的测试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4de9e894211de425115b2fdd0855de326a1b45a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840477"
---
# <a name="span-idtaefdata-driven_testing_in_scripting_languagesspandata-driven-testing-in-scripting-languages"></a><span id="taef.data-driven_testing_in_scripting_languages"></span>使用脚本语言创作数据驱动的测试


为了理解此部分，您应该熟悉如何 [在脚本语言中创作测试](authoring-tests-in-scripting-languages.md)。 本部分不讨论 [各种 TAEF 数据驱动的测试方法](data-driven-testing.md)的详细信息。 若要快速了解，请查看不同 TAEF 数据驱动的测试构造：

-   [基于表的数据驱动测试](table-data-source.md)
-   [基于 WMI 的数据驱动测试](wmi-data-source.md)
-   [基于 PICT 的数据驱动测试](pict-data-source.md)
-   [轻型数据驱动的测试](light-weight-data-driven-testing.md)

甚至可以通过使用上述任一数据源的一个或多个数据源来选择组合数据源。 有关详细信息，请参阅 [指定多个数据源](multiple-datasources.md) 。

## <a name="span-idspecifying_the_data_source_in_scripting_languagespanspan-idspecifying_the_data_source_in_scripting_languagespanspan-idspecifying_the_data_source_in_scripting_languagespanspecifying-the-data-source-in-scripting-language"></a><span id="Specifying_the_data_source_in_scripting_language"></span><span id="specifying_the_data_source_in_scripting_language"></span><span id="SPECIFYING_THE_DATA_SOURCE_IN_SCRIPTING_LANGUAGE"></span>用脚本语言指定数据源


通过 TAEF 中的数据驱动的测试，可以在类或测试级别指定 **数据源** 。 在数据驱动类中，数据可用于类和测试方法的安装、清理以及类中的所有测试方法。 **DataSource** 参数是用于指示从何处检索数据的信息。 对于基于表的数据驱动的测试，此值包括 XML 文件的相对路径和数据所在的 XML 文件中的 TableId。 有关更多详细信息，请参阅上面列出的链接。

下面的示例演示如何指定 **DataSource** 属性。

```cpp
1   <?xml version="1.0" ?>
2   <?component error="true" debug="true"?>
3   <package>
4       <component id="VBSampleTests">
5           <object id="Log" progid="WEX.Logger.Log" />
6           <object id="TestData" progid="Te.Common.TestData" />
7
8           <public>
9               <method name="TestOne">
10                  <TestMethodProperty name="DataSource" value="WMI:SELECT Label, Caption FROM Win32_Volume"/>
11              </method>
12
13              <method name="TestTwo">
14                  <TestMethodProperty name="DataSource" value="Table:ScriptExampleTable.xml#MyTable;WMI:SELECT Label, Caption FROM Win32_Volume"/>
15              </method>
16          </public>
17
18          <script language="VBScript">
19              <![CDATA[
20                  Function TestOne()
21                      dim caption
22                      caption = "NoCaption"
23                      Log.Comment("Caption is " + caption)
24
25                      If TestData.Contains("Caption") Then
26                      caption = TestData.GetValue("Caption")
27                      End If
28                      Log.Comment("Caption is " + caption)
29                  End Function
30
31                  Function TestTwo()
32                      Log.Comment("Calling TestTwo")
33                      dim caption
34                      caption = "NoCaption"
35                      Log.Comment("Caption is " + caption)
36
37                      If TestData.Contains("Caption") Then
38                      caption = TestData.GetValue("Caption")
39                      End If
40                      Log.Comment("Caption is " + caption)
41
42                      dim size
43                      If TestData.Contains("Size") Then
44                      size = TestData.GetValue("Size")
45                      End If
46                      Log.Comment("Size is " + CStr(size))
47
48                      dim transparency
49                      If TestData.Contains("Transparency") Then
50                      transparency = TestData.GetValue("Transparency")
51                      End If
52                      Log.Comment("Transparency is " + CStr(transparency))
53                  End Function
54              ]] >
55          </script>
56      </component>
57
58      <component id="JScriptSampleTests">
59          <object id="Log" progid="WEX.Logger.Log" />
60          <object id="TestData" progid="Te.Common.TestData" />
61
62          <TestClassProperty name="DataSource" value="Table:ScriptExampleTable.xml#MyTable"/>
63
64          <public>
65              <method name="ClassSetup" type="TestClassSetup"/>
66              <method name="ClassCleanup" type="TestClassCleanup"/>
67              <method name="MethodSetup"  type="TestMethodSetup"/>
68              <method name="MethodCleanup" type="TestMethodCleanup"/>
69
70              <method name="TestOne"/>
71              <method name="TestTwo">
72                  <TestMethodProperty name="DataSource" value="WMI:SELECT Label, Caption FROM Win32_Volume"/>
73              </method>
74          </public>
75
76          <script language="JScript">
77              <![CDATA[
78                  function ClassSetup()
79                  {
80                      Log.Comment("Calling class setup");
81                      var size;
82                      if(TestData.Contains("Size"))
83                      {
84                          size = TestData.GetValue("Size");
85                      }
86                      Log.Comment("Size is " + size);
87  
88                      var transparency;
89                      if(TestData.Contains("Transparency"))
90                      {
91                          transparency = TestData.GetValue("Transparency");
92                      }
93                      Log.Comment("Transparency is " + transparency);
94                  }
95
96                  function ClassCleanup()
97                  {
98                      Log.Comment("Calling class cleanup");
99                      return true;
100                 }
101
102                 function MethodSetup()
103                 {
104                     Log.Comment("Calling method setup");
105                     var size;
106                     if(TestData.Contains("Size"))
107                     {
108                         size = TestData.GetValue("Size");
109                     }
110                     Log.Comment("Size is " + size);
111
112                     var transparency;
113                     if(TestData.Contains("Transparency"))
114                     {
115                         transparency = TestData.GetValue("Transparency");
116                     }
117                     Log.Comment("Transparency is " + transparency);
118                     return true;
119                 }
120
121                 function MethodCleanup()
122                 {
123                     Log.Comment("Calling method cleanup");
124                     return true;
125                 }
126
127                 function TestOne()
128                 {
129                     Log.Comment("Calling TestOne");
130                     var size;
131                     if(TestData.Contains("Size"))
132                     {
133                         size = TestData.GetValue("Size");
134                     }
135                     Log.Comment("Size is " + size);
136
137                     var transparency;
138                     if(TestData.Contains("Transparency"))
139                     {
140                         transparency = TestData.GetValue("Transparency");
141                     }
142                     Log.Comment("Transparency is " + transparency);
143                 }
144
145                 function TestTwo()
146                 {
147                     Log.Comment("Calling TestTwo");
148                     var caption = "NoCaption";
149                     Log.Comment("Initial caption: " + caption);
150
151                     if(TestData.Contains("Caption"))
152                     {
153                         caption = TestData.GetValue("Caption");
154                     }
155                     Log.Comment("Caption is " + caption);
156
157                     var size;
158                     if(TestData.Contains("Size"))
159                     {
160                         size = TestData.GetValue("Size");
161                     }
162                     Log.Comment("Size is " + size);
163
164                     var transparency;
165                     if(TestData.Contains("Transparency"))
166                     {
167                         transparency = TestData.GetValue("Transparency");
168                     }
169                     Log.Comment("Transparency is " + transparency);
170                 }
171             ]] >
172         </script>
173     </component>
174 </package>
```

在上面的示例中，第6行和第60行声明并实例化一个 **TestData** 对象，该对象允许对数据驱动测试的数据进行访问。

**&lt; TestMethodProperty &gt;** 和 **&lt; TestClassProperty &gt;** 标记是为测试或类定义 **数据源** 的行。 在 VBSampleTests 中， **TestOne** 具有作为其 **数据源** 的 [WMI 查询](wmi-data-source.md)。 参数 **标签** 和 **标题** 可用于 **TestOne 的** 设置、清除和测试方法。 在同一个类中， **TestTwo** 定义了 [多个数据源](multiple-datasources.md) 。 第一种是 [基于表的数据源](table-data-source.md)，第二种是基于 WMI 的 **数据源** ，它是 **TestOne**。

TAEF 为每个 **数据源** 属性生成参数集的组合扩展。 一个参数集可用于每个测试方法调用。 如果 WMI 查询返回四组结果 (Win32 \_ 卷) 并且基于表的 **数据源** 中有三行， **TestOne** 将对 WMI 查询返回的每个 Win32 卷执行四次 \_ 。 另一方面， **TestTwo** 针对 Win32 \_ 卷数据和表指定的行的每个组合执行 12 (4 X 3) 次。 相关的安装和清理方法还提供了数据。

在 JScriptSampleTests 中，可以看到数据驱动类的示例。 由于该示例在类级别指定 **DataSource** ，因此数据可用于所有测试方法，还可用于测试和类级别的设置和清理方法。 由于 **TestTwo** 是数据驱动类中的数据驱动的测试，因此，来自类级别的数据 **源** 中的数据以及来自测试级别的数据都可用于 **TestTwo**。

## <a name="span-iddata_types_available_for_script_testsspanspan-iddata_types_available_for_script_testsspanspan-iddata_types_available_for_script_testsspandata-types-available-for-script-tests"></a><span id="Data_types_available_for_script_tests"></span><span id="data_types_available_for_script_tests"></span><span id="DATA_TYPES_AVAILABLE_FOR_SCRIPT_TESTS"></span>可用于脚本测试的数据类型


以下参数类型适用于脚本语言。 这些是可以在基于表的数据驱动测试中指定的类型。 默认参数类型为 *String* 或 *BSTR* (表示 *VT \_ BSTR*) 。

[基于表的数据源中的节参数类型](parameter-types-in-table-data-sources.md)演示了如何在使用脚本语言创作测试) 的情况下，在本机和托管代码中查看可用参数类型 (。

## <a name="span-idexecuting_data-driven_scriptsspanspan-idexecuting_data-driven_scriptsspanspan-idexecuting_data-driven_scriptsspanexecuting-data-driven-scripts"></a><span id="Executing_data-driven_scripts"></span><span id="executing_data-driven_scripts"></span><span id="EXECUTING_DATA-DRIVEN_SCRIPTS"></span>执行数据驱动的脚本


**/Listproperties** 选项不仅列出了元数据，还列出了可用于测试的每个调用的数据。 在整个 dll 上运行 **/listproperties** 选项 (将被留给读者执行。 ) 以下示例使用 [选择查询](selection.md)语言从 VBSampleTests 中选择调用 **TestOne** ：

``` syntax
f:\spartadev.binaries.x86chk\WexTest\CuE\TestExecution>te Examples\DataDrivenTest.wsc /listproperties /name:VBSampleTests::TestOne*

Test Authoring and Execution Framework v.R10 Build 6.1.6939.0 For x86

        f:\spartadev.binaries.x86chk\WexTest\CuE\TestExecution\Examples\DataDrivenTest.wsc
            VBSampleTests
                VBSampleTests::TestOne#0
                        Property[DataSource] = WMI:SELECT Label, Caption FROM Win32_Volume

                        Data[Caption] = C:\
                        Data[Label] =

                VBSampleTests::TestOne#1
                        Property[DataSource] = WMI:SELECT Label, Caption FROM Win32_Volume

                        Data[Caption] = D:\
                        Data[Label] = New Volume

                VBSampleTests::TestOne#2
                        Property[DataSource] = WMI:SELECT Label, Caption FROM Win32_Volume

                        Data[Caption] = F:\
                        Data[Label] = New Volume

                VBSampleTests::TestOne#3
                        Property[DataSource] = WMI:SELECT Label, Caption FROM Win32_Volume

                        Data[Caption] = E:\
                        Data[Label] = New Volume

                VBSampleTests::TestOne#4
                        Property[DataSource] = WMI:SELECT Label, Caption FROM Win32_Volume

                        Data[Caption] = G:\
                        Data[Label] = New Volume

                VBSampleTests::TestOne#5
                        Property[DataSource] = WMI:SELECT Label, Caption FROM Win32_Volume

                        Data[Caption] = H:\
                        Data[Label] = New Volume

                VBSampleTests::TestOne#6
                        Property[DataSource] = WMI:SELECT Label, Caption FROM Win32_Volume

                        Data[Caption] = K:\
                        Data[Label] =
```

**/Listproperties** 选项显示 TAEF 为每个 Win32 卷调用了测试方法 **VBSampleTests：： TestOne** 7 次 \_ 。 对于每个调用，TAEF 向测试方法追加一个隐式 *索引* 以区分每个调用。 还可以查看每次调用测试方法时可用的数据和元数据。

使用 **/listproperties** 选项中的信息，可以应用基于数据值或索引值的选择查询，以更好地控制要执行的测试调用。 下面的示例演示如何仅运行标题为 **E： \\** 的调用：

``` syntax
te Examples\DataDrivenTest.wsc /select:"@Name='VBSampleTests::TestOne*' and @Data:Caption='E:\'"
```

以下命令使用索引来选择同一测试：

``` syntax
te Examples\DataDrivenTest.wsc /select:"@Name='VBSampleTests::TestOne*' and @Data:Index=3"
```

如果在脚本测试中使用基于 PICT 和轻型数据驱动的测试，则会将其作为练习留给读者。

 

 





