---
title: INF UnregisterDlls 指令
description: UnregisterDlls 指令将引用一个或多个 INF 部分，这些部分用于指定作为 OLE 控件并且需要自行注销（自行删除）的文件。
ms.assetid: 11d29c7f-9bd8-4097-9842-ce7431389241
keywords:
- INF UnregisterDlls 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF UnregisterDlls Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 171c09d7f432d20853dd65e9a5c395808a1808e7
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223085"
---
# <a name="inf-unregisterdlls-directive"></a>INF UnregisterDlls 指令


**注意：**  如果要生成通用或移动驱动程序包，则此指令无效。 请参阅[使用通用 INF 文件](using-a-universal-inf-file.md)。

 

**UnregisterDlls**指令将引用一个或多个 INF 部分，这些部分用于指定作为 OLE 控件并且需要自行注销（自行删除）的文件。

```inf
[DDInstall]
  
UnregisterDlls=unregister-dll-section[,unregister-dll-section]...
```

**UnregisterDlls**指令引用的每个 INF 部分都必须具有以下条目格式：

```inf
[unregister-dll-section] 
  
dirid,[subdir],filename,registration-flags[,[timeout][,argument]] 
```

一个*取消注册 dll 部分*可以有任意数量的条目，每个条目都在单独的行上。

## <a name="entries"></a>条目


<a href="" id="dirid"></a>*dirid*  
指定要注销的文件的目标目录 ID。 有关详细信息，请参阅[Using Dirids](using-dirids.md)。

<a href="" id="subdir"></a>*subdir*  
指定要注销的文件的相对于当前目录的目录路径。 如果未指定，则文件位于当前目录中。

<a href="" id="filename"></a>*名字*  
标识要注销的 OLE 控件的文件名。

<a href="" id="registration-flags"></a>*注册标志*  
指示要对 OLE 控件执行的注册操作。 必须指定以下一个或两个标志。

<a href="" id="0x00000001--flg-regsvr-dllregister-"></a>**0x00000001** （FLG_REGSVR_DLLREGISTER）  
调用**DllUnRegisterServer**函数（如 Windows SDK 文档中所述）。

<a href="" id="0x00000002--flg-regsvr-dllinstall--"></a>**0x00000002** （FLG_REGSVR_DLLINSTALL）   
调用 OLE 控件的**DllInstall**函数（如 Windows SDK 文档中所述）。

<a href="" id="timeout"></a>*timeout*  
指定 OLE 控件完成指定的注销调用的超时时间，以秒为单位。 默认超时值为60秒。

<a href="" id="argument"></a>*实际*  
如果控件是可执行文件，则这是传递给可执行文件的命令字符串。 默认参数为 **/UnRegServer**。

如果控件不是可执行文件，则此参数指定要传递给**DllInstall**函数的命令行参数。

<a name="remarks"></a>备注
-------

每个*取消注册 dll 节*名称对于 INF 文件必须唯一，并且必须遵循用于定义节名称的常规规则。 有关这些规则的详细信息，请参阅[INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

有关 OLE 控件和自行注销的详细信息，请参阅 Windows SDK 文档。

<a name="examples"></a>示例
--------

```inf
[Dialer]
RegisterDlls = DialerRegSvr

[DialerUninstall]
UnregisterDlls = DialerRegSvr

[DialerRegSvr]
11,,avtapi.dll, 1
```

## <a name="see-also"></a>另请参阅


[**RegisterDlls**](inf-registerdlls-directive.md)

 

 






