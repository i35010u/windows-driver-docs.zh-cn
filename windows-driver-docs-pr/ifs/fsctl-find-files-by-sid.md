---
title: FSCTL_FIND_FILES_BY_SID 控制代码
description: FSCTL \_ \_ \_ 按 \_ SID 控制代码查找文件在目录中搜索其创建者和所有者 matche 指定 SID 的文件。
ms.assetid: fe0953d3-a009-431b-b03b-5d827dc732a1
keywords:
- FSCTL_FIND_FILES_BY_SID 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_FIND_FILES_BY_SID
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee07ea4edbb81bd330bc77fc0ead4807eb023065
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065594"
---
# <a name="fsctl_find_files_by_sid-control-code"></a>FSCTL \_ \_ \_ 按 \_ SID 控制代码查找文件


FSCTL \_ \_ \_ 按 \_ SID 控制代码查找文件在目录中搜索其创建者和所有者 matche 指定 SID 的文件。

要执行此操作，微筛选器驱动程序将调用 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 与以下参数、文件系统、重定向程序和旧文件系统筛选器驱动程序调用 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) ，并提供以下参数。

**参数**

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 要搜索的目录的文件对象指针。 此参数是必需的，不能为 **NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 要搜索的目录的文件句柄。 此参数是必需的，不能为 **NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL \_ \_ \_ 按 SID 查找 \_ 此操作的文件。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向输入缓冲区的指针，该缓冲区由 \_ \_ SID 数据结构的查找描述 \_ 。 " \_ 按 SID 查找" \_ \_ 数据结构定义如下：

```cpp
typedef struct {
  DWORD  ;
  SID  ;
} FIND_BY_SID_DATA, *PFIND_BY_SID_DATA;
```

**成员**

<a href="" id="restart"></a>**重新启动**  
指示是否要重新启动搜索。 第一次调用时，此成员应设置为1，以便从根开始搜索。 对于后续调用，应将此成员设置为零，以便搜索将在停止时恢复。

<a href="" id="sid-"></a>**Sid**   
指定创建者和所有者的 [**SID**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_sid) 类型的结构。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
*InputBuffer*缓冲区的长度（以字节为单位）。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
一个指针， \_ 它指向由 \_ SID \_ 输出结构（接收每个文件的完全限定的路径名称）的、由 " \_ 按 SID 查找" \_ \_ 输出结构的定义如下所示：

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
要转到下一条记录必须跳过的字节数。 如果值为零，则表示这是最后一条记录。

<a href="" id="fileindex-"></a>**FileIndex**   
文件的索引。

<a href="" id="filenamelength-"></a>**FileNameLength**   
文件名的大小（以字节为单位）。

<a href="" id="filename-"></a>**名字**   
一个以 null 结尾的字符串，它指定文件名。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer*参数指向的缓冲区中返回的数据的大小（以字节为单位）。

<a name="remarks"></a>备注
-------

当 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 和 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 处理 **FSCTL \_ \_ \_ 按 \_ SID 控制代码查找文件** 时，这些例程会检查卷上的每个文件和目录。 如果卷上有多个文件，即使要搜索的目录非常小，此操作的速度可能会很慢。

## <a name="see-also"></a>另请参阅


[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**SID**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_sid)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

 

