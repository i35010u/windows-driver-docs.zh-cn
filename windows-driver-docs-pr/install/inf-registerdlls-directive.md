---
title: INF RegisterDlls 指令
description: RegisterDlls 指令引用用来指定 OLE 控件并需要自行注册的文件的一个或多个 INF 部分。
ms.assetid: 59da13e6-f801-4efe-8cd3-d0305e503c24
keywords:
- INF RegisterDlls 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF RegisterDlls Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89ec7c7fe0ad0ac159c2cbfad20016c06b3895f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563919"
---
# <a name="inf-registerdlls-directive"></a>INF RegisterDlls 指令


**请注意**  如果要构建一个通用或移动设备的驱动程序包，此指令无效。 可以使用[Reg2inf 工具](../devtest/reg2inf.md)要转换现有[INF RegisterDlls 指令](../install/inf-registerdlls-directive.md)到[INF AddReg 指令](../install/inf-addreg-directive.md)以使驱动程序包通用。  有关详细信息，请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

一个**RegisterDlls**指令引用用来指定 OLE 控件并需要自行注册的文件的一个或多个 INF 部分。

```ini
[DDInstall]
  
RegisterDlls=register-dll-section[,register-dll-section]...
```

引用的每个 INF 部分**RegisterDlls**指令必须具有以下条目格式：

```ini
[register-dll-section] 
  
dirid,[subdir],filename,registration-flags[,[timeout][,argument]] 
```

一个*注册 dll 部分*可以有任意数量的条目，每个单独的行上。

## <a name="entries"></a>条目


<a href="" id="dirid"></a>*dirid*  
指定要注册该文件的目标目录 ID。 有关详细信息，请参阅[使用 Dirids](using-dirids.md)。

<a href="" id="subdir"></a>*subdir*  
指定的目录路径，相对于当前目录中，要注册的文件。 如果未指定，该文件是当前目录中。

<a href="" id="filename"></a>*filename*  
标识要注册 OLE 控件的文件名称。

<a href="" id="registration-flags"></a>*registration-flags*  
指示 OLE 控件上执行注册操作。 必须指定一个或两个以下的标志。

<a href="" id="0x00000001--flg-regsvr-dllregister-"></a>**0x00000001** (FLG_REGSVR_DLLREGISTER)  
调用 OLE 控件的**DllRegisterServer**函数 （Windows SDK 文档中所述）。

<a href="" id="0x00000002--flg-regsvr-dllinstall--"></a>**0x00000002** (FLG_REGSVR_DLLINSTALL)   
调用 OLE 控件的**DllInstall**函数 （Windows SDK 文档中所述）。

<a href="" id="timeout"></a>*timeout*  
指定超时，单位为秒，OLE 控件以完成指定的注册调用。 默认超时值为 60 秒。

<a href="" id="argument"></a>*自变量*  
如果控件是可执行文件，这是传递给可执行文件的命令字符串。 默认自变量是 **/RegServer**。

如果控件不是可执行文件，此参数指定命令行参数来传递给**DllInstall**函数。

<a name="remarks"></a>备注
-------

每个*注册 dll 部分*名称必须是唯一的 INF 文件和必须遵从常规规则，用于定义的节名称。 有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

以下规则适用于使用**RegisterDlls**指令对于设备安装：

-   尽管语法允许为一个 DLL 或可执行文件的文件名，但对于设备安装被允许仅 DLL。
-   若要注册的代码必须提示用户输入。
-   在系统上下文中执行服务器端的安装。 因此，您必须非常确信要注册的代码包含任何安全漏洞和文件权限防止代码的恶意修改。

关于 OLE 控件和自助注册的详细信息，请参阅 Windows SDK 文档。

<a name="examples"></a>示例
--------

```ini
[Dialer]
RegisterDlls = DialerRegSvr
[DialerUninstall]
UnregisterDlls = DialerRegSvr
[DialerRegSvr]
11,,avtapi.dll, 1
```

## <a name="see-also"></a>请参阅


[**UnregisterDlls**](inf-unregisterdlls-directive.md)

 

 






