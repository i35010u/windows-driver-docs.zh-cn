---
title: 清单文件格式
description: 清单文件格式
ms.assetid: 1b0dc305-878c-4eb2-9e92-f7f7017ae4eb
keywords:
- 日志查看器，清单，文件格式
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b289e0d526d5906528b4112ddb56836ae1eca60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523834"
---
# <a name="manifest-file-format"></a>清单文件格式


## <span id="ddk_manifest_file_format_dtoolq"></span><span id="DDK_MANIFEST_FILE_FORMAT_DTOOLQ"></span>


清单文件的文件格式尽可能多地从 c + + 和 IDL 中继承。 因此，它是相当轻松地执行普通的 c + + SDK 标头文件和其修改为清单文件。 分析程序完全支持 C 和 c + + 样式注释，以帮助您组织和文档文件。

如果你尝试添加一个清单文件或对现有的文件进行更改，执行此操作的最佳方式是只是试验。 当您发出 **！ logexts.logi**或 **！ logexts.loge**命令在调试器中，记录器将尝试分析清单文件。 如果遇到问题，则会产生一条错误消息可能指示错误。

清单文件的以下基本元素组成： 模块标签、 分类标签、 函数声明、 COM 接口定义和类型定义。 其他类型的元素存在，但它们是最重要。

### <a name="span-idmodulelabelsspanspan-idmodulelabelsspanmodule-labels"></a><span id="module_labels"></span><span id="MODULE_LABELS"></span>模块标签

模块标签只需声明 DLL 所导出的之后声明的函数。 例如，如果你的清单文件用于记录来自 Comctl32.dll 的一组函数，应声明任何函数原型之前包括以下模块标签：

```cpp
module COMCTL32.DLL:
```

模块标签必须出现在清单文件中的任何函数声明之前。 清单文件可以包含任意数量的模块的标签。

### <a name="span-idcategorylabelsspanspan-idcategorylabelsspancategory-labels"></a><span id="category_labels"></span><span id="CATEGORY_LABELS"></span>类别标签

与模块标签类似，类别标签用于标识的所有后续函数和/或 COM 接口属于哪个"类别"。 例如，如果要创建的 Comctl32.dll 清单文件，您可以使用以下作为类别标签：

```cpp
category CommonControls:
```

清单文件可以包含任意数量的类别标签。

### <a name="span-idfunctiondeclarationsspanspan-idfunctiondeclarationsspanfunction-declarations"></a><span id="function_declarations"></span><span id="FUNCTION_DECLARATIONS"></span>函数声明

函数声明是什么情况下实际要求记录器以记录的内容。 它与几乎完全相同的 C/c + + 标头文件中找到的函数原型。 有几个值得注意的新增功能为格式，这可以最好地说明了下面的示例：

```cpp
HANDLE [gle] FindFirstFileA(
       LPCSTR lpFileName,
       [out] LPWIN32_FIND_DATAA lpFindFileData);
```

该函数**FindFirstFileA**采用两个参数。 第一个是*lpFileName*，它定义要搜索的文件或文件的位置是完整路径 （通常使用通配符）。 第二个是指向 WIN32\_查找\_DATAA 结构，它将用于包含搜索结果。 返回的句柄用于未来调用**FindNextFileA**。 如果**FindFirstFileA**返回无效\_处理\_值，则函数调用失败，错误代码可以通过调用采购**GetLastError**函数。

句柄类型声明，如下所示：

```cpp
value DWORD HANDLE
{
#define NULL                       0 [fail]
#define INVALID_HANDLE_VALUE      -1 [fail]
};
```

如果此函数返回的值为 0 或-1 (0xFFFFFFFF)，记录器将假定，该函数失败，因为此类值具有\[失败\]值声明中的修饰符。 （请参阅本节后面的值类型部分。）由于没有\[gle\]修饰符的函数名称之前，此函数使用记录器可识别**GetLastError**返回错误代码，以便它可以捕获错误代码并将其记录到日志文件。

\[出\]上的修饰符*lpFindFileData*参数将告知数据结构填充函数和函数返回时，应记录的记录器。

### <a name="span-idcominterfacedefinitionsspanspan-idcominterfacedefinitionsspancom-interface-definitions"></a><span id="com_interface_definitions"></span><span id="COM_INTERFACE_DEFINITIONS"></span>COM 接口定义

COM 接口基本上是 COM 对象的客户端可以调用的函数的向量。 清单格式很大程度利用从接口定义语言 (IDL) 在 COM 中用于定义接口。

请考虑下面的示例：

```cpp
interface IDispatch : IUnknown
{
    HRESULT GetTypeInfoCount( UINT pctinfo  );
 
    HRESULT GetTypeInfo(
        UINT iTInfo,
        LCID lcid,
        LPVOID ppTInfo );
 
    HRESULT GetIDsOfNames(
        REFIID riid,
        LPOLECHAR* rgszNames,
        UINT cNames,
        LCID lcid,
        [out] DISPID* rgDispId );
 
    HRESULT Invoke( 
        DISPID  dispIdMember,      
        REFIID  riid,              
        LCID  lcid,                
        WORD  wFlags,              
        DISPPARAMS*  pDispParams,  
        VARIANT*  pVarResult,  
        EXCEPINFO*  pExcepInfo,  
        UINT*  puArgErr );
};
```

这会将声明一个称为接口**IDispatch**派生自**IUnknown**。 它包含四个接口的大括号内的特定顺序中声明的成员函数。 记录器将截获，并记录这些成员函数通过将接口的 vtable （在运行时使用的函数指针的实际二进制向量） 中的函数指针替换为自己使用。 请参阅 COM\_接口\_PTR 类型部分稍后在本部分中有关如何记录器捕获接口，因为它们分发的详细信息。

### <a name="span-idtypedefinitionsspanspan-idtypedefinitionsspantype-definitions"></a><span id="type_definitions"></span><span id="TYPE_DEFINITIONS"></span>类型定义

定义数据类型是清单文件开发的最重要 （和最乏味） 部分。 清单的语言，可定义用户可读的标签的传入或从函数返回数字值。

例如，Winerror.h 定义一个名为"WinError"类型，它是大多数 Microsoft Win32 函数和其相应的用户可读标签返回的错误值的列表。 这允许记录器和日志查看器将说明性的错误代码替换为有意义的文本。

此外可以标记允许记录器的位掩码中的单个位和日志查看器以中断一个 dword 值，位掩码为其组件。

有 13 清单支持的基本类型。 下表中列出。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在任务栏的搜索框中键入</th>
<th align="left">长度</th>
<th align="left">显示示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>指针</p></td>
<td align="left"><p>4 个字节</p></td>
<td align="left"><p>0x001AF320</p></td>
</tr>
<tr class="even">
<td align="left"><p>VOID</p></td>
<td align="left"><p>0 字节</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>BYTE</p></td>
<td align="left"><p>1 个字节</p></td>
<td align="left"><p>0x32</p></td>
</tr>
<tr class="even">
<td align="left"><p>WORD</p></td>
<td align="left"><p>2 个字节</p></td>
<td align="left"><p>0x0A23</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DWORD</p></td>
<td align="left"><p>4 个字节</p></td>
<td align="left"><p>-234323</p></td>
</tr>
<tr class="even">
<td align="left"><p>BOOL</p></td>
<td align="left"><p>1 个字节</p></td>
<td align="left"><p><strong>TRUE</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>LPSTR</p></td>
<td align="left"><p>长度的字节以及任意数量的字符</p></td>
<td align="left"><p>&quot;快速 brown fox&quot;</p></td>
</tr>
<tr class="even">
<td align="left"><p>LPWSTR</p></td>
<td align="left"><p>长度的字节以及任意数量的 Unicode 字符</p></td>
<td align="left"><p>&quot;跳过那只懒狗&quot;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GUID</p></td>
<td align="left"><p>16 个字节</p></td>
<td align="left"><p>{0CF774D0-F077-11D1-B1BC-00C04F86C324}</p></td>
</tr>
<tr class="even">
<td align="left"><p>COM_INTERFACE_PTR</p></td>
<td align="left"><p>4 个字节</p></td>
<td align="left"><p>0x0203404A</p></td>
</tr>
<tr class="odd">
<td align="left"><p>value</p></td>
<td align="left"><p>相关的基类型</p></td>
<td align="left"><p>ERROR_TOO_MANY_OPEN_FILES</p></td>
</tr>
<tr class="even">
<td align="left"><p>掩码</p></td>
<td align="left"><p>相关的基类型</p></td>
<td align="left"><p>WS_MAXIMIZED | WS_ALWAYSONTOP</p></td>
</tr>
<tr class="odd">
<td align="left"><p>结构</p></td>
<td align="left"><p>根据封装类型的大小</p></td>
<td align="left"><p></p>
+ lpRect nLeft 34 nRight 54 nTop 100 nBottom 300</td>
</tr>
</tbody>
</table>

 

清单文件的工作中的类型定义，如 C/c + + typedef。 例如，下面的语句定义 PLONG 为指向 long 类型的值：

```cpp
typedef LONG *PLONG;
```

已在 Main.h 声明最基本的 typedef。 只需添加特定于你的组件的 typedef。 结构定义具有与 C/c + + 结构类型相同的格式。

有四种特殊类型： 值、 掩码、 GUID 和 COM\_接口\_PTR。

<span id="Value_Types"></span><span id="value_types"></span><span id="VALUE_TYPES"></span>值类型  
值为划分为人工可读的标签的基本类型。 大多数函数文档仅指**\#定义**函数中使用的特定常量的值。 例如，大多数程序员不了解什么是返回的所有代码的实际值**GetLastError**，使其无用，若要查看日志查看器中的含义模糊的数值。 清单值克服了这通过允许声明值如以下示例所示：

```cpp
value LONG ChangeNotifyFlags
{
#define SHCNF_IDLIST      0x0000        // LPITEMIDLIST
#define SHCNF_PATHA       0x0001        // path name
#define SHCNF_PRINTERA    0x0002        // printer friendly name
#define SHCNF_DWORD       0x0003        // DWORD
#define SHCNF_PATHW       0x0005        // path name
#define SHCNF_PRINTERW    0x0006        // printer friendly name
};
```

这会将声明一个称为"ChangeNotifyFlags"长时间从派生新类型。 如果这用作函数参数，用户可读的别名将显示而不是原始的数字。

<span id="Mask_Types"></span><span id="mask_types"></span><span id="MASK_TYPES"></span>掩码类型  
类似于值类型，掩码类型是划分为人工可读的标签具有含义的位的每个基本类型 （通常是一个 dword 值）。 执行下面的示例：

```cpp
mask DWORD DirectDrawOptSurfaceDescCapsFlags
{
#define DDOSDCAPS_OPTCOMPRESSED                 0x00000001
#define DDOSDCAPS_OPTREORDERED                  0x00000002
#define DDOSDCAPS_MONOLITHICMIPMAP              0x00000004
};
```

这会将声明从 DWORD，如果用作函数参数，将具有单个值划分日志查看器中的用户的派生的新类型。 因此，如果值为 0x00000005，将显示日志查看器：

```cpp
DDOSDCAPS_OPTCOMPRESSED | DDOSDCAPS_MONOLITHICMIPMAP
```

<span id="GUID_Types"></span><span id="guid_types"></span><span id="GUID_TYPES"></span>GUID 类型  
Guid 是 16 字节 com。 在广泛使用的全局唯一标识符 两种方式声明它们：

```cpp
struct __declspec(uuid("00020400-0000-0000-C000-000000000046")) IDispatch;
```

或者

```cpp
class __declspec(uuid("11219420-1768-11D1-95BE-00609797EA4F")) ShellLinkObject;
```

第一种方法用于声明接口标识符 (IID)。 当通过日志查看器，显示"IID\_"追加到显示名称的开头。 第二种方法用于声明类标识符 (CLSID)。 日志查看器将追加"CLSID\_"显示名称的开头。

GUID 类型是否为函数参数，日志查看器将针对所有声明的 Iid 和 Clsid 值进行比较。 如果找到匹配项，则它将显示 IID 友好名称。 如果没有，它将以标准 GUID 表示法显示 32 个十六进制字符值。

<span id="COM_INTERFACE_PTR_Types"></span><span id="com_interface_ptr_types"></span><span id="COM_INTERFACE_PTR_TYPES"></span>COM\_接口\_PTR 类型  
COM\_接口\_PTR 类型是一个 COM 接口指针的基类型。 声明一个 COM 接口时，实际定义新类型派生自 COM\_接口\_PTR。 在这种情况下，指针指向此类的类型可以是函数的参数。 如果 COM\_接口\_PTR 基本类型声明为 OUT 参数的函数，并且具有一个单独参数\[iid\]标签，记录器将比较传入的针对所有声明的 Guid 的 IID。 如果没有匹配项并且具有 IID 与相同的名称声明一个 COM 接口，记录器将挂接该接口中的所有函数，并记录。

下面是一个示例：

```cpp
STDAPI CoCreateInstance(
  REFCLSID rclsid,     //Class identifier (CLSID) of the object
  LPUNKNOWN pUnkOuter, //Pointer to controlling IUnknown
  CLSCTX dwClsContext, //Context for running executable code
  [iid] REFIID riid,   //Reference to the identifier of the interface
  [out] COM_INTERFACE_PTR * ppv
                       //Address of output variable that receives 
                       //the interface pointer requested in riid
);
```

在此示例中， *riid*已\[iid\]修饰符。 这将指示在返回的指针的记录器*ppv*是由标识的接口的 COM 接口指针*riid*。

还有可能声明函数，如下所示：

```cpp
DDRESULT DirectDrawCreateClipper( DWORD dwFlags, [out] LPDIRECTDRAWCLIPPER *lplpDDClipper, IUnknown *pUnkOuter );
```

在此示例中，LPDIRECTDRAWCLIPPER 定义为指向**IDirectDrawClipper**接口。 由于记录器可以标识要返回哪些接口类型*lplpDDClipper*参数，则无需\[iid\]上的任何其他参数修饰符。

 

 





