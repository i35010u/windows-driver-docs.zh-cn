---
title: 清单文件格式
description: 清单文件格式
keywords:
- LogViewer，清单，文件格式
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d90822babf19a20cafc256cc7cf57d7ed64fa7b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814571"
---
# <a name="manifest-file-format"></a>清单文件格式


## <span id="ddk_manifest_file_format_dtoolq"></span><span id="DDK_MANIFEST_FILE_FORMAT_DTOOLQ"></span>


清单文件的文件格式与 c + + 和 IDL 的文件格式的借用大致相同。 这样，就可以轻松地使用普通的 c + + SDK 标头文件，并将其修改为清单文件。 分析器完全支持 C 和 c + + 样式注释，以帮助您组织和记录文件。

如果尝试添加清单文件或对现有文件进行更改，最佳方法是只进行试验。 当在调试器中发出 **！ logexts** 或 **loge** 命令时，记录器将尝试分析清单文件。 如果遇到问题，它将生成一条错误消息，指示错误。

清单文件由以下基本元素组成：模块标签、类别标签、函数声明、COM 接口定义和类型定义。 其他类型的元素也存在，但它们是最重要的。

### <a name="span-idmodule_labelsspanspan-idmodule_labelsspanmodule-labels"></a><span id="module_labels"></span><span id="MODULE_LABELS"></span>模块标签

模块标签只是声明哪些 DLL 导出此后声明的函数。 例如，如果清单文件用于记录 Comctl32.dll 的一组函数，则在声明任何函数原型之前，您将包括以下模块标签：

```cpp
module COMCTL32.DLL:
```

模块标签必须出现在清单文件中的任何函数声明之前。 清单文件可以包含任意数量的模块标签。

### <a name="span-idcategory_labelsspanspan-idcategory_labelsspancategory-labels"></a><span id="category_labels"></span><span id="CATEGORY_LABELS"></span>类别标签

与模块标签类似，类别标签标识所有后续的函数和/或 COM 接口所属的 "category"。 例如，如果要创建 Comctl32.dll 清单文件，则可以使用以下作为类别标签：

```cpp
category CommonControls:
```

清单文件可以包含任意数量的类别标签。

### <a name="span-idfunction_declarationsspanspan-idfunction_declarationsspanfunction-declarations"></a><span id="function_declarations"></span><span id="FUNCTION_DECLARATIONS"></span>函数声明

函数声明实际上会提示记录器记录某些内容。 它与在 C/c + + 头文件中找到的函数原型几乎完全相同。 这种格式有一些值得注意的内容，下面的示例对此进行了说明：

```cpp
HANDLE [gle] FindFirstFileA(
       LPCSTR lpFileName,
       [out] LPWIN32_FIND_DATAA lpFindFileData);
```

函数 **FindFirstFileA** 使用两个参数。 第一个是 *lpFileName*，它是一个完整路径 (通常使用通配符) 定义文件或文件的搜索位置。 第二个是指向 WIN32 \_ FIND \_ DATAA 结构的指针，该结构将用于包含搜索结果。 返回的句柄用于以后对 **FindNextFileA** 的调用。 如果 **FindFirstFileA** 返回无效 \_ 的句柄 \_ 值，则函数调用失败，并通过调用 **GetLastError** 函数来采购错误代码。

句柄类型的声明方式如下：

```cpp
value DWORD HANDLE
{
#define NULL                       0 [fail]
#define INVALID_HANDLE_VALUE      -1 [fail]
};
```

如果此函数返回的值为0或-1 (0xFFFFFFFF) ，则记录器将假定函数失败，因为此类值 \[ \] 在值声明中具有 fail 修饰符。  (参阅本部分后面的 "值类型" 一节。 ) 由于 \[ \] 函数名称前有一个 gle 修饰符，因此记录器识别此函数使用 **GetLastError** 来返回错误代码，因此它捕获错误代码并将其记录到日志文件中。

\[ \] *LpFindFileData* 参数上的 out 修饰符通知记录器数据结构由函数填充，并且应在函数返回时进行记录。

### <a name="span-idcom_interface_definitionsspanspan-idcom_interface_definitionsspancom-interface-definitions"></a><span id="com_interface_definitions"></span><span id="COM_INTERFACE_DEFINITIONS"></span>COM 接口定义

COM 接口本质上是可由 COM 对象的客户端调用的函数的矢量。 清单格式在 COM 中使用的接口定义语言 (IDL) 用于定义接口。

请考虑以下示例：

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

这将声明一个名为 **IDispatch** 的接口，该接口派生自 **IUnknown**。 它包含四个成员函数，这些函数在接口的大括号内按特定顺序声明。 记录器将通过替换接口的 vtable 中的函数指针来截获并记录这些成员函数 (在运行时使用的函数指针的实际二进制向量) 使用其自己的。 请参阅 \_ 本部分后面的 "COM 接口 \_ PTR 类型" 一节，了解有关记录器如何捕获接口的详细信息。

### <a name="span-idtype_definitionsspanspan-idtype_definitionsspantype-definitions"></a><span id="type_definitions"></span><span id="TYPE_DEFINITIONS"></span>类型定义

定义数据类型是清单文件开发最重要的 (和最枯燥的) 部分。 使用清单语言，可以为传入或从函数返回的数值定义用户可读标签。

例如，Winerror.h 定义了一个名为 "Winerror.h" 的类型，该类型是由大多数 Microsoft Win32 函数返回的错误值的列表及其相应的用户可读标签。 这允许记录器和 LogViewer 将 uninformative 错误代码替换为有意义的文本。

你还可以在位掩码中标记各个位，以允许记录器和 LogViewer 将 DWORD 位掩码分解为其组件。

清单支持13种基本类型。 下表中列出了这些字段。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">类型</th>
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
<td align="left"><p>导致</p></td>
<td align="left"><p>0字节</p></td>
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
<td align="left"><p>长度字节加任意多个字符</p></td>
<td align="left"><p>"快速棕色 fox"</p></td>
</tr>
<tr class="even">
<td align="left"><p>LPWSTR</p></td>
<td align="left"><p>长度字节加任意数量的 Unicode 字符</p></td>
<td align="left"><p>"在懒惰狗上跳过"</p></td>
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
<td align="left"><p>值</p></td>
<td align="left"><p>依赖于基类型</p></td>
<td align="left"><p>ERROR_TOO_MANY_OPEN_FILES</p></td>
</tr>
<tr class="even">
<td align="left"><p>掩码</p></td>
<td align="left"><p>依赖于基类型</p></td>
<td align="left"><p>WS_MAXIMIZED |WS_ALWAYSONTOP</p></td>
</tr>
<tr class="odd">
<td align="left"><p>struct</p></td>
<td align="left"><p>依赖于封装类型的大小</p></td>
<td align="left"><p></p>
+ lpRect nLeft 34 nRight 54 nTop 100 nBottom 300</td>
</tr>
</tbody>
</table>

 

清单文件中的类型定义的工作方式类似于 C/c + + typedef。 例如，下面的语句将 PLONG 定义为指向 LONG 的指针：

```cpp
typedef LONG *PLONG;
```

大多数基本的 typedef 已在 Main .h 中声明。 仅需添加特定于你的组件的 typedef。 结构定义与 C/c + + 结构类型具有相同的格式。

有四种特殊类型：值、掩码、GUID 和 COM \_ 接口 \_ PTR。

<span id="Value_Types"></span><span id="value_types"></span><span id="VALUE_TYPES"></span>值类型  
值是指分为用户可读标签的基本类型。 大多数函数文档仅指函数中使用的特定常量的 **\# 定义** 值。 例如，大多数程序员不知道由 **GetLastError** 返回的所有代码的实际值是什么，这使得它无用在 LogViewer 中查看一个不确定的数值。 清单值通过允许值声明（如以下示例中所示）来克服这一点：

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

这将声明一个名为 "ChangeNotifyFlags" 的新类型，该类型派生自 LONG。 如果将此用作函数参数，则将显示用户可读的别名，而不是原始数字。

<span id="Mask_Types"></span><span id="mask_types"></span><span id="MASK_TYPES"></span>掩码类型  
类似于值类型，掩码类型是一种基本类型 (通常是一种 DWORD) ，它会被分割为每个有意义的位的用户可读标签。 执行以下示例：

```cpp
mask DWORD DirectDrawOptSurfaceDescCapsFlags
{
#define DDOSDCAPS_OPTCOMPRESSED                 0x00000001
#define DDOSDCAPS_OPTREORDERED                  0x00000002
#define DDOSDCAPS_MONOLITHICMIPMAP              0x00000004
};
```

这会声明从 DWORD 派生的新类型（如果用作函数参数），将会在 LogViewer 中为用户细分各个值。 因此，如果值为0x00000005，则 LogViewer 将显示：

```cpp
DDOSDCAPS_OPTCOMPRESSED | DDOSDCAPS_MONOLITHICMIPMAP
```

<span id="GUID_Types"></span><span id="guid_types"></span><span id="GUID_TYPES"></span>GUID 类型  
Guid 是在 COM 中广泛使用的16字节全局唯一标识符。 它们通过两种方式进行声明：

```cpp
struct __declspec(uuid("00020400-0000-0000-C000-000000000046")) IDispatch;
```

或

```cpp
class __declspec(uuid("11219420-1768-11D1-95BE-00609797EA4F")) ShellLinkObject;
```

第一种方法用于声明 (IID) 的接口标识符。 当 LogViewer 显示 "IID" 时，将在 \_ 显示名称的开头追加 "IID"。 第二种方法用于声明类标识符 (CLSID) 。 LogViewer \_ 在显示名称的开头追加 "CLSID"。

如果 GUID 类型是函数的参数，则 LogViewer 会将值与所有已声明的 Iid 和 Clsid 进行比较。 如果找到匹配项，它将显示 IID 友好名称。 否则，它将在标准 GUID 表示法中显示 32-十六进制字符值。

<span id="COM_INTERFACE_PTR_Types"></span><span id="com_interface_ptr_types"></span><span id="COM_INTERFACE_PTR_TYPES"></span>COM \_ 接口 \_ PTR 类型  
COM \_ 接口 \_ PTR 类型是 com 接口指针的基类型。 当你声明一个 COM 接口时，实际上是在定义一个从 COM 接口 PTR 派生的新类型 \_ \_ 。 因此，指向此类类型的指针可以是函数的参数。 如果将 COM \_ 接口 \_ PTR 基本类型声明为函数的 OUT 参数，并且有一个单独的参数具有 \[ iid \] 标签，则记录器会将传入的 iid 与所有声明的 guid 进行比较。 如果存在匹配项，并且声明与 IID 同名的 COM 接口，则记录器将挂钩该接口中的所有函数并记录这些函数。

以下是示例：

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

在此示例中， *riid* 具有 \[ iid \] 修饰符。 这指示在 *ppv* 中返回的指针是由 *riid* 标识的接口的 COM 接口指针。

还可以按如下所示声明函数：

```cpp
DDRESULT DirectDrawCreateClipper( DWORD dwFlags, [out] LPDIRECTDRAWCLIPPER *lplpDDClipper, IUnknown *pUnkOuter );
```

在此示例中，LPDIRECTDRAWCLIPPER 定义为指向 **IDirectDrawClipper** 接口的指针。 由于记录器可以标识在 *lplpDDClipper* 参数中返回的接口类型，因此不需要对 \[ \] 任何其他参数使用 iid 修饰符。

 

 





