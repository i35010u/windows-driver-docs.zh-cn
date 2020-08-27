---
title: 使用脚本语言创作测试
description: 使用脚本语言创作测试
ms.assetid: 4F5328E4-4817-4391-BF56-EC9E7F469AA7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8a3ccc486752f839ea8c9108daaa3a687ac57cb
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902392"
---
# <a name="authoring-tests-in-scripting-languages"></a>使用脚本语言创作测试

除了 c + + 和 c # 外，TAEF 还支持编写脚本语言的测试。

使用支持 Microsoft COM 脚本接口的任何脚本语言创建脚本组件。 支持这些接口的脚本语言包括 JScript、Microsoft Visual Basic Scripting Edition (VBScript) 、PERLScript、PScript、Ruby 和 Python。

## <a name="current-limitations-of-the-script-test-authoring"></a>脚本测试创作的当前限制

Windows 只支持 JScript 和 VBScript。

## <a name="script-test-file-format"></a>脚本测试文件格式

对于脚本语言测试，TAEF 使用略微修改 [Windows 脚本组件](https://docs.microsoft.com/previous-versions/07zhfkh8(v=vs.85)) 文件格式。 下面的示例演示一个包含 VBScript 和 JScript 测试类的测试文件。

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

此示例是一个 XML 文件，并以普通 XML 标头开头：

```cpp
<?xml version="1.0" ?>
```

通过设置属性 " **错误** " 和 " **调试**"，为文件配置调试设置：

```cpp
<?component error="true" debug="true"?>
```

- 将 " **错误** " 设置为 " *true* " 将显示脚本组件中的语法或运行时错误的详细错误消息。
- 将 " **调试** " 设置为 " *true* " 以启用调试。 如果未启用调试，则无法启动脚本的脚本调试程序 (例如，使用 JScript 代码) 中的 **debug** 关键字。

** &lt; Package &gt; **元素在**wsc**文件中包含 test 类定义。 在此元素后，可以通过添加 **ModuleProperty** 元素插入模块级元数据：

```cpp
<ModuleProperty name = "Owner" value = "Someone"/>
```

**ModuleProperty**元素必须包括**name**和**value**属性。

**Component**元素启动脚本测试类的声明。 此元素应始终具有设置为类名的 **id** 属性。

在 **Component** 元素之后，可以通过使用 **TestClassProperty** 元素插入类级元数据。 与 **ModuleProperty** 元素一样，它必须具有 **name** 和 **value** 属性。

此时，您还可以创建对象并定义对对象的引用。 有关详细信息，请参阅 [其他组件部分](https://docs.microsoft.com/previous-versions/ye6w00x4(v=vs.85)) 。 XML 示例中的第15、18、49和52行说明了如何引用和初始化**WEX。记录对象。**

** &lt; 公共 &gt; **元素包含测试脚本模块的测试方法声明。 通过在** &lt; &gt; 方法**元素的**name**特性中指定测试方法名称来声明测试方法。 你还可以在** &lt; 方法 &gt; **元素中添加 "测试方法" 属性。 与其他级别的属性一样，它不是必需的。 但是，如果添加它，则必须包含 **名称** 和 **值** 属性。

** &lt; Script &gt; **元素标识测试脚本语言，并包含测试方法的实现。

** &lt; ！ \[\[CDATA \] 节 \] 包含测试的实际实现-用脚本语言编写的代码。 &gt; ** 在本部分中，你将实现在** &lt; public &gt; &lt; /public &gt; **节中声明的测试方法。
