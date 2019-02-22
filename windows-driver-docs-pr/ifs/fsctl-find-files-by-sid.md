---
title: FSCTL_FIND_FILES_BY_SID 控制代码
description: FSCTL\_查找\_文件\_BY\_SID 控件代码目录中搜索的文件的创建者和所有者匹配出现指定的 SID。
ms.assetid: fe0953d3-a009-431b-b03b-5d827dc732a1
keywords:
- FSCTL_FIND_FILES_BY_SID 控制代码可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_FIND_FILES_BY_SID
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97833e2dae3f018a93f95e17e1d6684273034f2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554124"
---
# <a name="fsctlfindfilesbysid-control-code"></a>FSCTL\_查找\_文件\_BY\_SID 控制代码


FSCTL\_查找\_文件\_BY\_SID 控件代码目录中搜索的文件的创建者和所有者匹配出现指定的 SID。

若要执行此操作，微筛选器驱动程序调用[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)与以下参数和文件系统中，重定向程序和旧的文件系统筛选驱动程序调用[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)使用以下参数。

**参数**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)仅。 要搜索的目录文件对象指针。 此参数是必需的不能**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)仅。 要搜索的目录文件句柄。 此参数是必需的不能**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
该操作控制代码。 使用 FSCTL\_查找\_文件\_BY\_SID 对此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区中查找描述\_BY\_SID\_数据结构。 查找\_BY\_SID\_数据结构定义，如下所示：

```cpp
typedef struct {
  DWORD  ;
  SID  ;
} FIND_BY_SID_DATA, *PFIND_BY_SID_DATA;
```

**成员**

<a href="" id="restart"></a>**重新启动**  
指示是否要重新启动搜索。 此成员应设置为 1，第一次调用，以便从根目录开始搜索。 以便进行后续调用，应将此成员设置为零，以便搜索将停止的位置的点处恢复。

<a href="" id="sid-"></a>**sid**   
类型的结构[ **SID** ](https://msdn.microsoft.com/library/windows/hardware/ff556740) ，指定的创建者和所有者。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
在缓冲区的长度，以字节为单位， *InputBuffer*。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
指向调用方分配的四对齐查找数组的指针\_BY\_SID\_接收的每个文件的完全限定的路径名称的输出结构。 查找\_BY\_SID\_输出结构定义，如下所示：

```cpp
typedef struct _FIND_BY_SID_OUTPUT {
  DWORD  ;
  DWORD  ;
  DWORD  ;
  WCHAR  [1];
} FIND_BY_SID_OUTPUT, *PFIND_BY_SID_OUTPUT;
```

**成员**

<a href="" id="nextentryoffset"></a>**NextEntryOffset**  
必须跳过以转到下一条记录的字节数。 零值指示这是最后一条记录。

<a href="" id="fileindex-"></a>**FileIndex**   
该文件的索引。

<a href="" id="filenamelength-"></a>**FileNameLength**   
文件名称，以字节为单位的大小。

<a href="" id="filename-"></a>**FileName**   
一个以 null 结尾的字符串，指定的文件的名称。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
大小 （字节），返回所指向的缓冲区中的数据*OutputBuffer*参数。

<a name="remarks"></a>备注
-------

当[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)并[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)过程**FSCTL\_查找\_文件\_BY\_SID**控制代码，这些例程检查每个文件和目录的卷上。 即使要搜索的目录是非常小，此操作可能很慢，如果有多个文件的卷上。

## <a name="see-also"></a>另请参阅


[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**SID**](https://msdn.microsoft.com/library/windows/hardware/ff556740)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






