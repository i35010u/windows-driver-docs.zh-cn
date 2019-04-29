---
title: 使用脚本语言创作测试
description: 使用脚本语言创作测试
ms.assetid: 4F5328E4-4817-4391-BF56-EC9E7F469AA7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 989f1f25825050e7115933e57bd2bd82f5ab90ac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385156"
---
# <a name="authoring-tests-in-scripting-languages"></a>使用脚本语言创作测试


除了C++和C#、 TAEF 支持创作脚本语言中的测试。

创建脚本组件使用支持脚本编写 Microsoft COM 接口的任何脚本语言。 脚本语言支持这些接口包括 JScript、 Microsoft Visual Basic Scripting Edition (VBScript)、 PERLScript、 PScript、 Ruby 和 Python。

## <a name="span-idcurrentlimitationsofthescripttestauthoringspanspan-idcurrentlimitationsofthescripttestauthoringspanspan-idcurrentlimitationsofthescripttestauthoringspancurrent-limitations-of-the-script-test-authoring"></a><span id="Current_Limitations_of_the_Script_Test_Authoring"></span><span id="current_limitations_of_the_script_test_authoring"></span><span id="CURRENT_LIMITATIONS_OF_THE_SCRIPT_TEST_AUTHORING"></span>该脚本的当前限制测试创作


默认情况下，Windows JScript 和 VBScript 仅支持。

## <a name="span-idscripttestfileformatspanspan-idscripttestfileformatspanspan-idscripttestfileformatspanscript-test-file-format"></a><span id="Script_Test_File_Format"></span><span id="script_test_file_format"></span><span id="SCRIPT_TEST_FILE_FORMAT"></span>脚本的测试文件格式


对于脚本语言的测试，TAEF 使用略有修改[Windows 脚本组件](https://msdn.microsoft.com/library/07zhfkh8.aspx)文件格式。 下面的示例显示了包含 VBScript 和 JScript 测试类的测试文件。

```cpp
1   <?xml version="1.0" ?>
2
3   <!-- Debugging helpers -->
4   <!-- error    Set this to true to display detailed error messages for syntax or run-time errors in the script component.-->
5   <!-- debug    Set this to true to enable debugging. If this debugging is not enabled, you cannot launch the script debugger for a script -->
6   <?component error="true" debug="true"?>
7
8   <package>
9       <!-- Test module metadata -->
10      <ModuleProperty name="Owner" value="Someone"/>
11
12      <!-- Define a test class -->
13      <component id="VBSampleTests">
14          <!-- define and instantiate a logger -->
15          <object id="Log" progid="WEX.Logger.Log" />
16  
17          <!-- include a reference to the logger so you could use the constants defined in logger library -->
18          <reference guid="e65ef678-a232-42a7-8a36-63108d719f31" version="1.0"/>
19
20          <!-- Test class metadata -->
21          <TestClassProperty name="DocumentationUrl" value="http://shelltestkb/"/>
22
23          <public>
24              <!-- Define a test method with metadata -->
25              <method name="TestOne">
26                  <!-- Test method metadata -->
27                  <TestMethodProperty name="Priority" value="1"/>
28              </method>
29  
30              <!-- Define a test method without metadata -->
31              <method name="TestTwo"/>
32         </public>
33
34          <script language="VBScript">
35              <![CDATA[
36                  Function TestOne()
37                      Log.Comment("Calling TestOne")
38                  End Function
39
40                  Function TestTwo()
41                      Log.Comment("Calling TestTwo")
42                  End Function
43              ]] >
44          </script>
45      </component>
46
47      <!-- Define another test class -->
48      <component id="JScriptSampleTests">
49          <object id="Log" progid="WEX.Logger.Log" />
50
51          <!-- need reference to use logger constants -->
52          <reference guid="e65ef678-a232-42a7-8a36-63108d719f31" version="1.0"/>
53
54          <public>
55              <!-- Test setup and cleanup methods are declared using corresponding type = '' attributes -->
56              <method name="ClassSetup" type="TestClassSetup"/>
57              <method name="ClassCleanup" type="TestClassCleanup"/>
58              <method name="MethodSetup"  type="TestMethodSetup"/>
59              <method name="MethodCleanup" type="TestMethodCleanup"/>
60
61              <method name="TestOne"/>
62              <method name="TestTwo"/>
63          </public>
64
65          <!-- Setup and Cleanup methods return false on failure -->
66          <script language="JScript">
67              <![CDATA[
68                  function ClassSetup()
69                  {
70                      Log.Comment("Calling class setup");
71                      return true;
72                  }
73
74                  function ClassCleanup()
75                  {
76                      Log.Comment("Calling class cleanup");
77                      return true;
78                  }
79
80                  function MethodSetup()
81                  {
82                      Log.Comment("Calling method setup");
83                      return true;
84                  }
85
86                  function MethodCleanup()
87                  {
88                      Log.Comment("Calling method cleanup");
89                      return true;
90                  }
91
92                  function TestOne()
93                  {
94                      Log.Comment("Calling TestOne");
95  
96                      // For the purpose of demonstration, declare the test failed
97                      Log.Result(TestResult_Failed);
98                  }
99
100                 function TestTwo()
101                 {
102                     Log.Comment("Calling TestTwo");
103                 }
104             ]] >
105         </script>
106     </component>
107 </package>
```

此示例是一个 XML 文件，并启动与普通的 XML 标头：

```cpp
<?xml version="1.0" ?>
```

为你的文件中设置的特性配置调试设置**错误**并**调试**:

```cpp
<?component error="true" debug="true"?>
```

-   设置**错误**到*true*若要在脚本组件中显示的语法或运行时错误的详细的错误消息。
-   设置**调试**到*true*以启用调试。 如果未启用调试，不能启动脚本调试程序的脚本 (如使用**调试**JScript 代码中的关键字)。

**&lt;包&gt;** 元素包含中的测试类定义 **.wsc**文件。 此元素后，可以插入模块级元数据通过添加**ModuleProperty**元素：

```cpp
<ModuleProperty name = "Owner" value = "Someone"/>
```

**ModuleProperty**元素必须包括**名称**并**值**属性。

**组件**元素的开始脚本测试类的声明。 此元素应始终具有**id**设置为类名称的属性。

之后**组件**元素中，可以使用插入类级别的元数据**TestClassProperty**元素。 如同**ModuleProperty**元素，它必须具有**名称**并**值**属性。

此时，您还可以创建对象并定义对对象的引用。 请参阅[其他组件部分](https://msdn.microsoft.com/library/ye6w00x4.aspx)有关详细信息。 15、 18、 49、 和中的 XML 示例的第 52 行显示了如何引用和初始化**WEX。Logger.Log**对象。

**&lt;公共&gt;** 元素包含测试脚本模块的测试方法声明。 通过指定测试方法名称中的声明一个测试方法**名称**的属性**&lt;方法&gt;** 元素。 您还可以添加测试方法属性内的**&lt;方法&gt;** 元素。 与在其他级别的属性，并不总是这样。 但是，如果将其添加，则必须包括**名称**并**值**属性。

**&lt;脚本&gt;** 元素标识的测试脚本语言，并且包含了测试方法的实现。

**&lt;！\[CDATA\[ \] \] &gt;** 部分包含测试的实际实现中的脚本语言编写的代码。 在本部分中，您可以实现中声明的测试方法**&lt;公共&gt; &lt;/public&gt;** 部分。

 

 





