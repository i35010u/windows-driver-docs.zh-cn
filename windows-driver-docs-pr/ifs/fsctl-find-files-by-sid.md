---
title: FSCTL_FIND_FILES_BY_SID 控制代码
description: FSCTL\_\_\_通过\_SID 控制代码在目录中搜索其创建者和所有者 matche 指定 SID 的文件。
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
ms.openlocfilehash: 64fe5299f09585574e7effbdbacd272ecd1f677f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841310"
---
# <a name="fsctl_find_files_by_sid-control-code"></a>FSCTL\_通过\_SID 控制代码查找\_文件\_


FSCTL\_\_\_通过\_SID 控制代码在目录中搜索其创建者和所有者 matche 指定 SID 的文件。

要执行此操作，微筛选器驱动程序将调用[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)与以下参数、文件系统、重定向程序和旧文件系统筛选器驱动程序调用[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) ，并提供以下参数。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
仅[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 要搜索的目录的文件对象指针。 此参数是必需的，不能为**NULL**。

<a href="" id="filehandle"></a>*FileHandle*  
仅[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462) 。 要搜索的目录的文件句柄。 此参数是必需的，不能为**NULL**。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作的控制代码。 使用 FSCTL\_通过此操作\_SID 查找\_\_文件。

<a href="" id="inputbuffer"></a>*InputBuffer*  
一个指向输入缓冲区的指针，该指针由 FIND\_通过\_SID\_数据结构进行描述。 \_SID\_数据结构的 "查找\_" 定义如下：

```cpp
typedef struct {
  DWORD  ;
  SID  ;
} FIND_BY_SID_DATA, *PFIND_BY_SID_DATA;
```

**组员**

<a href="" id="restart"></a>**重新启动**  
指示是否要重新启动搜索。 第一次调用时，此成员应设置为1，以便从根开始搜索。 对于后续调用，应将此成员设置为零，以便搜索将在停止时恢复。

<a href="" id="sid-"></a>**Sid**   
指定创建者和所有者的[**SID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_sid)类型的结构。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
*InputBuffer*缓冲区的长度（以字节为单位）。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
一个指针，该指针指向由\_四个部分组成的、通过\_SID\_输出结构的调用方分配的、用于接收每个文件的完全限定路径名称的输出结构的数组。 \_SID\_输出结构的 "查找\_" 定义如下：

```cpp
typedef struct _FIND_BY_SID_OUTPUT {
  DWORD  ;
  DWORD  ;
  DWORD  ;
  WCHAR  [1];
} FIND_BY_SID_OUTPUT, *PFIND_BY_SID_OUTPUT;
```

**组员**

<a href="" id="nextentryoffset"></a>**NextEntryOffset**  
要转到下一条记录必须跳过的字节数。 如果值为零，则表示这是最后一条记录。

<a href="" id="fileindex-"></a>**FileIndex**   
文件的索引。

<a href="" id="filenamelength-"></a>**FileNameLength**   
文件名的大小（以字节为单位）。

<a href="" id="filename-"></a>**文件名**   
一个以 null 结尾的字符串，它指定文件名。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
*OutputBuffer*参数指向的缓冲区中返回的数据的大小（以字节为单位）。

<a name="remarks"></a>备注
-------

当[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)和[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)处理**FSCTL\_通过\_SID 控制代码查找\_文件\_** 时，这些例程会检查卷上的每个文件和目录。 如果卷上有多个文件，即使要搜索的目录非常小，此操作的速度可能会很慢。

## <a name="see-also"></a>另请参阅


[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**SID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_sid)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






