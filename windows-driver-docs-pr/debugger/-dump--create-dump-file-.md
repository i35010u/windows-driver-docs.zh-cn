---
title: .dump（创建转储文件）
description: Dump 命令创建用户模式或内核模式故障转储文件。
ms.assetid: df6bcf7f-eb2e-4605-87a0-c0a7e9e4776b
keywords:
- 创建转储文件（dump）命令
- 转储文件，创建转储文件（dump）命令
- 。转储（创建转储文件） Windows 调试
ms.date: 08/01/2018
topic_type:
- apiref
api_name:
- .dump (Create Dump File)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: edbe1c9c7a3d2adc25a46bab2d535c2337842542
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968045"
---
# <a name="dump-create-dump-file"></a>.dump（创建转储文件）


**Dump**命令创建用户模式或内核模式故障转储文件。

```dbgcmd
.dump Options FileName 
.dump /?
```

## <a name="span-idddk_meta_create_dump_file_dbgspanspan-idddk_meta_create_dump_file_dbgspanparameters"></a><span id="ddk_meta_create_dump_file_dbg"></span><span id="DDK_META_CREATE_DUMP_FILE_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
表示以下一个或多个选项

<span id="_o"></span><span id="_O"></span>**/o**  
覆盖具有相同名称的现有转储文件。 如果未使用此选项，且文件名称相同，则不会写入转储文件。

<span id="_f_FullOptions_"></span><span id="_f_fulloptions_"></span><span id="_F_FULLOPTIONS_"></span>**/f \[ **<em>FullOptions</em>**\]**  
（内核模式：）创建[完整的内存转储](complete-memory-dump.md)。

（用户模式：）创建*完整的用户模式转储*。 有关详细信息，请参阅[用户模式转储文件的种类](user-mode-dump-files.md#varieties)。 尽管名称相同，但最大的小型转储文件实际上包含了比完整用户模式转储更多的信息。 例如， **dump/mf**或 **/ma**创建的文件比**转储/f**大，更完整。 在用户模式下， **. 转储** **/m \[ **<em>MiniOptions</em> **\]** 始终优于 **. 转储/f**。

可以添加以下*FullOptions*来更改转储文件的内容;选项区分大小写。

**FullOption**：效果

**y**：将 AVX 寄存器信息添加到转储文件。

 

<span id="_m_MiniOptions_"></span><span id="_m_minioptions_"></span><span id="_M_MINIOPTIONS_"></span>**/m \[ **<em>MiniOptions</em>**\]**  
创建*小型内存转储*（在内核模式下）或*小型转储*（处于用户模式）。有关详细信息，请参阅[用户模式转储文件](user-mode-dump-files.md)。 如果不指定 **/f**和 **/m** ，则默认值为 **/m** 。

在用户模式下， **/m**可以后跟额外的*MiniOptions* ，以指定要包含在转储中的额外数据。 如果未包括*MiniOptions* ，则转储将包含模块、线程和堆栈信息，但不包含其他数据。 可以添加以下任何*MiniOptions*来更改转储文件的内容;它们区分大小写。

|MiniOption|效果|
|--- |--- |
|a|创建包含所有可选添加项的小型转储。 /Ma 选项等效于/mfFhut--它将完整内存数据、处理数据、卸载的模块信息、基本内存信息和线程时间信息添加到小型转储。 读取无法访问内存的任何失败都将导致小型转储生成终止。|
|A|/MA 选项等效于/mA，只不过它会忽略读取无法访问内存的任何失败并继续生成小型转储。|
|f|将完整内存数据添加到小型转储。 将包括目标应用程序拥有的所有可访问的已提交页面。|
|F|将所有基本内存信息添加到小型转储。 这会将流添加到小型转储，其中包含所有基本内存信息，而不仅仅是有关有效内存的信息。 这使调试器能够在调试小型转储时重新构造进程的完整虚拟内存布局。|
|h|将有关与目标应用程序关联的句柄的数据添加到小型转储。|
|u|将卸载的模块信息添加到小型转储。 此功能仅在 Windows Server 2003 和更高版本的 Windows 中可用。|
|T|向小型转储添加其他线程信息。 这包括线程时间，在调试小型转储时，可以使用！失控扩展或 ttime （显示线程时间）命令来显示线程时间。|
|i|将辅助内存添加到小型转储。 "辅助内存" 是指堆栈或后备存储中的指针所引用的任何内存以及此地址周围的小区域。|
|p|将进程环境块（PEB）和线程环境块（TEB）数据添加到小型转储。 如果需要访问有关应用程序进程和线程的 Windows 系统信息，这会很有用。|
|w|将所有提交的读写专用页面添加到小型转储。|
|d|将可执行映像内的所有读写数据段添加到小型转储。|
|c|在图像中添加代码段。|
|r|从小型转储中删除堆栈的部分，并存储用于重新创建堆栈跟踪的内存。 还会删除本地变量和其他数据类型值。 此选项不会使小型转储更小（因为这些内存部分只是归零），但如果你想要保护其他应用程序的隐私，则此选项很有用。|
|R|从小型转储中删除完整的模块路径。 只包含模块名称。 如果要保护用户的目录结构的隐私，这是一个非常有用的选项。|
|y|将 AVX 寄存器信息添加到转储文件。|

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关内核模式转储文件的说明和其用法的说明，请参阅[内核模式转储文件](kernel-mode-dump-files.md)。 有关用户模式转储文件的说明和其用法的说明，请参阅[用户模式转储文件](user-mode-dump-files.md)。

## <a name="remarks"></a>备注
-------

此命令可在各种情况下使用：

-   在实时用户模式调试期间，此命令指示目标应用程序生成转储文件，但目标应用程序不会终止。

-   在实时内核模式调试期间，此命令指示目标计算机生成转储文件，但目标计算机不会崩溃。

-   在故障转储调试过程中，此命令从旧的故障转储文件中创建新的故障转储文件。 如果你有一个较大的故障转储文件，并且想要创建一个较小的转储文件，这会很有用。

可以控制将生成的转储文件的类型：

- 在内核模式下，若要生成[完整的内存转储](complete-memory-dump.md)，请使用 **/f**选项。 若要生成[小内存转储](small-memory-dump.md)，请使用 **/m**选项（或 "无选项"）。 Dump 命令无法生成[内核内存转储](kernel-memory-dump.md)。

- 在用户模式下，**转储** **/m \[ **<em>MiniOptions</em> **\]** 是最佳选择。 尽管 "m" 代表 "小型转储"，但使用此*MiniOption*创建的转储文件的大小可能不同于非常小到非常大。 通过指定正确的*MiniOptions* ，你可以精确控制所包含的信息。 例如， **dump/ma**生成包含大量信息的转储。 旧的命令 " **dump/f**" 生成一个适度的 "标准转储" 文件，并且无法对其进行自定义。

无法指定转储的进程。 所有正在运行的进程都将转储。

**/Xc**、 **/xr**、 **/xp**和 **/xt**选项用于将异常和上下文信息存储在转储文件中。 这允许在此转储文件上运行[**ecxr （显示异常上下文记录）**](-ecxr--display-exception-context-record-.md)命令。

下面的示例将创建一个用户模式小型转储，其中包含完整内存和句柄信息：

```dbgcmd
0:000> .dump /mfh myfile.dmp 
```

可以使用[**！ handle**](-handle.md) extension 命令读取句柄信息。

 

 





