---
title: 数据驱动的测试中的脚本语言
description: 数据驱动的测试中的脚本语言
ms.assetid: CF60C594-8877-4f09-AF82-9F4CA27123C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 782808f9c7d86008e84b524312ddbfcd1024658a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554224"
---
# <a name="span-idtaefdata-driventestinginscriptinglanguagesspandata-driven-testing-in-scripting-languages"></a><span id="taef.data-driven_testing_in_scripting_languages"></span>数据驱动的测试中的脚本语言


若要了解本部分中，您应熟悉如何[创作的脚本语言中的测试](authoring-tests-in-scripting-languages.md)。 本部分不会讨论的详细信息[各种 TAEF 数据驱动测试方法](data-driven-testing.md)。 有关快速概述，查看不同 TAEF 数据驱动测试的构造：

-   [基于表的数据驱动的测试](table-data-source.md)
-   [基于 WMI 数据驱动的测试](wmi-data-source.md)
-   [PICT 基于数据驱动的测试](pict-data-source.md)
-   [轻量数据驱动的测试](light-weight-data-driven-testing.md)

您甚至可以选择具有通过上述任一的一个或多个数据源的数据源的组合。 请参阅[指定多个数据源](multiple-datasources.md)有关详细信息。

## <a name="span-idspecifyingthedatasourceinscriptinglanguagespanspan-idspecifyingthedatasourceinscriptinglanguagespanspan-idspecifyingthedatasourceinscriptinglanguagespanspecifying-the-data-source-in-scripting-language"></a><span id="Specifying_the_data_source_in_scripting_language"></span><span id="specifying_the_data_source_in_scripting_language"></span><span id="SPECIFYING_THE_DATA_SOURCE_IN_SCRIPTING_LANGUAGE"></span>指定脚本语言中的数据源


数据驱动测试 TAEF 中可以指定**数据源**类或测试级别。 在数据驱动的类中，数据是可用于类和测试类中方法安装程序、 清理和所有测试方法。 **数据源**参数是告知将从中检索的数据的信息。 在基于表的数据驱动测试的情况下此值在数据所在的位置的 XML 文件中包括 XML 文件和 TableId 的相对路径。 请参阅上述的更多详细信息的链接。

下面的示例演示如何指定**数据源**属性。

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

在上面的示例中，第 6 和 60 行声明和实例化**TestData**对象，它允许对数据的数据驱动测试的访问。

**&lt;TestMethodProperty&gt;** 并**&lt;TestClassProperty&gt;** 标记是定义的行**DataSource**对于测试或类。 在 VBSampleTests **TestOne**已[WMI 查询](wmi-data-source.md)作为其**数据源**。 参数**标签**并**标题**可供**TestOne 的**安装程序、 清理和测试方法。 在同一类中， **TestTwo**已[多个数据源](multiple-datasources.md)定义。 第一个是[基于表的数据源](table-data-source.md)，第二个是基于同一个 WMI**数据源**作为**TestOne**。

TAEF 生成的每个参数集的组合扩展**数据源**属性。 一个参数集是可用于每个测试方法调用。 如果 WMI 查询返回四个组的结果 (Win32\_卷) 和基于表中有三个行**数据源**， **TestOne**将执行四次-一次与每个 Win32\_WMI 查询返回的卷。 但是， **TestTwo**执行 12 (4 X 3) 的每个组合 Win32 时间\_卷数据和表指定的行。 也有关联的设置和清理方法可用的数据。

在 JScriptSampleTests，可以看到数据驱动的类的一个示例。 因为该示例指定**数据源**在类级别中，数据可供所有测试方法中的测试和类级别设置和清理方法。 因为**TestTwo**是在数据驱动类中，将数据从一个数据驱动测试**数据源**级别是在类级别，以及从测试，可用于**TestTwo**.

## <a name="span-iddatatypesavailableforscripttestsspanspan-iddatatypesavailableforscripttestsspanspan-iddatatypesavailableforscripttestsspandata-types-available-for-script-tests"></a><span id="Data_types_available_for_script_tests"></span><span id="data_types_available_for_script_tests"></span><span id="DATA_TYPES_AVAILABLE_FOR_SCRIPT_TESTS"></span>可供脚本测试使用的数据类型


以下参数类型都可用于脚本编写语言。 这些是可以在数据驱动的测试基于的表中指定的类型。 默认参数类型是*字符串*或*BSTR* (表示*VT\_BSTR*)。

部分[表中的参数类型基于数据源](parameter-types-in-table-data-sources.md)演示了如何创作脚本语言中的测试时查看可用的参数类型 （在本机和托管代码）。

## <a name="span-idexecutingdata-drivenscriptsspanspan-idexecutingdata-drivenscriptsspanspan-idexecutingdata-drivenscriptsspanexecuting-data-driven-scripts"></a><span id="Executing_data-driven_scripts"></span><span id="executing_data-driven_scripts"></span><span id="EXECUTING_DATA-DRIVEN_SCRIPTS"></span>执行数据驱动的脚本


**/Listproperties**选项列出不仅元数据，但也可用于测试的每个调用的数据。 (运行 **/listproperties**整个 dll 上的选项留给大家练练手读取器。)下面的示例选择的调用**TestOne** VBSampleTests 使用[选择查询](selection.md)语言：

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

**/Listproperties** TAEF 调用测试方法显示选项**VBSampleTests::TestOne** 7 次-一次每个 Win32\_卷。 对于每个调用 TAEF 追加一个隐式*索引*到测试方法以区分每个调用。 此外可以查看数据和元数据可用于测试方法的每个调用。

使用中的信息 **/listproperties**选项，可用于基于数据值的选择查询或要获得更细致的索引值控制这些测试执行的调用。 下面的示例演示如何运行仅调用标题所在**e:\\**:

``` syntax
te Examples\DataDrivenTest.wsc /select:"@Name='VBSampleTests::TestOne*' and @Data:Caption='E:\'"
```

以下命令使用索引来选择相同的测试：

``` syntax
te Examples\DataDrivenTest.wsc /select:"@Name='VBSampleTests::TestOne*' and @Data:Index=3"
```

读取器练习使用的 PICT 基于和浅色保留权重脚本测试中的数据驱动测试。

 

 





